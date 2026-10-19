# Evidence guide: where evidence lives in a plan package

A package (an eval bundle, or live the student's drafts plus the issue
thread) has six parts: Repo facts, Issue, Thread highlights, Repro
evidence, Candidate plan, and Candidate plan comment. In eval mode use only
these parts. In live mode the same facts come from the places named
under "Live" below.

## Diagnosis and grounding

- **Where it lives.** The stated cause is the plan's "Cause" or
  "Diagnosis" statement (the first lines of the Candidate plan). The
  behavior it must explain is in the Repro evidence block: the numbered
  steps, the "Actual" output, and any "Control" line or ruled-out variant
  (for example the same input run without a flag, or with a component
  disabled). Live: the cause is in `plan.md`; the behavior is in the
  student's posted repro comment on the issue, which `plan.md` must quote.
- **What good looks like.** The cause names a mechanism that accounts for
  the Actual output and does not conflict with any control run. A control
  that still fails with the blamed part removed, or an observation the
  cause cannot explain, means the diagnosis does not follow from the
  evidence, however confident or well written it is. A cause copied from a
  thread comment is only as good as the repro evidence behind it. The
  change site should be the stage where the cause says the fault arises,
  not a later stage that shows or hides it.

## Scope

- **Where it lives.** The Candidate plan's in-scope statement ("In:",
  "Scope", "One bounded change"), its not-in-scope statement ("Out:",
  "Not in scope", "Not in"), and the files it names. The issue's title and
  body (the Issue section) say what is being asked.
- **What good looks like.** One bounded change that resolves what the issue
  reports, touching only the files that change needs. Creep looks like a
  second purpose (rename helpers, migrate config, tidy docs, add an
  option, redesign the module) or a file named only because it was seen.
  A plan may fix part of the issue if it says which part it defers and
  why; that is a boundary, not a gap. A part of the issue dropped with no
  mention is a gap.

## Executability

- **Where it lives.** The Candidate plan's file or area names, and its
  Approach (or "Change") lines.
- **What good looks like.** At least one specific file, function, or area
  is named, and the approach says what the change is (what is added,
  removed, or computed differently) so a developer who has never seen the
  repo could start. "Look into", "poke around", "make it robust", and "the
  relevant code" are directions to investigate, not an approach.

## Test plan

- **Where it lives.** The Candidate plan's "Test" or "Test plan" lines,
  read against the Repro evidence's steps and its "Actual" and "Expected"
  lines. Live: `plan.md`'s test plan against the student's repro comment.
- **What good looks like.** The test plan names a command or action and the
  result it must now produce, and that result is the issue's behavior
  changing (a number, output text, exit status, or a test going from fail
  to pass), ideally written down before the fix. It re-runs the repro
  evidence's own steps (or a check through the same code path). "Run the
  full suite", "see if it works", and "check nothing regresses" name no
  outcome for the fix, so they do not decide anything.

## Honesty

- **Where it lives.** The Candidate plan's "Risks" or "Unknowns" lines and
  any sentence that states something as certain ("confirmed", "no other
  caller", "will not affect", "verified"). Live: also `plan.md`'s
  `## Deviations` section, where a mid-build change from the posted plan is
  recorded.
- **What good looks like.** What the repro evidence did not show is
  written as an assumption or an unknown ("I have not checked other
  callers"), not as fact. A stated unknown is honest; a confident claim
  with nothing in the Repro evidence behind it is not. A deviation found
  in the build is written into the plan, not left only in the diff.

## Comms

- **Where it lives.** The Candidate plan comment, read against (a) the
  Thread highlights, where a maintainer's direction is a line from an
  owner, member, or collaborator that sets a constraint, decision,
  request, or "do not"; (b) the Repo facts block's "bug reports" line
  (template asks) and "contribution policy" line (contribution asks and AI
  rules); and (c) the Candidate plan, whose contents bound what the comment
  may promise. Live: the real thread on the issue and the repo's
  CONTRIBUTING.md, issue template, and any AI policy file.
- **What good looks like.** The comment engages what the maintainer
  already said (follows it, or says why it differs), promises only what the
  plan contains (an investigation or a pull request for the planned
  change; never "assign me", a deadline, or a guarantee), honors the
  repo's stated asks, and contains a plain disclosure sentence when the
  policy requires disclosure or requires comments in the author's own
  words. Boilerplate that would fit any issue is not engagement with this
  thread. A policy that applies only to pull requests, or is silent, needs
  no disclosure in the comment.
