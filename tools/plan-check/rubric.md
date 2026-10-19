# Rubric: is this plan ready to post and build from?

## Checks

One check asks one question. Checks 1-2 read the diagnosis, 3-5 read the
scope, 6-7 read whether a stranger could start, 8-9 read the test plan,
10 reads the plan's honesty, and 11-14 read the plan comment against the
plan, the thread, and the repo's rules.

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-grounded | The plan's stated cause, read against every observation in the repro evidence block (the steps, the actual output, and any control run or ruled-out variant) | The stated cause is consistent with all of the repro evidence and explains the failing behavior it shows. Fails if any observation in the repro evidence contradicts the cause (for example a control run that still fails with the blamed component removed or unused), or if the cause is a guess the repro evidence neither supports nor tests. A cause taken from the thread passes only if the repro evidence supports it. | required |
| fix-at-cause | The plan's named change site (file, function, or stage), read against the stage where the stated cause says the fault happens | The change lands at the stage that produces the fault. Fails if the change only hides, catches, or reformats the symptom downstream of the cause (for example clamping a displayed value when the stated cause is a wrong calculation upstream). A deliberate workaround passes only if the plan says it is a workaround and says why the cause is not fixed. | required |
| scope-one-change | The plan's in-scope statement and approach, read against the issue's title and body | The plan describes one change that resolves what the issue reports. Fails if the plan adds a second purpose the issue did not ask for: a refactor, rename, migration, redesign, new option, dependency change, or "while I'm here" cleanup. | required |
| scope-covers-issue | The plan's in-scope and not-in-scope statements, read against what the issue asks for | Every part of the issue is either in the plan's scope or named as deliberately deferred, with the reason. A plan that fixes part of the issue and says so passes. Fails if part of the issue is dropped without being named. | required |
| files-match-scope | The files or areas the plan says it will touch, read against its own in-scope statement | Every file or area the plan says it will change is needed for the stated change, and the plan names no file just because it was seen. Fails if a file the plan says it will change serves no part of the in-scope change. A file the plan lists only as "no change expected" or "noted for review" is not a file it will change, and does not fail this check. | required |
| files-named | The plan's list of files, functions, or areas to change | The plan names at least one specific file, function, or area where the work starts. Fails if it says only "the relevant code", "the backend", or "poke around". | required |
| approach-concrete | The plan's approach, read as a stranger who has never seen the repo | The approach states the change itself (what will be added, removed, or computed differently) so another developer could make it without asking the author. Fails if it only states a direction to investigate or a goal ("make it robust", "look into the parser"). | required |
| test-observable | The plan's test plan | The test plan names a command or action to run and an observable result that shows the issue's behavior is fixed (an output, exit status, value, or test result). Fails if the only check is "run the test suite", "see if it works", or "make sure nothing regresses" with no result tied to the issue's behavior. | required |
| test-reruns-repro | The plan's test plan, read against the repro evidence's steps and actual output | The test plan re-runs the repro evidence's steps, or a check that goes through the same code path, and states what the output must change to. Fails if the test plan checks a different scenario than the repro reproduced. | required |
| confidence-matches-evidence | The plan's stated risks, unknowns, and any claim that something is verified or certain, read against the repro evidence | Anything the repro evidence did not show is stated as an assumption or unknown, not as fact. Fails if the plan asserts as certain something the evidence never tested (for example "this affects no other caller", "root cause confirmed" with only a guess behind it). | required |
| comment-matches-plan | The plan comment, read against the plan | The comment promises no more than the plan contains. Fails if the comment promises an outcome or guarantee the plan does not contain (a fix that covers more than the plan's scope, "will definitely work"), gives a deadline, or asks the maintainers to assign or reserve the issue. Saying the author will open a pull request for the planned change, report back, mention the issue in the pull request, or "take" the issue as a statement of intent all pass. | required |
| comment-follows-thread | The plan comment, read against the thread highlights (and, live, the full thread) | Where a maintainer gave explicit direction in the thread (a constraint, a request, a decision, a "do not"), the comment follows it or says why it does not. Passes when the thread holds no maintainer direction that bears on the plan. Fails if the comment or the plan contradicts or ignores such direction. | required |
| comment-follows-conventions | The plan comment, read against the repo-facts block's stated asks (bug-report template fields, contribution asks), apart from AI-use rules | Where the repo states a contribution ask that applies to a plan comment or the change, the comment honors it. Passes when the repo states no such ask. Fails if the comment or plan skips an ask the repo states plainly. | required |
| ai-disclosure-met | The repo-facts contribution policy line, read against the text of the plan comment. Treat these packages as AI-assisted work. | Passes if the policy has no disclosure requirement covering comments (silence, a permissive policy, an own-words rule, or a disclosure rule that applies only to pull requests all pass). If the policy requires disclosing AI use in comments or issues, passes only if the comment contains a plain sentence disclosing AI assistance (naming the tool and the extent when the policy asks for them). Fails if disclosure is required and the comment contains none. | required |
| comment-conveys-plan | The plan comment read alone, as a maintainer would read it | A maintainer reading only the comment can say what the cause is, what will change, and how it will be shown to work. | preferred |

## Verdict rule

Accept only if every required check passes. `unclear` counts as `fail` for
every required check. `comment-conveys-plan` (preferred) never changes the
verdict. A plan that is terse but passes every required check is ready: a
plan is judged on what it says, not on how long it is. A plan that defers
part of the issue and says so passes `scope-covers-issue`.

## Design note: why the checks are this small

Each failure family maps to named checks, so a `fail` says which part is
missing and nothing has to be inferred from a long cell:

- **Cause:** `diagnosis-grounded` asks whether the cause survives the
  evidence; `fix-at-cause` asks whether the change lands where the cause
  says the fault is. A polished plan can adopt a confident cause that the
  package's own control run rules out, so the first check reads the
  evidence, never the confidence.
- **Scope:** `scope-one-change` (nothing extra), `scope-covers-issue`
  (nothing silently dropped), and `files-match-scope` (no file just
  because it was seen) are three questions, not one.
- **A stranger could start:** `files-named` and `approach-concrete`.
- **Proof:** `test-observable` asks for a result tied to the issue;
  `test-reruns-repro` asks that it is the repro's scenario.
- **Honesty:** `confidence-matches-evidence`.
- **Comms:** the comment is checked against the plan
  (`comment-matches-plan`), the thread (`comment-follows-thread`), the repo's
  stated asks (`comment-follows-conventions`), and the repo's AI-use policy
  (`ai-disclosure-met`), because a plan can be sound on every check above
  and still be unpostable on this thread or under this repo's rules.

Rules for adding a check here:

- One question per check. A pass condition may list several acceptable
  forms of the same answer, but if it joins two different questions with
  "or" or "and", split it.
- Name the failing case, not just the passing one.
- Judge the thing itself (does the plan's cause survive the evidence?),
  never the write-up's shape (length, headings, number of steps).
- Write carve-outs ("a deferral that is stated passes", "silence passes")
  into the check they belong to.
