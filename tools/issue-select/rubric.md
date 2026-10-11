# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.
-->

## Checks

One check asks one question. A check that would need the word "or" in its
pass condition is two checks; see the design note below.

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| commits-alive | Dates of the last 5 default-branch commits | At least 2 of those 5 commits are within 90 days (of the capture date in eval mode, of today in live mode) | required |
| not-archived | The `archived:` flag on the repo line / the archived banner on the repo page | The repo is not archived | required |
| pushed-recently | Date of the last push to any branch | That push is within 90 days (capture date in eval mode, today in live mode) | required |
| single-goal | Issue title and body: the list of deliverables it asks for | The issue asks for one deliverable — one bug, one feature, or one doc topic. Fails if the body enumerates two or more separable deliverables that could each ship as their own PR, or if it labels itself umbrella / tracking / epic / meta. A checklist whose items are all steps toward the same deliverable passes. | required |
| actionable-change | Issue body: what it asks someone to do | The issue asks for a change to the repo's code, docs, tests, or config. Fails if it only asks for help using the project, for an answer, or for an opinion, with nothing to change. | required |
| spec-concrete | Issue body: the end state it describes | The body names a concrete end state — the behavior that should change, the wrong output to fix, or the text to add. Fails if it is a wish with no spec ("would be nice if X were faster") that leaves someone to decide what to build first. A terse body that still names a concrete end state passes. | required |
| bounded-footprint | Issue body: the files, modules, or call sites the work would touch | The work fits inside one bounded area. Fails if the issue asks for a repo-wide sweep — renaming or migrating every call site, or changing a shared convention everywhere. Touching several files within one subsystem passes. | required |
| no-core-rewrite | Comments by Owner / Member / Collaborator in the thread | No maintainer says the fix needs changes to core internals or architecture. Maintainer silence on the point passes. | required |
| design-settled | Thread: disagreement about the approach, plus the state of any linked or mentioned PRs | The approach is decided. Fails only when both are true: (1) the thread shows disagreement about the approach that no maintainer has settled, and (2) at least one earlier PR attempt was closed unmerged. | required |
| no-assignee | The issue's Assignees field | The Assignees field is empty | required |
| no-open-pr | Linked PRs in the Development box, plus any PR mentioned in the thread | No open PR is linked to or mentioned for this issue | required |
| no-live-claim | Claim comments in the thread, with their dates and any maintainer reply | No claim comment within the last 30 days that a maintainer left unanswered | required |
| ai-policy-allows | CONTRIBUTING.md / AI_POLICY.md / the repo-facts contribution policy line | No outright ban on AI-assisted contributions. Silence passes; stated conditions pass. | required |
| responds-to-issues | Maintainer first-response times in the recent issue sample | At least one maintainer reply within 30 days somewhere in the sample | preferred |

## Verdict rule

Accept only if every required check passes. `unclear` is treated as `fail`
for every check. `responds-to-issues` (preferred) never changes the
verdict — it only breaks ties when ranking accepted issues.

## Design note: why the checks are this small

An earlier version of this rubric had a single `scope-fits` check whose
pass condition listed six different ways to fail, joined by semicolons.
It behaved like a long `if` with many OR-branches: when a run disagreed
with gold, the output said only "scope-fits: fail", which gave no way to
tell *which* branch fired, and the model's reading of the cell was not
stable across runs with identical wording.

Those six conditions are now six checks — `single-goal`,
`actionable-change`, `spec-concrete`, `bounded-footprint`,
`no-core-rewrite`, `design-settled` — each with its own evidence and its
own one-question pass condition. The two compound checks on the repo and
availability sides (`shipped-recently`, `unclaimed`) were split the same
way for the same reason. The verdict is unchanged: every required check
still has to pass, so an issue that used to fail `scope-fits` on one
branch now fails exactly the check that names that branch.

Rules for adding a check here:

- One question per check. If the pass condition needs "or", split it.
- Name the failing case, not just the passing one, so a `fail` is
  defensible from the evidence quote alone.
- Write the carve-outs ("a terse body still passes") into the check they
  belong to, rather than as a general exception at the bottom.
- A conjunction is allowed when the check still asks one question and
  every part is objectively checkable — `design-settled` is the only one
  here, and it numbers its two parts so a `fail` says which held.
