# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
Unit 1\ai301-unit1-starter-main\ai301-unit1-starter-main\eval> claude "issue-select: grade these candidate first issues: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/62 https://github.com/codepath/pathreview-ai301-fa26-s3/issues/63 https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72 https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60"
 ▐▛███▛█   Claude Code v2.1.278
▝▜██████▀  Opus 5 (1M context) with high effort · Claude Enterprise
  ▝▝ ▝▝    ~\Desktop\Codepath Fall 2026\Unit 1\ai301-unit1-starter-main\ai301-unit1-starter-main\eval

  Updated to latest. Got 67 features, 396 bugfixes, and 150 other changes.
  code.claude.com/docs/en/changelog for details


> issue-select: grade these candidate first issues: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/62
  https://github.com/codepath/pathreview-ai301-fa26-s3/issues/63
  https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72
  https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60

● I'll invoke the issue-select skill to grade these against its rubric.

● Skill(issue-select)
  ⎿  Successfully loaded skill

● I'll start by reading the skill's scope and rubric.

  Read 3 files (ctrl+o to expand)

● Bash(gh --version 2>&1 | head -3)
  ⎿  /usr/bin/bash: line 1: gh: command not found

● PowerShell((Get-Command gh -ErrorAction SilentlyContinue).Source)
  ⎿  (No output)

● Fetch(https://api.github.com/repos/codepath/pathreview-ai301-fa26-s3)
  ⎿  Received 6.6KB (200 OK)

● Fetch(https://api.github.com/repos/codepath/pathreview-ai301-fa26-s3/issues/62)
  ⎿  Received 4.1KB (200 OK)

● Fetch(https://api.github.com/repos/codepath/pathreview-ai301-fa26-s3/commits?per_page=5)
  ⎿  Received 19.8KB (200 OK)

● Fetch(https://api.github.com/repos/codepath/pathreview-ai301-fa26-s3/issues/62/comments)
  ⎿  Received 1.7KB (200 OK)

● Fetch(https://api.github.com/repos/codepath/pathreview-ai301-fa26-s3/issues/63)
  ⎿  Received 3.9KB (200 OK)

● Fetch(https://api.github.com/repos/codepath/pathreview-ai301-fa26-s3/issues/63/comments)
  ⎿  Received 2 bytes (200 OK)

● Fetch(https://api.github.com/repos/codepath/pathreview-ai301-fa26-s3/issues/72)
  ⎿  Received 3.9KB (200 OK)

● Fetch(https://api.github.com/repos/codepath/pathreview-ai301-fa26-s3/issues/72/comments)
  ⎿  Received 2 bytes (200 OK)

● Fetch(https://api.github.com/repos/codepath/pathreview-ai301-fa26-s3/issues/60)
  ⎿  Received 4.1KB (200 OK)

● Fetch(https://api.github.com/repos/codepath/pathreview-ai301-fa26-s3/issues/60/comments)
  ⎿  Received 2 bytes (200 OK)

● Fetch(https://api.github.com/repos/codepath/pathreview-ai301-fa26-s3/contents/)
  ⎿  Received 16.3KB (200 OK)

● Fetch(https://api.github.com/repos/codepath/pathreview-ai301-fa26-s3/pulls?state=all&per_page=50)
  ⎿  Received 2 bytes (200 OK)

● Fetch(https://api.github.com/repos/codepath/pathreview-ai301-fa26-s3/issues/comments?sort=created&direction=desc&per_p
       age=30)
  ⎿  Received 10.7KB (200 OK)

● Fetch(https://api.github.com/repos/codepath/pathreview-ai301-fa26-s3/issues/62/timeline)
  ⎿  Received 7.7KB (200 OK)

● Fetch(https://api.github.com/repos/codepath/pathreview-ai301-fa26-s3/contents/.github)
  ⎿  Received 2.6KB (200 OK)

● Fetch(https://api.github.com/repos/codepath/pathreview-ai301-fa26-s3/contents/docs)
  ⎿  Received 4.2KB (200 OK)

● Fetch(https://raw.githubusercontent.com/codepath/pathreview-ai301-fa26-s3/main/docs/CONTRIBUTING.md)
  ⎿  Received 6.5KB (200 OK)

● Fetch(https://raw.githubusercontent.com/codepath/pathreview-ai301-fa26-s3/main/.github/PULL_REQUEST_TEMPLATE.md)
  ⎿  Received 808 bytes (200 OK)

● All four are in scope (codepath/pathreview-ai301-fa26-s3), and all four pass every required check. Repo-level evidence
  is shared across them: not archived, last push 2026-09-16 (4 days ago), 5 of the last 5 default-branch commits within
  90 days, no AI restriction in docs/CONTRIBUTING.md or the PR template, and collaborator Aburke225 replying on issues
  as recently as 2026-09-16. The repo has zero pull requests, so no issue carries a linked-PR claim.

  Ranked (all accepted), by fit:

  1. #72 — verify_password raises UnknownHashError instead of returning False — best fit. A fail-open vs. fail-closed
     security judgment in pure Python (core/security.py), with an @pytest.mark.xfail test already written to unmark.
     It's exactly the "is this code actually correct and safe?" reasoning you said you want to practice, and the test
     makes your verdict checkable rather than a guess. No framework depth required.
  2. #60 — Faithfulness checker crashes on text: None — close second. The chunk.get("text", "") vs. present-but-None
     distinction is a classic trap in AI-written code, there's a reproduction one-liner and an existing failing test,
     and it's plain-Python with no framework knowledge needed.
  3. #63 — README scorer fixture too short for its assertion — smallest and safest, good for proving your pytest
     environment works end to end. It does carry a real judgment call (expand the fixture vs. loosen the assertion — one
     preserves the test's intent, the other hides it), but the stakes are lowest of the four.
  4. #62 — Health check references settings.redis_host — still a clean single-file fix, but it's the most
     infrastructure-coupled (settings wiring, Redis, the broad except that swallowed the AttributeError), so verifying
     it means more environment setup than reading. Also the only one with a classmate claim comment (skonda29,
     2026-09-21) — under the Path Review house rule that doesn't block you, but among four accepted issues it's a reason
     to prefer one of the others.

  Per-check grades:

  - #72 / #60 / #63 — commits-alive: pass · shipped-recently: pass · scope-fits: pass · unclaimed: pass (no assignees,
    no comments, no PRs) · ai-policy-allows: pass · responds-to-issues: pass
  - #62 — same, except unclaimed passes only via the house rule (one unanswered student claim comment).

  [
    {
      "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72",
      "checks": [
        {"name": "commits-alive", "grade": "pass", "evidence": "Last 5 default-branch commits: 3 on 2026-09-16, 2 on
  2026-08-24 (all within 90 days of 2026-09-20)"},
        {"name": "shipped-recently", "grade": "pass", "evidence": "archived: false; pushed_at 2026-09-16T21:50:20Z, 4
  days before today"},
        {"name": "responds-to-issues", "grade": "pass", "evidence": "Aburke225 (COLLABORATOR) commented on #52 and #43
  on 2026-09-16, within 30 days"},
        {"name": "scope-fits", "grade": "pass", "evidence": "One bug: 'Verification against a malformed hash should fail
  closed (return False), not raise' — core/security.py plus unmarking one xfail test"},
        {"name": "unclaimed", "grade": "pass", "evidence": "Assignees: none; comments: 0; repo-wide pulls list is empty
  so no linked PR"},
        {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and
  .github/PULL_REQUEST_TEMPLATE.md contain no AI mention; silence passes"}
      ],
      "verdict": "accept"
    },
    {
      "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60",
      "checks": [
        {"name": "commits-alive", "grade": "pass", "evidence": "Last 5 default-branch commits: 3 on 2026-09-16, 2 on
  2026-08-24 (all within 90 days of 2026-09-20)"},
        {"name": "shipped-recently", "grade": "pass", "evidence": "archived: false; pushed_at 2026-09-16T21:50:20Z, 4
  days before today"},
        {"name": "responds-to-issues", "grade": "pass", "evidence": "Aburke225 (COLLABORATOR) commented on #52 and #43
  on 2026-09-16, within 30 days"},
        {"name": "scope-fits", "grade": "pass", "evidence": "One bug with a one-line repro:
  FaithfulnessChecker().check('Knows Python.', [{'text': None}]) -> TypeError; existing test
  test_none_context_chunk_text"},
        {"name": "unclaimed", "grade": "pass", "evidence": "Assignees: none; comments: 0; repo-wide pulls list is empty
  so no linked PR"},
        {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and
  .github/PULL_REQUEST_TEMPLATE.md contain no AI mention; silence passes"}
      ],
      "verdict": "accept"
    },
    {
      "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/63",
      "checks": [
        {"name": "commits-alive", "grade": "pass", "evidence": "Last 5 default-branch commits: 3 on 2026-09-16, 2 on
  2026-08-24 (all within 90 days of 2026-09-20)"},
        {"name": "shipped-recently", "grade": "pass", "evidence": "archived: false; pushed_at 2026-09-16T21:50:20Z, 4
  days before today"},
        {"name": "responds-to-issues", "grade": "pass", "evidence": "Aburke225 (COLLABORATOR) commented on #52 and #43
  on 2026-09-16, within 30 days"},
        {"name": "scope-fits", "grade": "pass", "evidence": "One test-level mismatch: 'assert 51 > 100' in
  test_readme_with_all_quality_signals; fix is expand fixture or adjust assertion"},
        {"name": "unclaimed", "grade": "pass", "evidence": "Assignees: none; comments: 0; repo-wide pulls list is empty
  so no linked PR"},
        {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and
  .github/PULL_REQUEST_TEMPLATE.md contain no AI mention; silence passes"}
      ],
      "verdict": "accept"
    },
    {
      "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/62",
      "checks": [
        {"name": "commits-alive", "grade": "pass", "evidence": "Last 5 default-branch commits: 3 on 2026-09-16, 2 on
  2026-08-24 (all within 90 days of 2026-09-20)"},
        {"name": "shipped-recently", "grade": "pass", "evidence": "archived: false; pushed_at 2026-09-16T21:50:20Z, 4
  days before today"},
        {"name": "responds-to-issues", "grade": "pass", "evidence": "Aburke225 (COLLABORATOR) commented on #52 and #43
  on 2026-09-16, within 30 days"},
        {"name": "scope-fits", "grade": "pass", "evidence": "One bug in api/routes/health.py: probe uses
  settings.redis_host/redis_port, but Settings only defines redis_url"},
        {"name": "unclaimed", "grade": "pass", "evidence": "Assignees: none; no linked PR (repo pulls list empty); sole
  claim comment is from student skonda29 (author_association NONE), which the Path Review house rule says does not
  block"},
        {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and
  .github/PULL_REQUEST_TEMPLATE.md contain no AI mention; silence passes"}
      ],
      "verdict": "accept"
    }
  ]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

1. Smoke run (--limit 3): "agreement: 3/3 scored items"
2. First full run: "agreement: 16/20 scored items (bar: 18/20: below the bar)"
3. Revised scope-fits, re-tested 4 disputed issues (--only issue-01,issue-15,issue-19,issue-20): "agreement: 2/4 scored items"
4. Full run with revised rubric: "agreement: 16/20 scored items (bar: 18/20: below the bar)"
5. Merged fix, re-tested 6 disputed issues (--only issue-01,issue-04,issue-09,issue-15,issue-19,issue-20): "agreement: 6/6 scored items"
6. Final full run (committed): "agreement: 19/20 scored items (bar: 18/20: PASS)"
   

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

issue-19. My rubric's scope-fits check rejected issue-19 in the final
committed run ("issue-19 accept reject NO failed: scope-fits"), while
the gold label is accept. The gold note calls it a "maintainer-diagnosed
performance bug with named causes" — it's one bug (UI freezes selecting
large subgraphs) with two named root causes and a few suggested fix
approaches (multi-processing, separate threads), all serving one goal.

This is a genuinely borderline case: in an earlier smoke test with the
same rubric wording, my skill graded issue-19 accept; it flipped to
reject in the final full run with no rubric change in between. That
tells me the model's judgment of the "multiple suggested approaches
= too broad?" line is not fully stable, and my scope-fits wording,
while it names "several concrete sub-steps toward one goal" as
acceptable, doesn't explicitly address the case where the sub-steps
are alternative fix *strategies* rather than sequential implementation
steps — a distinction the model may be weighing inconsistently.


**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

scope-fits: "Serves one coherent goal (a single bug, feature, or doc
topic), even if the fix touches multiple files or has several concrete
sub-steps toward that one goal. FAILS if: the issue explicitly bundles
multiple separable features/tasks meant to be split into separate work;
it requires a codebase-wide/cross-cutting change; a maintainer states
it needs core/internal architecture changes; it is a pure usage/support
question with no actionable fix; the thread shows unresolved design
debate together with a history of closed/abandoned PR attempts and no
maintainer-settled direction; or it is a vague feature request/wish
with no concrete spec that hides an undecided design or product
decision. A checklist of concrete sub-steps toward one goal, or a terse
body, does NOT by itself fail this check."

This wording exists because my first two rubric versions each optimized
for one failure mode and broke on the other: version 1 was too strict
about multi-step issues and wrongly rejected legitimate accepts
(issue-01, issue-04, issue-09, issue-19); version 2 loosened that but
lost the ability to catch vague, undecided feature requests (issue-15,
issue-20). This version keeps the permissive "checklist toward one
goal is fine" rule from the fix that rescued the wrongly-rejected
issues, while re-adding the specific "vague request hiding an
undecided design decision" fail condition that catches the wrongly-
accepted ones.


**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

The permissive clause ("a checklist of concrete sub-steps toward one
goal does NOT by itself fail this check") is what let issue-01 (a
multi-page documentation task with several update points) and issue-19
(a bug with named causes and several suggested fix strategies) pass
instead of being wrongly rejected as "too broad." I canary-tested the
opposite risk directly with --only issue-15,issue-20: both are gold-
labeled reject for a stalled-design-debate/vague-feature-request
reason, and both correctly failed in the final run (issue-15 reject
reject yes; issue-20 reject reject yes), because the check's explicit
fail condition for "a vague feature request... that hides an undecided
design or product decision" caught them independently of the
permissive clause. The trade-off I'm accepting: an issue that quietly
bundles several individually-substantial tasks under one vaguely-
plausible-sounding goal, without tripping the "vague request" or
"design debate" language specifically, could still slip through as
accept. My rubric bets that outright vagueness or unresolved debate is
a more reliable, checkable signal than counting sub-steps.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.


**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

Answers:
1. Fit: I know Python, and issue #72 is a pure-Python fail-open vs.
fail-closed security bug in verify_password, with an existing
@pytest.mark.xfail test written to unmark once fixed. No framework
setup needed, which matches the time I have this week.

2. The verdict correctly identified that the repo is active, the issue
is unclaimed, the AI-contribution policy allows my workflow, and the
fix is a single bounded change in one file. What I weighed that the
rubric couldn't: that this issue specifically lets me practice judging
whether a security-relevant fix is actually correct rather than just
"looks right" — the pre-written failing test gives me an objective way
to check that, which is exactly the skill I said I want to build. My
rubric's fit-profile ranking pointed me here, but the "why this teaches
me what I want" reasoning is mine, not the tool's.

3. Anticipated difficulty: low to moderate. The fix itself is isolated
to core/security.py, so I don't expect environment complexity. The
main risk is making sure I understand exactly what "fail closed"
should mean for the specific hashing library in use, rather than just
wrapping the exception and calling it done.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
