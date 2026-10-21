# Rubric: is this pull request ready to submit?

## Checks

One check asks one question. The first four read plan fidelity (silent
drift), the next five read the test evidence (not tested), the next two read
the diff itself (unreviewable), and the last four required checks read the
standards the repo states (standards wall).

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diff-within-plan | The list of changed files and hunks in the diff, read against the plan's in-scope files and its not-in-scope line, plus any deviation note | Every changed file and every hunk falls inside what the plan says it will change, or inside a deviation note that names it. Fails if the diff changes a file or makes a change the plan does not name and no deviation note covers (for example a rewrite of a file the plan never touches), even when the description says "no changes beyond the plan". | required |
| diff-delivers-plan | The plan's approach steps, read against what the diff actually changes | The diff carries out every in-scope step of the plan. Fails if a planned step is missing from the diff and neither the description nor a deviation note says it was deferred or dropped (for example a plan to fix an input translation while the diff only bumps a dependency). A planned step the PR says it left out, with the reason, passes. | required |
| description-matches-diff | The description's claims about what changed and how closely it follows the plan, read against the diff | Every claim the description makes about the change is true of the diff, including any claim that it stays inside the plan. Fails if the description claims a change, a file, or a fidelity the diff contradicts. | required |
| deviations-recorded | The differences between the diff and the plan's posted approach, read against the plan's Deviations section and the description's notes | Every way the diff differs from the plan's approach is written down in the Deviations section or the description's notes for reviewers. Passes when the diff matches the plan and there is nothing to record. Fails if the diff differs from the plan and nothing records it. | required |
| test-observable-result | The test evidence, read for an observable before and after of the issue's behavior | The evidence shows the issue's behavior before the change and after it, each as an output, exit status, value, or test result someone can read. Fails if the evidence only says "tests pass", "verified", or "works" with nothing named, or shows only the after. | required |
| test-covers-test-plan | The test evidence, read against each scenario or failure mode the plan's test plan names | The evidence covers every scenario the plan's test plan names. The question is whether the evidence speaks to the scenario at all: it shows the run, or states that the scenario was run and what the result was. Fails if the plan's test plan names a scenario (for example a second failure mode) that the evidence says nothing about, and the PR does not say it was not run. A scenario the PR openly says was not run, with the reason, passes. | required |
| test-exercises-changed-path | The test evidence, read against the files and functions the diff changes | The evidence runs through the code the diff changes, so its result could differ without the change. Fails if the evidence exercises only a path the diff does not touch. | required |
| repo-checks-run | The test evidence, read against what the repo's PR template or contributing guide tells contributors to run | Passes if the repo names nothing to run, or if everything it names was run and its result is shown, including a failing result reported with its reason or a command that cannot run on the project stated as such. Fails if something the repo tells contributors to run is absent from the evidence with no mention. The dividing line is whether the repo asks for something to execute, which leaves output the evidence can show, or asks for the author's attestation about their own work, which leaves none. An attestation is read by `template-filled`, not here. | required |
| test-on-declared-environment | The test evidence's stated environment (runtime and version), read against the environment the repo declares (the repo-facts block in eval mode; setup docs, CI configuration, and project metadata live) | Passes if the repo declares no environment, or if the evidence ran on the declared environment, or if the evidence names the difference and says why. Fails if the evidence ran on a different runtime or version from the one the repo declares and says nothing about the difference. A newer version the repo's metadata allows still needs to be named when the repo's CI or setup docs pin another. | required |
| no-debris | The diff's added lines | The added lines contain no debug prints or logging added for debugging, no commented-out code, no dead or unreachable code, and no leftover TODO notes from working. Fails if any of these is in the diff. | required |
| no-churn-or-unrelated-hunks | The diff's hunks, read for lines changed without a bearing on the planned change | Every hunk changes behavior or tests for the planned change. Fails if a hunk only reformats, reorders, or renames lines, or changes something unrelated to the issue, so a reviewer must read it to find the fix. | required |
| template-filled | The description, read against the sections of the repo's PR template (live: `.github/PULL_REQUEST_TEMPLATE.md`; eval: the repo-facts block) | Passes if the repo has no PR template. If it has one, every section holds real content for this change, and no checked box is contradicted by the package. The dividing line for a checked box is what it asserts: a box that asserts the output of a command needs that output in the evidence; a box that attests to a property of the author's own work passes unless the diff or the evidence contradicts it. Fails if a section is left empty, left as the template's placeholder text, deleted, or a checked box is contradicted or asserts command output the evidence does not show. | required |
| ai-disclosure-met | The repo's contribution policy (the repo-facts block in eval mode; `docs/CONTRIBUTING.md` and any AI policy file live), read against the description. Treat these packages as AI-assisted work. | Passes if the policy has no disclosure requirement covering pull requests (silence, a permissive policy, or a rule that applies only to issue comments all pass). If the policy requires disclosing AI use in pull requests, passes only if the description contains a plain sentence disclosing AI assistance (naming the tool and the extent when the policy asks for them). Fails if disclosure is required and the description has none. | required |
| issue-referenced | The description, read for the number of the issue the PR resolves | The description names the issue the PR resolves (for example `Closes #72`) and it is the issue the plan belongs to. Fails if it names no issue, or a different one. | required |
| thread-direction-followed | The description and diff, read against any explicit maintainer direction in the thread highlights (live: the issue thread) | Passes if the thread holds no maintainer direction that bears on the change, or if the PR follows it or says why it does not. Fails if the PR ignores or contradicts explicit maintainer direction. | required |
| description-says-what-and-why | The description's summary read alone | A reviewer reading only the summary can say what the change does and why. | preferred |

## Verdict rule

Accept only if every required check passes. `unclear` counts as `fail` for
every required check. `description-says-what-and-why` (preferred) never
changes the verdict. A terse pull request that passes every required check
is ready: a PR is judged on what its diff and evidence show, not on how
long its description is. A pull request that honestly discloses a
shortfall (a step left out, a scenario not run, a deviation) and has the
disclosure where the relevant check looks passes that check; a rubric that
equates "less than everything" with "hold" is wrong.

## Design note: why the checks are this small

Each failure family maps to named checks, so a `fail` says which part is
missing and nothing has to be inferred from a long cell:

- **Silent drift:** `diff-within-plan` (nothing extra), `diff-delivers-plan`
  (nothing missing), `description-matches-diff` (the words are true), and
  `deviations-recorded` (every difference is written down). A beautiful,
  confident description can sit on a diff whose second hunk rewrites a file
  the plan never touches, so the description is read against the diff, never
  graded on how it sounds.
- **Not tested:** `test-observable-result` (a before and after someone can
  read), `test-covers-test-plan` (each named scenario), 
  `test-exercises-changed-path` (the evidence could fail),
  `repo-checks-run` (the repo's own checks), and `test-on-declared-environment`
  (the evidence ran where the project says it should run).
- **Unreviewable:** `no-debris` and `no-churn-or-unrelated-hunks`, because
  debris and drive-by hunks bury the fix even when the fix is right.
- **Standards wall:** `template-filled`, `ai-disclosure-met`,
  `issue-referenced`, and `thread-direction-followed`, because a PR can be
  perfect on every check above and still be unsubmittable under the repo's
  stated rules.

Rules for adding a check here:

- One question per check. A pass condition may list several acceptable
  forms of the same answer, but if it joins two different questions with
  "or" or "and", split it.
- Name the failing case, not just the passing one.
- Judge the thing itself (does the diff fall inside the plan?), never the
  write-up's shape (length, headings, number of commits).
- Write carve-outs ("a stated deferral passes", "silence passes") into the
  check they belong to.
