# Phase 3 Workflow Upgrades — Implementation Handoff

This document hands off a planning conversation to Claude Code for implementation.
The goal is to add three skills and supporting standards documents to this
repository to improve the user-story refinement and GitHub issue creation workflow.

**Scope of this handoff:** items 1, 2, and 3 from the original phase-3 plan. Items
4 (`/address-pr`) and 5 (Playwright integration tests) are out of scope here and
will be tackled separately.

## How to use this document

Read this whole document before making any changes. Then:

1. Confirm the build order with the user.
2. Start with **Phase A** (the `issue-splitting.md` standards doc). Do not skip ahead.
3. After each phase, stop and let the user try it on a real milestone before
   moving to the next phase.
4. When in doubt about a heuristic, decision, or format choice, **ask the user**.
   Do not invent conventions silently.

This is a tools-for-the-user project, not a build-the-spec project. The user's
judgment supersedes anything written here.

---

## Background — original requirements

The user has an existing workflow:

- `/docs/business-requirements.md` and `/docs/prd.md` define goals, scope, milestones.
- For each milestone, user stories live as markdown files under
  `/docs/milestone-NN/NN-slug.md`.
- Stories are refined one milestone at a time.
- Once refined, stories are pushed to GitHub as issues, which the agent then
  works against.

Three friction points to address:

1. **Generating better stories.** No structured way to reach shared understanding
   with the agent on what a story should contain. Want the agent to "grill" the
   user to surface gaps in requirements and acceptance criteria, while preventing
   stories from ballooning.

2. **Generating milestones/stories in GitHub.** Currently ad-hoc. Want a
   repeatable command that copies story markdown to GitHub issues and links them
   as sub-issues of a milestone issue.

3. **More predictable issue creation.** "Drift" happens when the agent copies
   markdown to GitHub — content gets paraphrased, dropped, or invented. Also,
   one story sometimes needs to become multiple issues (e.g., DB migration
   separate from app code, backend separate from frontend) and the splitting
   heuristics need to be encoded.

## Decisions already made

The user and Claude (via the conversation that produced this handoff) agreed on
these points. Treat them as fixed unless the user explicitly revisits them.

- **Markdown stays user-focused; GitHub holds the task split.** When a story is
  split into multiple GitHub issues, the markdown file remains a single
  user-facing story. The split lives only in GitHub as task sub-issues of the
  story issue.
- **Grilling order is fixed.** Scope boundaries → acceptance criteria → edge
  cases. In that order, one section at a time.
- **Drift prevention is by automated check.** After creating a GitHub issue,
  fetch it back and compare the body against the source markdown. Fail loudly
  on mismatch. Do not let the agent "fix" the mismatch automatically.
- **The user already has a user-stories standards doc** in the repo. The new
  skills should reference it, not replace it. Confirm its location with the
  user before writing skills that depend on it.
- **Milestones contain fewer than 12 stories**, typically. Pace the interview
  accordingly.
- **The "plan" output of `/refine-milestone` is more than titles + one-liners,
  but not fully fleshed out.** Roughly: title, 2–3 sentence summary, user value
  per story.
- **GitHub linking uses native sub-issues.** Not task lists, not labels.

## File structure to add

```
/docs/standards/
  user-stories.md          (already exists — confirm path with user)
  issue-splitting.md       (NEW — Phase A)
  milestone-workflow.md    (NEW — short overview of the 3-skill pipeline)

/.claude/skills/
  refine-milestone/SKILL.md      (NEW — Phase B)
  share-milestone/SKILL.md       (NEW — Phase C)
  refine-story/SKILL.md          (NEW — Phase D)
```

Skills in Claude Code live as markdown files in `.claude/skills/{skill-name}/SKILL.md`. The
folder name becomes the skill name. `$ARGUMENTS` substitutes positional args.
Verify this is still accurate against current Claude Code docs before building.

## Build order — four phases

Each phase produces something usable on its own. Stop at the end of each phase
and let the user exercise it on a real milestone before continuing.

### Phase A — `issue-splitting.md` standards doc

Write this **before any skills**. It is the document `/refine-story` will
reference, and writing it forces the heuristics to be articulated.

Contents to include:

- A short statement of when to split vs. keep as one issue.
- A decision checklist the agent walks in order. Suggested heuristics, to be
  refined with the user:
  - Schema change required → propose splitting migration into its own issue.
  - Spans >N files across backend and frontend → propose splitting at the API
    boundary.
  - Independently deployable pieces exist → propose splitting at deploy
    boundaries.
  - Otherwise → single issue.
- 3–4 worked examples: a story, the proposed split, the reasoning.
- 2–3 anti-examples: stories that *look* splittable but shouldn't be. These
  matter more than positive examples.

Ask the user for their splitting heuristics before writing. The list above is a
starting point, not a spec.

### Phase B — `/refine-milestone {N}`

A three-phase skill with explicit handoffs between phases.

1. **Plan phase.**
   - Read `/docs/prd.md` and the milestone-N section.
   - Read `/docs/standards/user-stories.md`.
   - Propose a list of stories. For each: title, 2–3 sentence summary, user
     value.
   - Stop. Wait for user approval. User may edit, add, remove, reorder.

2. **Interview phase.** For each approved story, walk the checklist in fixed
   order:
   - Scope boundaries (what's in, what's out).
   - Acceptance criteria (how do we know it's done, in testable terms).
   - Edge cases and error handling.

   One section at a time. Provide an escape hatch — a phrase like "move on" or
   "skip" that ends the interview for the current story. Track which stories
   have been interviewed so the skill can resume across sessions.

3. **Draft phase.** Write each story to `/docs/milestone-N/NN-slug.md` using
   the format from the user-stories standards doc. Add frontmatter:
   ```yaml
   ---
   status: draft
   milestone: N
   github_issue:
   task_issues: []
   ---
   ```
   Append a `## Refinement Notes` section capturing the key decisions from the
   interview (not a transcript — the decisions).

**Watch out for:** the interview becoming a chore. Be ruthless about cutting
questions that don't surface anything useful. The user has explicit permission
to skip ahead at any time.

### Phase C — `/share-milestone {N}`

Mechanical, but with strict verification.

1. Read all story files in `/docs/milestone-N/`. Refuse to proceed if:
   - Any story has `status: draft` (user must mark them ready).
   - Any story already has `github_issue` set (would need an explicit
     `--update` flag, which is out of scope for v1).

2. Create the milestone issue first via `gh issue create`. Capture the issue
   number.

3. For each story file:
   - Strip the frontmatter from the markdown body.
   - Create a GitHub issue with the remaining body **verbatim**. No
     paraphrasing. No "improvements." No summaries.
   - Run `gh issue view {N} --json body` and compare the returned body to the
     source. On mismatch: abort, show the diff, do not continue. Do not "fix"
     it.
   - On match: link the issue as a native sub-issue of the milestone issue.

4. Write `github_issue: {N}` and `status: shared` back to each story's
   frontmatter.

5. Print a summary: milestone issue URL, story issue URLs, suggested next step.

**Sub-issue mechanics:** GitHub native sub-issues may require `gh api graphql`
rather than a first-class `gh` flag. Verify the current state of `gh` before
writing the skill. If a flag exists, use it. If not, embed the exact GraphQL
mutation in the skill file so the agent doesn't improvise.

**Watch out for:** the verification step being skipped. Make failures loud and
unmissable. The whole point of this skill is preventing drift.

### Phase D — `/refine-story {M} {S}`

Run after a story is shared, when implementation is about to start and the
story may need to become multiple task issues.

1. Read `/docs/milestone-M/SS-*.md` and the corresponding GitHub issue.
2. Read `/docs/standards/issue-splitting.md`.
3. Walk the decision checklist. Surface each heuristic that triggers and each
   that doesn't, briefly, so the user can see the reasoning.
4. Propose either no-split or a specific split (task titles + 2–3 sentence
   descriptions each). Wait for approval. User may edit anything.
5. On approval: create each task issue as a native sub-issue of the **story**
   issue (not the milestone).
6. **Coverage check:** verify the union of task descriptions mentions every
   acceptance criterion in the story. If any criterion isn't covered, flag it
   and stop. Do not auto-fix.
7. Update the story file's frontmatter `task_issues` list with the new issue
   numbers.

**Watch out for:** drift moving down a layer. The split tasks together must
still cover the story; verify it programmatically, not by vibe.

## Cross-cutting concerns

- **Frontmatter schema (v1):** `status` (draft|ready|shared|split),
  `github_issue`, `task_issues`, `milestone`. Keep it minimal. Adding fields
  later is easy; removing them is not.
- **Re-running skills:** v1 refuses to overwrite. Each skill should detect
  the conflict and tell the user exactly what flag will be needed in a future
  version. Don't build the `--update` paths now.
- **End-of-skill summary:** every skill ends by stating what changed,
  what the current state is, and what the suggested next step is. The user
  works across many milestones; don't make them reconstruct context.
- **The standards docs are where judgment lives.** The skills should be
  thin orchestration. If a skill is getting long and prescriptive, move
  the prescription into a standards doc.

## What to do first

1. Read this whole document.
2. Confirm with the user:
   - The path of the existing user-stories standards doc.
   - Whether `/docs/standards/` is the right home for the new docs.
   - Whether `.claude/skills/` is where skills live in their setup.
   - The splitting heuristics for Phase A — is the starter list above
     accurate, or do they have different/additional rules?
3. Begin Phase A: draft `issue-splitting.md`. Show it to the user. Iterate.
4. Stop. Let the user use it (mentally, or by referencing it in a normal
   chat) before moving to Phase B.

Do not build all four phases in one go. Each phase is a checkpoint.
