# Rubric: is this reproduction package ready to post?

## Checks

One check asks one question. Checks 1-6 read the repro report; checks 7-9
read the claim comment; check 10 reads the repo's stated policy against
both comments.

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| env-recorded | The repro report's environment record: the line(s) before or inside the steps naming where it was run | The report names BOTH the operating system AND the version (or commit) of the software under test. Fails if either is missing, or if the environment can only be guessed from the output. A shell, runtime, or driver the issue depends on is also named when the issue's bug is specific to it. | required |
| version-matches-target | The version the report tested, read against the versions the issue names (issue body, template fields, thread, the repo-facts "latest release" line) | The tested version is the issue's version, a newer one, or the latest release / main, OR the report explicitly says it tested a different version and why. Fails if the report tested an OLDER version than the one the issue was reported or confirmed on, and says nothing about the difference. Running on a different OS or shell is not this check. | required |
| steps-rerunnable | The report's steps and commands, read as a stranger starting from a clean machine | Every input the steps depend on (commands, files, config, project, link) is either written out in the report or publicly obtainable from the issue or repo. Fails if any step depends on something private, unshared, or too vague to recreate ("our internal config", "set up the project", "checked out our monorepo", "a large file"). An input described in prose passes when the description names the exact elements that trigger the issue, so a stranger could recreate it in one step (for example "a minimal env.yml with a valid `dependencies:` list plus a `category:` section"). | required |
| artifact-shown | The report's pasted output, log, transcript, or screenshot description from an actual run | The report contains at least one pasted output or observation from a run it performed, quoted in the report itself. Fails if the report only asserts results ("verified", "confirmed", "reproduces every time") without any pasted output from the run. | required |
| artifact-matches-issue | The pasted artifact, read line by line against the symptom the issue describes (the exact error text, exit status or crash, wrong output, or wrong behavior) | The artifact shows the SAME symptom the issue describes: same error message or exception type, same crash vs non-crash, same wrong output. Fails if it shows a different or adjacent outcome (a graceful error where the issue has a crash, a syntax error where the issue has a panic, garbled output with the program still alive where the issue has a crash, or only that the program starts), even when the report calls it a match. For an honest cannot-reproduce, passes if the artifact shows a real attempt at the issue's trigger and the report says the symptom did not appear. | required |
| conclusion-within-evidence | The report's stated result, scope, and any causes or guarantees it claims, read against what its artifact actually shows | The report states exactly what its artifact supports: reproduced, or not reproduced, only on the environment it tested. Fails if it asserts a root cause with no shown evidence, calls an observation a confirmation when the artifact shows something else, generalizes to versions or builds it did not test, or claims it "verified" something no artifact shows as its headline finding. A one-sentence side observation, such as a control run that is described but not pasted, does not fail this check when the headline result is shown in the artifact and the side observation does not change what the artifact proves. | required |
| claim-specific | The claim comment, read against the issue's title, body, and thread | The claim comment names at least one fact specific to this issue (its symptom, a file or function, a pointer from the thread, or the result of the report) that could not be pasted onto a different issue unchanged. Fails if the comment is interchangeable text ("I'd like to work on this, please assign it to me") or flattery of the project. | required |
| claim-next-step | The claim comment: what it says the author will do next | The claim states a concrete next investigation step the author will take (what they will read, test, or report), so a reader knows what to expect. Fails if the comment only asks for the issue or states no next step. | required |
| claim-no-overpromise | The claim comment: any promise of outcome, date, or ownership | The claim promises at most investigation or a report. Fails if it promises a fix, a deadline ("within 2 days"), a guaranteed result, or asks maintainers to reserve or assign the issue. | required |
| ai-disclosure-met | The repo's contribution policy (the repo-facts "contribution policy" line in eval mode; CONTRIBUTING.md and any AI policy file in live mode), read against the text of the claim comment and the repro report. Treat these packages as AI-assisted work. | Passes if the policy has no disclosure requirement that covers issue comments or reports (silence, a permissive policy, an own-words rule, or a disclosure rule that applies only to pull requests all pass). If the policy DOES require disclosing AI use in issue comments or reports, passes only if at least one of the two comments contains a plain sentence disclosing AI assistance (naming the tool and the extent when the policy asks for them). Fails if disclosure is required and no comment contains one. | required |
| expected-vs-actual | The report's statement of expected and actual behavior | The report states what it expected and what it observed as two separate statements. | preferred |

## Verdict rule

Accept only if every required check passes. `unclear` is treated as `fail`
for every required check. `expected-vs-actual` (preferred) never changes
the verdict. A report that honestly says "could not reproduce" can still
accept: an evidenced cannot-reproduce passes every check above.

## Design note: why the checks are this small

Each proof family maps to named checks, so a `fail` says which proof is
missing and nothing has to be inferred from a long cell:

- **Environment:** `env-recorded`, `version-matches-target`.
- **Steps:** `steps-rerunnable`.
- **Behavior shown:** `artifact-shown` (is there output at all) is separate
  from `artifact-matches-issue` (is it the issue's symptom), because a
  long, confident, well-formatted report can contain real output of the
  wrong behavior. The second check reads the artifact, never the polish.
- **Honesty:** `conclusion-within-evidence` holds the words to the artifact
  in both directions, so a bare "I verified it" fails and an honest
  cannot-reproduce passes.
- **Comms:** the claim comment is three checks (`claim-specific`,
  `claim-next-step`, `claim-no-overpromise`) and the repo's AI-use policy
  is its own check (`ai-disclosure-met`), because a package can be perfect
  on every proof check and still be unpostable under the repo's rules.

Rules for adding a check here:

- One question per check. A pass condition may list several acceptable
  forms of the same answer, but if it joins two different questions with
  "or" or "and", split it.
- Name the failing case, not just the passing one.
- Judge the thing itself (does the artifact show the issue's behavior?),
  never the write-up's shape (length, headings, step count).
- Write carve-outs ("a different OS is not this check", "an honest
  cannot-reproduce passes") into the check they belong to.
