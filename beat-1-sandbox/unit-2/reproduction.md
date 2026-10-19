# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

AbdulazizArabov

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-6258222453

````markdown
I'd like to take #72: `verify_password()` lets passlib's `UnknownHashError` escape for a malformed stored hash instead of returning `False`. I can see several classmates have commented here; I'll do my own setup and post my own report rather than building on theirs.

What I've read so far: `verify_password()` in `core/security.py` is `return bool(pwd_context.verify(plain_password, hashed_password))` (line 37), and the covering test, `test_verify_with_wrong_hash_format` in `tests/unit/test_security.py`, is marked `xfail(strict=True)` with the reason "issue #72 (manifest H-05)".

Next I'll clone my fork of `main`, set up following `docs/SETUP.md`, run that test with `--runxfail`, and post a separate reproduction report here with my environment, the exact commands, and the raw output, whatever the result is. This comment is only about reproducing; I'm not promising a fix or a date.
````

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-6258429807

````markdown
Reproduction report for #72. **Result: reproduced** on current `main`. `verify_password()` raises `passlib.exc.UnknownHashError` for the test's malformed stored hash instead of returning `False`.

**Environment**

- Windows 11 (10.0.26200.9711), x64, run in Git Bash
- Python 3.14.4 (note: SETUP.md and CI target 3.11; I did not test 3.11)
- passlib 1.7.4, bcrypt 4.3.0, pytest 9.1.1, python-jose 3.5.0
- Code: `codepath/pathreview-ai301-fa26-s3` at commit `2f4e82f52efbcfcc57d65b3fa5348672163ca088` (current `main`), fresh clone, no local changes

**Steps** (from `docs/SETUP.md`; I skipped Docker, the database, and the frontend because this test does not touch them)

```
git clone https://github.com/codepath/pathreview-ai301-fa26-s3.git pathreview
cd pathreview
python3 -m venv .venv
.venv/Scripts/python.exe -m pip install -e ".[dev]"
.venv/Scripts/python.exe -m pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format --runxfail
```

**Observed.** As committed, the test reports `1 xfailed`. With `--runxfail` it fails inside passlib's `identify_record`:

```
>           raise exc.UnknownHashError("hash could not be identified")
E           passlib.exc.UnknownHashError: hash could not be identified

.venv\Lib\site-packages\passlib\context.py:1132: UnknownHashError
FAILED tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format
1 failed
```

Calling the function directly from the repo root (`.venv/Scripts/python.exe -W ignore script.py`), with a valid hash as a control:

```python
from core.security import hash_password, verify_password
good = hash_password("password")
print("control valid hash, right pw  ->", verify_password("password", good))
print("control valid hash, wrong pw  ->", verify_password("wrong", good))
try:
    print("malformed hash                ->", verify_password("password", "not_a_valid_bcrypt_hash"))
except Exception as e:
    print("malformed hash                -> raised", type(e).__module__ + "." + type(e).__name__ + ":", e)
```

```
control valid hash, right pw  -> True
control valid hash, wrong pw  -> False
malformed hash                -> raised passlib.exc.UnknownHashError: hash could not be identified
```

(passlib 1.7.4 also prints a "(trapped) error reading bcrypt version" traceback once, when the bcrypt backend first loads with bcrypt 4.3.0; it is trapped and the control calls still work.)

**Expected:** `verify_password("password", "not_a_valid_bcrypt_hash")` returns `False`, as the issue and the test's assertion (`result is False`) say.

**Actual:** it raises `UnknownHashError`, as shown above. The valid-hash controls return `True` and `False` normally, so the failure is specific to the malformed stored hash.

Two more shapes I tried with the same call, because one differs:

```
shape ''           -> raised UnknownHashError: hash could not be identified
shape '$2b$12$abc' -> raised ValueError: salt too small (bcrypt requires exactly 22 chars)
```

So a truncated `$2b$` hash raises a plain `ValueError` rather than `UnknownHashError`. I only checked these three inputs; I did not look at callers or the login endpoint.
````

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. First full invocation: crashed before grading anything, with no score
   ("FileNotFoundError: [WinError 2] The system cannot find the file specified"). On Windows
   `claude` is an npm `claude.cmd` shim that Python's `subprocess` cannot launch by bare name.
   I put the real `claude.exe` folder on PATH for the run; the harness itself is unchanged.
2. Smoke run (`--limit 1`): "agreement: 1/1 scored items"
3. First full run: "agreement: 15/17 scored items" ("3 item(s) errored; fix and re-run."). The
   two real disagreements were pkg-03 (failed: conclusion-within-evidence) and pkg-05 (failed:
   steps-rerunnable). The three errors were pkg-04, pkg-07 and pkg-11.
4. Revised those two checks, then `--only` on the 2 disagreements, the 3 errored packages and
   7 canaries (pkg-13, 14, 15, 17, 18, 06, 20): "agreement: 9/9 scored items". The same three
   packages errored again ("no stdin data received in 3s"), so it was not load.
5. Found the cause: pkg-04, pkg-07 and pkg-11 are exactly the packages containing emoji, and
   Python on Windows encodes stdin as cp1252. With `PYTHONUTF8=1`, `--only pkg-04,pkg-07,pkg-11`:
   "agreement: 3/3 scored items"
6. Final full run (committed): "agreement: 20/20 scored items  (bar: 18/20: PASS)"

**Package analysis**

**pkg-05** (conda/conda#16543). Gold label: accept ("minimal env.yml repro with a json.tool
parse failure as the artifact"). My rubric's final decision, in the committed run: accept. My
first run decided reject, which disagreed with gold, and that is the useful part.

In the first run the grader failed `steps-rerunnable` with this evidence: "The env.yml is
described only in prose ("a minimal env.yml containing a valid dependencies: list plus a
category: section"); its contents are not shown and the issue's conda-lock URL is not
linked." My original pass condition required every input to be "written out in the report or
publicly obtainable" and failed anything "described only in prose", so the grader applied it
literally. That reading was defensible but wrong against the gold label: the prose names the
exact element that triggers the bug (the unrecognized `category:` section), a stranger can
recreate the file in one step, and the artifact (`json.tool` failing with "Expecting value:
line 1 column 1 (char 1)") shows the issue's symptom. The failure I wanted `steps-rerunnable`
to catch is pkg-18, whose input is a private monorepo nobody can recreate. After the revision
the committed run graded: "Minimal env.yml described with valid `dependencies:` list plus
`category:` section; exact command written out", and pkg-05 accepted.

**Check rationale**

`steps-rerunnable`, as the row reads now in `tools/repro-check/rubric.md`:

| steps-rerunnable | The report's steps and commands, read as a stranger starting from a clean machine | Every input the steps depend on (commands, files, config, project, link) is either written out in the report or publicly obtainable from the issue or repo. Fails if any step depends on something private, unshared, or too vague to recreate ("our internal config", "set up the project", "checked out our monorepo", "a large file"). An input described in prose passes when the description names the exact elements that trigger the issue, so a stranger could recreate it in one step (for example "a minimal env.yml with a valid `dependencies:` list plus a `category:` section"). | required |

Why it reads that way: my first version ended at "...or described only in prose", which made
the grader reject pkg-05 (see Package analysis). I did not delete the prose clause, because
the thing the check exists to catch is an input a stranger cannot get, as in pkg-18
(private monorepo, unshared config). Instead I changed the test from "is it written out?" to
"could a stranger recreate it?", changed "described only in prose" to "too vague to recreate",
and put the carve-out inside this check with the exact pkg-05 wording as its example. I
rejected adding a general exception at the bottom of the rubric, because a carve-out that
lives outside the check it modifies is the kind of thing a grader reads inconsistently.

**Trade-offs**

Loosening `steps-rerunnable` (and the matching carve-out in `conclusion-within-evidence`, for
pkg-03's unpasted control run) could flip a rejected package to accept, so before the
confirming run I re-ran canaries with `--only`: pkg-18 and pkg-06 (unfollowable-comms) for the
steps change; pkg-13, pkg-14, pkg-15 and pkg-17 (no-evidence and wrong-target) for the
conclusion change; and pkg-20, the one-package `disclosure` category. All seven stayed reject,
matching gold ("agreement: 9/9 scored items" with the two fixed packages), and the committed
full run then agreed on all 20 with every category matched.

What this check gives up: a report whose prose description sounds precise but would not
actually trigger the bug (for example "a file with a bad section" that names the right section
name but leaves out a required key). The check judges whether the description names the
triggering element, not whether the recreated file really reproduces. I accept that miss:
catching it means executing the report, and the grader only reads text, so a missing recipe
shows up in the artifact check instead (the output would not match the issue's symptom).

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
