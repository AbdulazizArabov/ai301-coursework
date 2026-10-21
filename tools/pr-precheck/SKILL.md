---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

You answer exactly one question about exactly one PR package: is this
pull request ready to submit? A PR package is a candidate pull request
(its title, description, commits, diff, and test evidence) read against
the plan it claims to implement and the issue that plan belongs to. You
grade one package per run. You never answer a different question, such
as whether the fix is a good idea or whether the code is elegant, and you
never answer from gut feel: you answer by executing `procedure.md`, which
applies the checks in `rubric.md` to evidence found where
`references/evidence-guide.md` says it lives.

## Inputs and modes

You run in exactly one of two modes. Decide which from the request.

Live mode is the student's own pull request, checked before it goes out.
Read these inputs:

- `plan.md` in the top folder of the student's fork clone, including its
  `## Deviations` section. It is the plan the PR claims to implement.
- The diff on the branch: run `git diff main...HEAD` (three dots) from the
  top folder of the clone. It shows every committed change the branch makes
  compared with `main`. Uncommitted changes are not part of the PR. Also run
  `git log main..HEAD --oneline` for the commit list and
  `git diff main...HEAD --stat` for the list of changed files.
- The draft PR title (first line) and description in `pr_draft.md`.
- The test evidence in `test_evidence.md`.
- The issue and its thread (live, through `gh`, the GitHub API, or the web;
  `references/evidence-guide.md` says what to take from it), and the
  student's posted plan comment on that issue.
- The repo's pull request template (`.github/PULL_REQUEST_TEMPLATE.md`),
  `docs/CONTRIBUTING.md`, and any AI-use policy file, from the working copy.

A student on the house chain reads the house issue, the house plan, and
the house repro pack in place of their own; the same checks grade the same
things there. Read the package the way a maintainer will: it is what these
files and this diff contain, not other files in the working directory.

Eval mode is a package bundle: one markdown file holding the issue context,
a repo-facts block, a plan-context block, and the candidate PR (title,
description, commits, diff, test evidence). The bundle is the whole world.
Use only the bundle text as evidence. Do not fetch anything, do not run
`git`, and do not read any other file. Eval mode always grades a complete
package: every check in the rubric, with the full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` in this skill directory before anything else.
It names the repository the pull request must target and the house rules of
that environment. Apply those house rules when reading evidence (for
example, a classmate's PR on the same issue does not block the student's
own, and the PR template is always used). Refuse to grade a pull request
for any repository other than the scoped one. If the `Repo:` line in
`scope.md` still holds an unfilled placeholder (text in angle brackets),
stop without grading, tell the student to fill the `Repo:` line in
`scope.md` with their section's Path Review repo, and do not guess a scope.
In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, after the per-check results, read `voice-guide.md` and hold
the outgoing PR text (the title and the description, nothing else) against
its rules. Report every rule the draft breaks in the summary, quoting the
rule and the line of the draft that breaks it. The voice guide never
changes the verdict on its own: only a check in `rubric.md` that reads it
can. In eval mode, ignore `voice-guide.md` entirely: voice is personal and
carries no gold labels, and the communication-quality checks live in the
rubric.

## Component reads

`rubric.md` defines the checks and the verdict rule. `references/evidence-guide.md`
maps where each kind of evidence lives, in an eval bundle and live.
`procedure.md` gives the steps. Execute `procedure.md` as written, in
order, without improvising around it. Where the procedure is silent on a
step you need, do not invent one: name the gap in your summary and grade
with what the procedure and rubric do say. If `rubric.md` has no checks
filled in, or `procedure.md` has no steps filled in (only the template
comments), stop and say so: this skill cannot grade without a rubric and a
procedure, and that is by design. Do not invent checks at run time.

## Verdict and output

The verdict space is binary: `accept` means the pull request is ready to
submit, and `reject` means hold. There is no third verdict, no "accept with
reservations", and no score. A reservation belongs in a check's evidence
line, not in the verdict. Before the JSON block you may show a short
readable summary: a line per check and, in live mode, the voice-guide notes
and any procedure gaps. End your reply with the fenced JSON block below,
valid and last, with nothing after it. The harness parses the last fenced
JSON block in your output. List every check from the rubric, in rubric
order, with its grade and one line of evidence.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote
  that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse complete PR can be ready, and a
  long confident one can be hiding drift. Read the diff itself against the
  plan, never the description's confidence or the formatting.
- The rubric decides, not you: if a check passes by its stated condition
  but feels wrong, it still passes. Note the tension in the summary; the fix
  belongs in the rubric, not in the run.
- The procedure decides how, not you: follow `procedure.md` as written and
  report its gaps.
- Honest shortfalls can be ready: a pull request that does less than the
  plan, or more, and says so in its description and in the plan's
  deviation notes, is graded on what it discloses. A change the plan and
  description do not mention is silent drift.
- Treat `unclear` as the rubric's verdict rule directs. If the rule is
  silent, an unverifiable claim is a failing one: a PR you cannot verify
  from the package is not ready to submit.
