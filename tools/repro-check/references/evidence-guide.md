# Evidence guide: where proof lives in a reproduction package

Every rubric check names an evidence source. This guide maps each proof
family to the exact place to look: in an eval bundle (a markdown file
with the sections `Repo facts`, `Issue`, `Thread highlights`,
`Candidate claim comment`, `Candidate repro report`) and in live mode
(the issue on GitHub, the repo's docs, and the student's draft files).
In eval mode use only the bundle; the bundle is the whole world.

Two things are always the reference, never the thing being graded: the
issue (what the bug is) and the repo facts (what the repo asks for). The
claim comment and the repro report are the candidate.

## Environment

**Where it lives.**
- Candidate side: the repro report, usually a line starting "Environment:"
  or a table, near the top or just before the steps. In live mode this is
  the draft repro file.
- Reference side: the versions and platform the issue names. In the bundle
  they are in the `Issue` section (a "Version:" line, an installed-versions
  block, "reported on ...") and in `Thread highlights` (a commenter
  confirming on another version). The `Repo facts` block gives the latest
  release. Live: the issue body, the issue template fields, and the
  repo's Releases box.

**What good looks like.** The report names an operating system and the
version or commit of the software under test, so a stranger can place the
run. The version is the one the issue was reported or confirmed on, a
newer one, or the latest release, or the report says in words that it
tested something else and why. A different OS or shell from the reporter
is fine and only matters when the issue says the bug depends on it. An
environment you can only infer from the output (a path that looks like
Windows) is not recorded.

## Steps

**Where it lives.** The numbered steps, commands, and code blocks in the
repro report, between the environment and the observed result. In live
mode, also check anything the steps link to: a playground link, a gist,
a file named in the issue.

**What good looks like.** A stranger on a clean machine could run the
steps in order: every command is written out, every input file or config
is shown or comes from the issue or the repo, and the trigger step is
explicit. Prose that stands in for an input ("set up the project", "our
internal config", "a large file") is a gap. Something private that the
report says the reader cannot have is a gap no matter how honest the
report is about it. An honest cannot-reproduce has steps too; it passes
this check when they are complete.

## Behavior shown

**Where it lives.** The pasted artifact in the repro report: a code block
of command output, a log or stack trace excerpt, a printed result, or a
description of a screenshot. Read it against the symptom in the `Issue`
section (live: the issue body): the error message or exception type, the
exit status, whether the program crashed or kept running, the wrong value
or wrong output.

**What good looks like.** The artifact contains the issue's own symptom:
the same error text or type, the same crash or non-crash, the same wrong
output, produced by the issue's trigger. It is an adjacent behavior when
it shows any of these instead: a graceful argument or syntax error where
the issue has a crash or panic; output of a modified input where the
issue has a different input; garbled output with the program still
running where the issue has a crash; a program that merely starts, lists
its version, or shows its UI. Compare the key line of the artifact to the
key line of the issue before trusting the report's own words ("exactly as
described", "matching the issue"). For a cannot-reproduce, good is the
artifact showing a real run of the issue's trigger in which the symptom
is absent.

## Honesty

**Where it lives.** The report's result sentences ("Result:", "Actual:",
"Conclusion", "confirmed", "verified", "guaranteed", "the cause is"),
read next to its artifact and environment line.

**What good looks like.** Every claim in the result sentences is backed
by something shown above it, and its scope is no wider than the
environments actually tested. Signals of a report claiming more than it
shows: a root cause or race condition named with no experiment shown;
"verified" or "reproduces every time" with no output; a confirmation on
one release that is generalized to another release the report never ran;
an artifact that contradicts the sentence next to it. Signals of an
honest report: it states a negative result as a negative result, names
what it did and did not test, and says what differed from the issue's
conditions. An honest cannot-reproduce is a pass here.

## Comms

**Where it lives.**
- The claim comment: the `Candidate claim comment` section (live: the
  draft claim file), read against the `Issue` title, body, and thread.
- The repo's rules: the `contribution policy` and `bug reports` lines of
  the `Repo facts` block (live: CONTRIBUTING.md, AI_POLICY.md, any
  `.github/` issue template, and the policy sections on AI use). Quote
  the sentence of the policy that decides the AI-use check.

**What good looks like.**
- Specific: the claim names something from this issue (its symptom, the
  file or function the thread points at, the result of the report) and
  says what the author will do next. A comment that could be pasted onto
  any issue is boilerplate, however friendly.
- Honest about intent: it promises investigation or a report. A fix, a
  date, "guaranteed", or "please reserve this for me" is an over-promise.
- AI policy: find out whether the policy requires disclosing AI use in
  issue comments or reports. A rule that covers only pull requests, a
  rule that asks for human-written own-words comments, or a permissive
  "AI tools welcome, you are responsible" rule does not require a
  disclosure sentence. A rule that says AI use must be disclosed in any
  form, or in comments, does, and the package passes only if a comment
  contains a plain sentence saying AI assistance was used. Treat the
  package as AI-assisted work.
