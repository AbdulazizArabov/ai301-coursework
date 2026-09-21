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

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

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

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
