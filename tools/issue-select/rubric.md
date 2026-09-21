# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| commits-alive | Last 5 default-branch commit dates | At least 2 of the last 5 commits are within 90 days (of capture date in eval, today in live) | required |
| shipped-recently | Archived flag + latest release date + last push to any branch | Not archived, and last push (any branch) within 90 days | required |
| responds-to-issues | Maintainer/Owner/Collaborator reply times in recent issue threads | At least one maintainer reply within 30 days somewhere in the sample | preferred |
| scope-fits | Issue body + comment thread | Serves one coherent goal (a single bug, feature, or doc topic), even if the fix touches multiple files or has several concrete sub-steps toward that one goal. FAILS if: the issue explicitly bundles multiple separable features/tasks meant to be split into separate work; it requires a codebase-wide/cross-cutting change; a maintainer states it needs core/internal architecture changes; it is a pure usage/support question with no actionable fix; the thread shows unresolved design debate together with a history of closed/abandoned PR attempts and no maintainer-settled direction; or it is a vague feature request/wish with no concrete spec that hides an undecided design or product decision. A checklist of concrete sub-steps toward one goal, or a terse body, does NOT by itself fail this check. | required |
| unclaimed | Assignees field, linked PRs, claim comments | Assignees empty, no open linked PR, and no claim comment within 30 days left unanswered by a maintainer | required |
| ai-policy-allows | CONTRIBUTING.md / AI_POLICY.md / repo-facts contribution policy line | No outright ban on AI-assisted contributions (silence or stated conditions both pass) | required |

## Verdict rule

Accept only if every required check passes. `unclear` is treated as `fail` for every check. `responds-to-issues` (preferred) never changes the verdict — it only breaks ties when ranking accepted issues.
