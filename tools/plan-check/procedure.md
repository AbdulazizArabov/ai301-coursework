# Procedure: how this skill grades a plan package

These steps are for GRADING a plan, not for making one. Follow them in
order. Where a step says "the package", in eval mode it means the bundle
text and nothing else; in live mode it means the student's `plan.md`, the
draft plan comment, the issue thread, and the student's posted repro
comment on that issue.

## Read order

1. Read the Issue section first (title and body). Write down one line:
   what behavior the issue says is wrong, and what it asks to be true
   instead. Every scope check later reads against this line.
2. Read the Thread highlights next. Copy out every sentence in which a
   maintainer (owner, member, or collaborator) gives a direction: a
   constraint, a decision, a request, a "do not", or a statement of how
   the project wants it done. Write "no maintainer direction" if there
   is none. Classmates' or outsiders' comments are not direction.
3. Read the Repo facts block. Copy out (a) the contribution asks and
   bug-report template asks, and (b) the contribution policy line,
   including any AI-use rule. Note whether the policy requires AI
   disclosure in comments, requires comments in the author's own words,
   applies only to pull requests, or is silent.
4. Read the Repro evidence block before the plan. Write down: the exact
   steps, the actual output, every control run or ruled-out variant, and
   what each of those observations rules in or out. This is the baseline
   the diagnosis and the test plan are graded against, so it must be read
   before the plan can influence it.
5. Read the Candidate plan. Copy out, each on its own line: the stated
   cause, the change site (file, function, or stage), the in-scope
   statement, the not-in-scope statement (or "none"), the files named, the
   approach, the test plan, and the risks or unknowns (or "none").
6. Read the Candidate plan comment last, once, as a maintainer would.
   Copy out every promise it makes (what it says will be done, delivered,
   or guaranteed) and every sentence about AI use.

## Evidence gathering

1. For `diagnosis-grounded`: take the stated cause from step 5 and list
   each observation from step 4. For each observation write "supports",
   "contradicts", or "does not bear on" the cause. A control run that
   still fails after the blamed part is removed or unused is
   "contradicts".
2. For `fix-at-cause`: take the change site and the stage where the cause
   says the fault arises, and write whether the change site is that stage
   or is later in the flow (a display, a catch, a clamp, a format step).
3. For the scope checks: take the issue line from step 1. Write whether
   the plan's change resolves it, list any second purpose in the plan
   (refactor, rename, migration, redesign, new option, dependency,
   cleanup), list every part of the issue the plan does not cover and
   whether the plan names it as deferred, and list each file the plan says
   it will change with the part of the in-scope change that needs it. A
   file listed only as "no change expected" or "noted for review" goes on
   a separate line and is not counted as a file to change.
4. For `files-named` and `approach-concrete`: copy the files line and the
   approach lines. Write whether you, who have never seen the repo, could
   make the change from the approach alone.
5. For the test checks: copy the test plan. Write the command or action,
   the result it says to expect, whether that result is tied to the issue's
   behavior, and whether the steps are the repro evidence's steps (or go
   through the same code path).
6. For `confidence-matches-evidence`: list each sentence in the plan that
   states something as certain or verified, and for each write whether a
   repro observation shows it.
7. For the comment checks: lay the promises from step 6 beside the plan
   and write which ones the plan does not contain; lay the maintainer
   directions from step 2 beside the comment and the plan and write
   "follows", "addresses", or "ignores/contradicts" for each; lay the
   repo asks from step 3 beside the comment and plan; and lay the policy
   from step 3 beside the AI sentence from step 6.
8. If a piece of evidence a step asks for is not in the package, write
   "absent" for it. Do not fetch or invent it. In eval mode never fetch
   anything.

## Check execution

1. Run the checks in the order they appear in `rubric.md`.
2. Grade each check using only the lines written down in Evidence
   gathering for that check, plus a re-read of the one package part the
   check's Evidence column names. You do not re-read the whole package
   for each check.
3. Apply the check's pass condition literally. Where the pass condition
   names a failing case, a package in that case fails even if the plan is
   well written. Where it names a carve-out (a stated deferral, silence in
   the policy, an honest workaround), a package in that case passes.
4. If the evidence a check needs is "absent", grade the check `fail` when
   the absence is the plan's omission (for example no test plan), and
   `unclear` when the absence is something the package should have
   supplied and did not (for example no thread to read). Do not grade a
   check `pass` on evidence you did not see.
5. For every grade write one line of evidence: a short quote from the
   package that decided it, with the section it came from.
6. Do not let a check's grade depend on another check's grade. A plan that
   fails `diagnosis-grounded` can still pass `scope-one-change`.

## Verdict assembly

1. List the grades of the required checks. Apply the verdict rule in
   `rubric.md`: `accept` only if every required check is `pass`; any
   `fail` or `unclear` among them makes the verdict `reject`.
2. `comment-conveys-plan` is preferred: record its grade but never let it
   change the verdict.
3. If the verdict is `reject`, name the failing check or checks, and quote
   from the package the line that decided each one. If several checks
   failed, name the one earliest in the rubric first.
4. If the verdict is `accept`, say in one line that every required check
   passed, and quote the plan's test-plan line.
5. In live mode, after the per-check summary, report any voice-guide rule
   the draft comment breaks (quoting the rule), and any step of this
   procedure that was silent or unclear for this package.
6. End with the JSON block from `SKILL.md`, listing every check in
   rubric order with its grade and one line of evidence, then the verdict.
   Put nothing after the JSON block.
