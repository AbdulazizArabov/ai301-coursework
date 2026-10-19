# Plan for #72: `verify_password()` raises `UnknownHashError` on a malformed stored hash

## Repro evidence I rely on

From my posted repro comment on #72 (Windows 11 10.0.26200.9711, Python 3.14.4, passlib 1.7.4, bcrypt 4.3.0, pytest 9.1.1, main at commit 2f4e82f):

```
$ pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format --runxfail
>           raise exc.UnknownHashError("hash could not be identified")
E           passlib.exc.UnknownHashError: hash could not be identified
FAILED tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format
1 failed

control valid hash, right pw  -> True
control valid hash, wrong pw  -> False
malformed hash                -> raised passlib.exc.UnknownHashError: hash could not be identified
shape ''           -> raised UnknownHashError: hash could not be identified
shape '$2b$12$abc' -> raised ValueError: salt too small (bcrypt requires exactly 22 chars)
```

As committed the test reports 1 xfailed. The valid-hash controls behave normally, so the failure is specific to a stored hash passlib cannot identify.

## Diagnosis

verify_password() in core/security.py is a single line, return bool(pwd_context.verify(plain_password, hashed_password)) (line 37), with nothing around the call. passlib's CryptContext.verify raises UnknownHashError when the stored string matches none of the configured schemes (here only bcrypt). The repro shows exactly this: the traceback ends in passlib's identify_record with UnknownHashError, and the valid-hash controls return True and False. So the break is at the call itself, in verify_password(): the function documents "True if password matches, False otherwise" but lets passlib's exception through for an unrecognizable stored hash. I have not shown that anything upstream (hashing, storage) produces such hashes.

## Scope

In: make verify_password() return False when passlib raises UnknownHashError for the stored hash, and remove the xfail marker from test_verify_with_wrong_hash_format, which the issue and docs/CONTRIBUTING.md both ask for when fixing a seeded bug.

Not in:
- the truncated-$2b$ case ('$2b$12$abc'), which raises a plain ValueError from bcrypt, not UnknownHashError. The issue names UnknownHashError; I will report this shape to the maintainers instead of widening the change.
- any change to api/routes/auth.py, logging, or other functions in core/security.py.
- refactors, renames, new options, or dependency changes.

## Files

- core/security.py (the verify_password() function, plus the import of UnknownHashError)
- tests/unit/test_security.py (delete the @pytest.mark.xfail(...) decorator on test_verify_with_wrong_hash_format)

No file named only for review: api/routes/auth.py is read-only context for the risk below, and will not change.

## Approach

1. In core/security.py import UnknownHashError from passlib.exc.
2. Wrap the call: try: return bool(pwd_context.verify(...)) and except UnknownHashError: return False. Catch only that exception type, so other errors still surface.
3. Update the docstring to say an unrecognizable stored hash returns False.
4. Delete the xfail decorator (all four lines) on test_verify_with_wrong_hash_format.

## Test plan

Commands run from the repo root with the project venv; expected output written down before the change.

| Command | Today (before the fix) | Expected after the fix |
|---|---|---|
| `pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format --runxfail` | `1 failed`, `passlib.exc.UnknownHashError: hash could not be identified` | `1 passed` |
| `pytest tests/unit/test_security.py` | `24 passed, 1 xfailed` | `25 passed` (no xfail, no xpass) |
| the control script from my repro comment: `verify_password("password", "not_a_valid_bcrypt_hash")` | `raised passlib.exc.UnknownHashError` | `False` |
| same script, valid hash controls | `True`, then `False` | unchanged: `True`, then `False` |
| same script, shape `''` | `raised UnknownHashError` | `False` |
| same script, shape `'$2b$12$abc'` | `raised ValueError: salt too small` | unchanged (deferred, see Scope) |

Also make lint, make format, make typecheck and make test-unit, as docs/CONTRIBUTING.md asks.

## Risks and unknowns

- api/routes/auth.py:80 calls verify_password() in the login route. I expect a malformed stored hash to then lead to the route's existing 401 branch instead of an unhandled exception, but I have not run the login route; I only read it. I will say that in the PR rather than claim it.
- Returning False hides a corrupt hash from the caller. The issue explicitly asks for fail-closed behavior, so I am not adding logging in this change.
- My repro ran on Python 3.14.4; SETUP.md and CI target 3.11, which I have not run. CI will cover that.
- Other classmates have posted plans on this issue; I am working from my own reproduction.

## Deviations

The change itself matched the plan: the two files named in Files, nothing else. core/security.py got the UnknownHashError import, the try/except UnknownHashError: return False, and the docstring line; tests/unit/test_security.py lost the four-line xfail decorator. api/routes/auth.py was not touched, and I did not widen the catch to the '$2b$12$abc' ValueError case.

Two differences in how I checked it, neither changing the diff:

- make is not available in my Windows shell, so instead of make lint, make format, make typecheck and make test-unit I ran what they run: ruff check and black --check on the two changed files, mypy core/security.py, and pytest tests/unit on the whole unit folder. Results: ruff and black clean, mypy "no issues found", 376 passed, 52 xfailed (the other xfails are other seeded bugs, no XPASS). I did not run the integration tests or the frontend job; CI will.
- The test plan only listed the single test and the one file. I also ran all of tests/unit as above, to check nothing else regressed.

Results matched the table in the Test plan exactly: 1 failed became 1 passed, 24 passed, 1 xfailed became 25 passed, the malformed hash and '' now return False, the valid-hash controls are unchanged, and '$2b$12$abc' still raises ValueError (deferred, as posted). I still have not run the login route, so the PR will say only what I read in auth.py:80.
