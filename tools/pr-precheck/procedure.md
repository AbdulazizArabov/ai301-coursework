# Procedure: how this tool grades a PR package

These steps are for GRADING a pull request, not for making one. Follow
them in order. "The package" means, in eval mode, the bundle text and
nothing else; in live mode, the files and commands named in `SKILL.md`
(`plan.md`, `git diff main...HEAD`, `pr_draft.md`, `test_evidence.md`, the
issue thread, the PR template, and `docs/CONTRIBUTING.md`).

## Read order

1. Read the Issue (title and body) first. Write one line: the behavior the
   issue says is wrong and what it asks for instead. The plan and the PR are
   both graded against this line.
2. Read the Thread highlights (live: the issue thread). Copy out every
   sentence in which a maintainer (owner, member, or collaborator) gives
   direction: a constraint, a decision, a request, or a "do not". Write "no
   maintainer direction" if there is none. Classmates' and outsiders'
   comments are not direction.
3. Read the Repo facts block (live: the PR template, `docs/CONTRIBUTING.md`,
   and any AI policy file). Copy out: every PR template section; every
   check or command the repo says to run before a PR; the runtime and
   version the repo declares for development and CI (live: the setup docs,
   the CI configuration, and the project metadata); every other stated ask
   (title format, issue link, size); and the AI-use policy line, noting
   whether it requires disclosure in pull requests, applies only to issue
   comments, or is silent.
4. Read the Plan context (live: `plan.md`) before the PR. Copy out, each on
   its own line: the in-scope files and the not-in-scope line, each approach
   step, each scenario in the test plan, and every deviation note (or "no
   deviation notes"). Read the plan before the diff so that the diff is
   measured against what was promised, never the other way round.
5. Read the Diff (live: `git diff main...HEAD`, plus
   `git diff main...HEAD --stat`). Before reading any hunk closely, list
   every changed file with a one-line summary of what changed in it. Then
   read each hunk and note any added line that is a debug print, commented
   out code, dead code, a leftover TODO, or a change that only reformats.
6. Read the commit list. Note each commit subject.
7. Read the PR title and description last (live: `pr_draft.md`). Copy out
   every claim about what changed, every statement about the plan ("no
   changes beyond the plan", "implements the plan"), every ticked box, the
   issue reference, and every sentence about AI use. Read the description
   last so it cannot color how the diff is read.
8. Read the Test evidence (live: `test_evidence.md`). Copy out each
   command, its output, and the before and after of the behavior.

## Evidence gathering

1. For `diff-within-plan`: lay the changed-file list from Read order step 5
   beside the plan's in-scope files and not-in-scope line (step 4). For each
   changed file and hunk write "inside plan", "inside deviation note", or
   "outside plan". A file named in the plan but with a hunk the plan's
   approach does not describe is "outside plan" for that hunk.
2. For `diff-delivers-plan`: for each approach step in the plan, write the
   hunk in the diff that carries it out, or "missing". For each "missing",
   write whether the description or a deviation note says it was left out.
3. For `description-matches-diff`: for each claim copied from the
   description (step 7), write "true of the diff", "not in the diff", or
   "contradicted by the diff". A claim of fidelity ("no changes beyond the
   plan") is tested against the "outside plan" lines from step 1 above.
4. For `deviations-recorded`: list each difference between the diff and the
   plan's approach (from steps 1 and 2 above). For each, write whether the
   deviation notes or the description's notes record it.
5. For the test checks: copy each scenario in the plan's test plan and write
   the command and output in the evidence that covers it, the sentence in the
   evidence that says it was run and what came out, or "silent".
   Write whether the evidence shows the issue's behavior before and after as
   readable output. Write whether the evidence's commands run through the
   functions or files the diff changes. Write, for each repo check copied in
   Read order step 3, the command and result in the evidence, or "not
   present". Write the runtime and version the evidence says it ran on, and
   set it beside the declared runtime and version from Read order step 3:
   "same", "different and named (with the reason)", "different and not
   named", or "no declared environment".
6. For `no-debris` and `no-churn-or-unrelated-hunks`: copy each added line
   noted in Read order step 5 as debris, and each hunk that only reformats or
   is unrelated to the issue. Write "none" if there are none.
7. For `template-filled`: for each template section from step 3, write the
   description's content under it, or "empty", "placeholder", or "missing".
   For each ticked box, decide what it asserts, then write one of:
   "supported" (with the evidence line), "contradicted", "output not shown"
   (the box asserts the output of a command and the evidence lacks it), or
   "attestation, not contradicted" (the box attests to a property of the
   author's own work and nothing in the package contradicts it).
8. For `ai-disclosure-met`: lay the policy line from step 3 beside the
   description's AI sentence from step 7.
9. For `issue-referenced`: copy the issue number the description names and
   compare it with the issue number of the plan.
10. For `thread-direction-followed`: lay each maintainer direction from Read
    order step 2 beside the description and the diff and write "followed",
    "addressed", or "ignored or contradicted".
11. If evidence a step asks for is not in the package, write "absent". In
    eval mode never fetch anything.

## Check execution

1. Run the checks in the order they appear in `rubric.md`.
2. Grade each check using only the lines written in Evidence gathering for
   it, plus a re-read of the one package part the check's Evidence column
   names. Do not re-read the whole package for each check.
3. Apply the pass condition literally. Where it names a failing case, a
   package in that case fails even if it is well written. Where it names a
   carve-out (a stated deferral, silence in the policy, a stated check that
   cannot run), a package in that case passes.
4. If the evidence a check needs is "absent", grade `fail` when the absence
   is the pull request's omission (for example no test evidence section),
   and `unclear` when the package should have supplied it and did not (for
   example no thread to read). Never grade `pass` on evidence you did not
   see.
5. Write one line of evidence per grade: a short quote from the package
   with the part it came from.
6. Do not let one check's grade decide another's. A package that fails
   `diff-within-plan` can still pass `test-observable-result`.

## Verdict assembly

1. List the grade of every check. Apply the verdict rule exactly as it is
   written in `rubric.md`; this file does not restate or change it, and
   `rubric.md` is the only place the rule is defined.
2. Record the grade of every preferred check; how a preferred check enters
   the verdict is decided by the rule in `rubric.md`, not here.
3. If the verdict is `reject`, name the first failing required check in
   rubric order and quote from the package the line that decided it; name
   any other failing checks after it, briefly.
4. If the verdict is `accept`, say in one line that every required check
   passed, and quote the test-evidence line that shows the behavior after the
   change.
5. In live mode, after the per-check summary, report any voice-guide rule
   the PR title or description breaks (quoting the rule and the draft line),
   and any step of this procedure that was silent or unclear for this
   package.
6. End with the JSON block from `SKILL.md`, listing every check in rubric
   order with its grade and one line of evidence, then the verdict. Put
   nothing after the JSON block.
