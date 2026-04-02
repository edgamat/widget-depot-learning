# Claude Code Learning Log — Process Guide

This document describes how we capture, organize, and use our observations during the Claude Code learning exercise. The goal is to keep logging lightweight enough that we actually do it, while structured enough that the notes are useful when we synthesize at the midpoint and end.

---

## Wiki Structure

```
widget-depot-learning/
├── README.md                   ← this document
├── session-log.md              ← all session entries, newest first
├── patterns.md                 ← recurring observations worth tracking
└── synthesis/
    ├── phase-1-review.md      ← completed at end of Phase 1
    ├── phase-2-review.md      ← completed at end of Phase 2
    ├── ...                    ...
    └── final-review.md        ← completed at end of the final phase
```

---

## The Session Log

All entries go into `session-log.md`, newest first. One entry per session, written after the session ends.

An entry doesn't need to be long. A few honest sentences are more useful than a polished paragraph written two days later. If a session was uneventful, say so — that's data too.

### Entry Format

```
---
## YYYY-MM-DD — [Your Name] — Phase #

**Working on:** [brief description of the story or task]
**Duration:** [approximate time in session]

**What happened:**
[What you were trying to do and how it went. Be specific — vague entries
are hard to use later. If something took longer than expected, note why.
If something went surprisingly well, note that too.]

**Friction points:**
[Moments where you had to re-explain context, correct Claude's output,
or work around a limitation. Note whether each felt like a tooling gap
(something a CLAUDE.md or command might fix) or a workflow gap
(something about how you approached the session).]

**What worked well:**
[Anything Claude Code handled better than expected, or where it
genuinely saved time without special setup.]

**Questions or ideas:**
[Anything you want to discuss with other developers, or a hunch
about something worth trying.]
```

### What to Capture, What to Skip

**Worth capturing:**
- Repeated friction — if you had to do the same thing twice, write it down
- Surprises in either direction — better or worse than expected
- Moments where missing context caused Claude to go in the wrong direction
- Rough time estimates — even "this felt like it took twice as long" is useful

**Not worth capturing:**
- Every prompt and response — that level of detail won't be useful in synthesis
- Complaints without specifics — "Claude was annoying" tells us nothing
- Things you've already noted in a previous entry unless something changed

---

## The Patterns Page

`patterns.md` is where we promote observations from individual session entries into recurring themes. Either developer can add to it at any time.

An observation belongs on the patterns page when you've seen it more than once, or when the other developer has noted the same thing independently.

### Patterns Format

```
## [Short name for the pattern]

**First observed:** [date]
**Observed by:** [names]
**Phase:** [1, 2, or both]

**Description:**
[What keeps happening, with enough specificity to be actionable.]

**Possible cause:**
[Why you think this is happening — missing context, workflow habit,
tool limitation, etc.]

**Status:** [Watching | Confirmed | Addressed in Phase 2]
```

---

## Weekly Rhythm

We don't need a formal meeting cadence, but a brief check-in once a week keeps the log from going stale and surfaces patterns before they're forgotten.

A useful weekly check-in covers three things:
1. Has everyone written up their sessions from the past week?
2. Is anything from the session log ready to promote to the patterns page?
3. Is there anything one of us noticed that the other should be aware of?

This doesn't need to be long. Ten minutes is enough if the log is up to date.

---

## Midpoint Review (End of Week 5)

At the end of Phase 1, we pause and review everything before building out the Phase 2 setup. The midpoint review should answer:

- What friction points came up most often?
- Which of those are likely addressable with a CLAUDE.md file or custom commands?
- Which are workflow habits we should change?
- What worked well in Phase 1 that we want to keep?
- What do we want to deliberately test in Phase 2?

The output is a completed `synthesis/midpoint-review.md` and a working list of what we'll build before starting Phase 2.

---

## Final Review (End of Week 10)

The final review compares Phase 1 and Phase 2 and produces the team-facing best-practices guide. It should answer:

- What changed between phases, and did those changes have the effect we expected?
- Where did Claude Code genuinely improve our productivity?
- Where did it require more investment than it returned?
- What would we tell another developer on our team before they start using it?
- What setup would we recommend as a starting point for the rest of the team?

---

## A Few Principles

**Write it while it's fresh.** After-session entries work best when written the same day. Notes written two days later tend to smooth over the friction that was actually most instructive.

**Be specific about friction.** "Claude didn't understand what I wanted" is less useful than "Claude generated a component that didn't follow our naming conventions, and I had to correct it three times in the same session."

**Separate observation from conclusion.** In Phase 1 especially, try to capture what happened rather than what it means. Conclusions drawn too early can colour later observations. Save the meaning-making for the patterns page and synthesis documents.

**Both perspectives matter.** We are one shared log, but we bring different eyes to the same tool. If your experience of a session was different from what a previous entry describes, write that difference down — don't just note agreement.
