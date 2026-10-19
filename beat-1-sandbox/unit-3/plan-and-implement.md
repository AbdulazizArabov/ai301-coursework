# Unit 3 — Plan and Build

Path: beat-1-sandbox/unit-3/plan-and-implement.md

Record of your plan, the branch you built it on, and the evaluation runs that produced
eval-run.txt. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

AbdulazizArabov

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-6258792263

````markdown
Plan for #72, built from my own reproduction above (Windows 11, Python 3.14.4, passlib 1.7.4, `main` at `2f4e82f`).

**What I found.** `verify_password()` in `core/security.py` is one line, `return bool(pwd_context.verify(...))`, with nothing around the call. For a stored hash passlib can't identify, `pwd_context.verify` raises `UnknownHashError`, which is the traceback in my repro. The valid-hash controls return `True`/`False` normally, so the break is at that call.

**What I'll do.** The issue asks for fail-closed behavior and says to remove the `xfail` marker as part of the fix, and `docs/CONTRIBUTING.md` says the same, so I'll keep it to exactly that: catch `UnknownHashError` only in `verify_password()` and return `False`, update the docstring, and delete the `xfail` decorator on `test_verify_with_wrong_hash_format`. Files: `core/security.py` and `tests/unit/test_security.py`. Not touching `api/routes/auth.py`, logging, or other functions.

One thing I found and am deliberately leaving out: a truncated `$2b$` hash (`'$2b$12$abc'`) raises a plain `ValueError` ("salt too small") rather than `UnknownHashError`. Maintainers, if you want that covered too, say so and I can look at it separately.

**How I'll prove it.** Same single-test command as my repro, plus the whole security test file, which I ran on `main` for this plan. Today: the test with `--runxfail` gives `1 failed` with `UnknownHashError`, and `pytest tests/unit/test_security.py` gives `24 passed, 1 xfailed`. After the fix I expect `1 passed` and `25 passed`, and the direct call with `"not_a_valid_bcrypt_hash"` returning `False` while the valid-hash controls stay `True`/`False`. I haven't run the login route, so I'll only say in the PR what I read there, not what I verified.

I'll work on a branch in my fork, `fix/72-verify-password-unknown-hash`, and open a PR after this.
````

---

## Your branch

**Branch**

fix/72-verify-password-unknown-hash

(pushed to my fork, AbdulazizArabov/Unit2_pathreview-ai301-fa26-s3; issue #72 is the issue I claimed)

**Evidence**

Environment for every run below: Windows 11 (10.0.26200.9711), Python 3.14.4, passlib 1.7.4, bcrypt 4.3.0, pytest 9.1.1, repo root of my fork's clone. The before runs are on main at 2f4e82f; the after runs are on branch fix/72-verify-password-unknown-hash (commit 632f186).

Before the fix:

```
$ pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format --runxfail
E           passlib.exc.UnknownHashError: hash could not be identified
FAILED tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format
1 failed, 1 warning in 0.91s

$ pytest tests/unit/test_security.py
24 passed, 1 xfailed, 1 warning in 10.59s

$ python -W ignore script.py    (the control script from my repro comment)
control valid hash, right pw  -> True
control valid hash, wrong pw  -> False
malformed hash                -> raised passlib.exc.UnknownHashError: hash could not be identified
shape ''           -> raised UnknownHashError: hash could not be identified
shape '$2b$12$abc' -> raised ValueError: salt too small (bcrypt requires exactly 22 chars)
```

After the fix:

```
$ pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format --runxfail
1 passed, 1 warning in 0.62s

$ pytest tests/unit/test_security.py
25 passed, 1 warning in 7.90s

$ python -W ignore script.py    (same script)
control valid hash, right pw  -> True
control valid hash, wrong pw  -> False
malformed hash                -> False
shape ''             -> False
shape '$2b$12$abc'   -> raised ValueError: salt too small (bcrypt requires exactly 22 chars)

$ pytest tests/unit      (what make test-unit runs)
376 passed, 52 xfailed, 1 warning in 16.49s
```

Also clean after the fix: ruff check core/security.py tests/unit/test_security.py ("All checks passed!"), black --check on the same two files ("2 files would be left unchanged"), and mypy core/security.py ("Success: no issues found in 1 source file"). The '$2b$12$abc' case still raising ValueError is the deferred case from my plan comment, not a miss.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Smoke run (--limit 1): "agreement: 1/1 scored items"
2. First full run: "agreement: 18/20 scored items  (bar: 18/20: PASS)". The two disagreements were
   pkg-02 (failed: comment-matches-plan) and pkg-09 (failed: files-match-scope, ai-disclosure-met,
   comment-conveys-plan); both are clear-accepts in the gold labels.
3. Loosened those checks, then --only pkg-02,pkg-09,pkg-20,pkg-04,pkg-12,pkg-19,pkg-15 (the two
   fixed packages plus five canaries): "agreement: 7/7 scored items"
4. Final full run (committed, --save-run eval-run.txt): "agreement: 20/20 scored items  (bar: 18/20: PASS)",
   with "categories: clear-accept 7/7  scope-creep 4/4  thread-convention 2/2  unbuildable 3/3  wrong-cause 4/4"

**Package analysis**

pkg-09 (sharkdp/fd#2067). Gold label: accept ("honestly scoped-down: option 2 normalization gated
to Windows, defers the direct-globset rework with reasons, decisive three-spelling fixture test;
arguable on the deferral, ready as scoped"). My rubric's decision in the committed run: accept. My first
run decided reject, which disagreed with gold.

In the first run the grader failed two required checks. files-match-scope: "Files: src/main.rs (no
change expected to build_pattern_regex; noted for review)' - named file serves no part of the in-scope
change". ai-disclosure-met: "Policy: 'comments to maintainers are expected to be in the contributor's
own words'; comment contains no sentence disclosing AI assistance". Both were my rubric's fault, not the
grader's. The plan lists src/main.rs explicitly as "no change expected", so it is not a file the plan
will change; my pass condition said "every named file", which counted it. And the policy line says
disclosure is stated for pull requests and "the policy states no disclosure ask for issue comments", so an
own-words rule is not a disclosure requirement; my pass condition lumped the two together, which also
contradicted the rubric I wrote in unit 2. After narrowing both, pkg-09 accepted: the plan fixes one
thing at the match site, names the deferral of option 1 with a reason, and its test plan states the
output for each of the three pattern spellings.

**Check rationale**

files-match-scope, as the row reads now in tools/plan-check/rubric.md:

| files-match-scope | The files or areas the plan says it will touch, read against its own in-scope statement | Every file or area the plan says it will change is needed for the stated change, and the plan names no file just because it was seen. Fails if a file the plan says it will change serves no part of the in-scope change. A file the plan lists only as "no change expected" or "noted for review" is not a file it will change, and does not fail this check. | required |

Why it reads that way: my first version said "Every named file or area is needed for the stated
change... Fails if a named file serves no part of the in-scope change", which failed pkg-09 for
listing src/main.rs as "no change expected" (see Package analysis). I did not delete the check,
because the thing it exists to catch is scope creep by file (pkg-19, where a one-line fix drags in a
state-machine rewrite and a test-harness migration). I changed the test from "is the file named?" to
"does the plan say it will change it?", and put the carve-out inside the check, with the exact wording
the plan used as the example. I rejected a general exception at the bottom of the rubric, because a
carve-out outside the check it modifies is the kind a grader reads inconsistently.

**Trade-offs**

Narrowing files-match-scope (and the matching changes to comment-matches-plan and
ai-disclosure-met) could flip a rejected package to accept, so before the confirming run I re-ran
canaries with --only: pkg-19 and pkg-12 and pkg-15 (scope-creep, for the file and comment changes),
pkg-04 (thread-convention, comment never engages the owner's direction), and pkg-20 (the strict-AI-policy
thread-convention package, for the disclosure change). All five stayed reject, matching gold
("agreement: 7/7 scored items" with the two fixed packages), and the committed full run then agreed on
all 20 with every category matched.

What this check gives up: a plan that writes "no change expected" for a file it then actually edits
would pass files-match-scope. The check reads what the plan says, not what the diff later does. I
accept that miss: catching it needs the diff, which the grader does not see in this unit, and the
plan's ## Deviations section plus the unit 4 pull-request check are where a mismatch between plan and
diff shows up.

---

Related paths: plan.md and eval-run.txt in this directory; your skill's files in
tools/plan-check/.
