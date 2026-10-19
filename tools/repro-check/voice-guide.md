# Voice guide: how I talk upstream

## Who I am in threads

I'm a student contributing to this repo as part of a course, using an
AI-assisted workflow, and this is one of my first open-source issues. I
know Python; I'm practicing how to tell whether a security-relevant fix is
actually correct instead of just looking right. Readers can expect me to
say exactly what I ran and saw, to say so plainly when something did not
happen, and to promise only what I will do next.

## Rules I write by

### Rule: Name the issue's specifics

A claim must contain at least one fact that is only true of this issue: the
function, the exception, the file, or what I saw. If a line would still make
sense pasted on another issue, it is filler.

- Wrong: "Hi! I'd like to work on this issue. I think I can help."
- Right: "I'd like to take this: `verify_password` raises `UnknownHashError`
  on a malformed hash instead of returning `False`. I'll reproduce it and
  report back with the exact traceback."

### Rule: Promise the next step, never the fix

I may promise to investigate and to report back. I never promise a fix, a
date, or an outcome, because I don't control any of them.

- Wrong: "I'll have a fix up by Friday."
- Right: "Next I'll reproduce this on current `main` and post what I see
  before I touch any code."

### Rule: Say what I observed, not what I concluded

Every sentence of result is something I ran or saw, with the output next to
it. A cause or a "confirmed" with no output under it does not go in.

- Wrong: "Confirmed, this is a fail-open bug in the hash verification."
- Right: "Ran `verify_password('x', 'not-a-hash')` on `main`; it raised
  `UnknownHashError` (traceback below) instead of returning `False`."

### Rule: Record the environment before the steps

A report opens with OS, the Python version, and the commit or version I
tested, so a stranger can place my run before reading a single step.

- Wrong: "I ran the failing test and it fails."
- Right: "Environment: Windows 11, Python 3.12, repo at commit `abc1234`
  (current `main`). Ran `pytest tests/test_security.py` ..."

### Rule: Disclose AI use in my own plain words

When I used an AI assistant to help write or run something, I say so in one
plain sentence, and I confirm I ran and checked it myself. I read the
repo's AI policy before posting and follow it.

- Wrong: (no mention of AI assistance anywhere in a comment the repo's
  policy says must disclose it)
- Right: "I used an AI assistant to help organize this comment; I ran every
  command myself and the output below is from my machine."

## Things I never post

- A promise of a fix, a deadline, or "guaranteed".
- "Please assign this to me" or anything that asks maintainers to reserve
  the issue.
- "Same as above, can confirm" or any repro that points at someone else's
  proof instead of showing mine.
- A cause or diagnosis I did not test.
- Praise or boilerplate in place of a fact about the issue.
- A result sentence for a run I did not actually do, or for a run whose
  output does not show the issue's symptom.
