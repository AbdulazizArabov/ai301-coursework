# Evidence guide: where evidence lives in a PR package

A PR package has these parts. In an eval bundle: Repo facts, Issue, Thread
highlights, Plan context, and the Candidate PR (Title, Description,
Commits, Diff, Test evidence). In live mode the same facts come from the
working copy and GitHub: `plan.md` with its `## Deviations` section, the
branch's diff from `git diff main...HEAD`, `git log main..HEAD --oneline`,
`pr_draft.md` (title on the first line, description under it),
`test_evidence.md`, the issue thread and the student's posted plan comment,
`.github/PULL_REQUEST_TEMPLATE.md`, and `docs/CONTRIBUTING.md`.

## Plan fidelity (harness category: silent-drift)

- **Where it lives.** The plan's scope and boundary: in an eval bundle, the
  Plan context block (its "Files", "In", "Not in scope" lines, its approach
  steps, and any deviation note); live, `plan.md` (Scope, Files, Approach)
  and its `## Deviations` section. What actually changed: the Candidate PR's
  Diff (the file headers and hunks) and Commits; live, `git diff main...HEAD`
  and `git diff main...HEAD --stat`. What the PR says about itself: the
  Description (live: `pr_draft.md`).
- **What good looks like.** Every changed file and hunk is a file or change
  the plan names, or one a deviation note names; every approach step shows
  up as a hunk, or the description or a deviation note says it was left out
  and why; every claim in the description about the change (and any claim of
  "no changes beyond the plan") is true of the diff. Silent drift goes in
  two directions: the diff does more than the plan (an extra file, or a
  rewrite folded into a file the plan did touch) or less (a planned step
  missing) with no note. A description claiming more or less than the diff
  delivers is drift, not a wording problem. An honest deviation is a note
  that ties the mismatch back to the plan: it names what differs and why.

## Test evidence (harness category: not-tested)

- **Where it lives.** The Candidate PR's Test evidence section, read against
  the Plan context's test plan and the repro evidence in it; live,
  `test_evidence.md` against `plan.md`'s test plan and against the repro
  comment's steps. The repo's own checks: the Repo facts "pull requests"
  line (eval); live, the checks listed in `.github/PULL_REQUEST_TEMPLATE.md`
  and `docs/CONTRIBUTING.md`.
- **What good looks like.** The evidence shows the issue's behavior before
  the change and after it, as output a stranger can read (a result, an exit
  status, a number, a test going from fail to pass); it covers each scenario
  the plan's test plan names (a plan that names two failure modes needs both
  shown, or an honest note on the one not run); its commands run through the
  code the diff changes (a green run of a path the diff never touches proves
  nothing); and each check the repo says to run appears with its result.
  The evidence also says where it ran (runtime and version), and that matches
  what the repo declares (eval: the repo-facts block; live: the setup docs,
  the CI configuration, and the project metadata), or names the difference
  and why. "Tests pass" and "verified" with nothing named are not evidence. A failing
  check reported with its reason, or a check that cannot run on the project
  said so, is evidence; a check left out silently is not.

## Diff quality (harness category: unreviewable)

- **Where it lives.** The Candidate PR's Diff and Commits; live, the output
  of `git diff main...HEAD` and `git log main..HEAD --oneline`.
- **What good looks like.** The fix is visible and nothing else rides along.
  The debris tells, in the added lines: a debug print or a logging line added
  to see what happens, commented-out code, dead or unreachable code, a TODO
  left from working. The churn tells: a hunk that only reformats, reorders,
  or renames lines; a hunk in a file or area the issue does not concern. A
  reviewer should be able to find the whole change without reading past
  hunks that have nothing to do with it.

## Standards and comms (harness category: standards-wall)

- **Where it lives.** What the repo asks: in an eval bundle, the Repo facts
  block (the "pull requests" line for template sections and other asks, the
  "contribution policy" line for contribution asks and any AI-use rule); live,
  `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, and any AI
  policy file. How the PR answers: the Description (live: `pr_draft.md`), its
  Title, and the issue number it names. Maintainer direction: the Thread
  highlights (live: the issue thread, lines from an owner, member, or
  collaborator).
- **What good looks like.** Each template section holds real content for this
  change (a section left as the template's placeholder text, empty, or
  removed is ignored, not filled); no ticked box is contradicted by the package, and a box that claims a result
  has that result in the evidence;
  the description names the issue it resolves; where the policy requires AI
  disclosure in pull requests, the description has a plain sentence saying AI
  was used, naming the tool and the extent when the policy asks; explicit
  maintainer direction is followed or answered. A policy that applies only to
  issue comments, or is silent, needs no disclosure in the PR. Boilerplate
  that would fit any PR is not compliance. (Whether the description's claims
  match the diff is plan fidelity, above.)
