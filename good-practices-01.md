# Good Practices - 01

Distilled from the widget-depot session log (Phases 1–3). Personal notes; each
practice pairs the general principle with the concrete moment in this project
that taught it.

---

## 1. Write directives, not suggestions

"refer to X" is read as optional. "you MUST read and follow X before starting"
is read as binding. The same instruction in two voices produces two different
behaviors.

**Where this showed up:** On 2026-04-29, the github-workflow doc was referenced
from CLAUDE.md as `refer to [github-workflow](...)`. CC treated it as a hint
and ignored the `gh` command guidance for two sessions. Changing the wording
to `When working on a GitHub issue, you MUST read and follow [github-workflow]
before starting.` made it stick.

**How to apply:** For any rule you actually need followed, use imperative
language ("you MUST", "before any Edit or Write tool call", "stop and..."). Save
softer wording for genuine suggestions.

---

## 2. Layer context: CLAUDE.md → standards docs → skills

Three layers, each with a different job:

- **CLAUDE.md** — always loaded. Keep it short: the non-negotiables, the
  pointers, the invariants. Everything in here costs context on every turn.
- **/docs/standards/*** — progressive disclosure. Pulled in only when the
  relevant work needs it (architecture, testing, github-workflow, etc.).
- **.claude/skills/*** — callable, repeatable workflows. `/address-pr`,
  `/refine-story`, `/refine-milestone`, `/share-milestone`.

**Where this showed up:** The project evolved into this shape over three
phases. End of Phase 1 (2026-04-11): moved standards out of CLAUDE.md into
`/docs/standards/`. Phase 3 (2026-05-02 onward): introduced custom skills for
the workflows that were being re-prompted every session.

**How to apply:** On the next project, start with this shape rather than
discovering it. Treat any prompt you've typed twice as a candidate skill.

---

## 3. Hard-code invariants the agent keeps re-deriving

If CC has to scan the repo or run a command every turn to learn something that
never changes, write it down. This saves tokens *and* kills brittle discovery
paths.

**Where this showed up:**
- Repo name: CC kept trying `git remote get-url origin` and parsing the result.
  Replacing that with the literal `edgamat/widget-depot` in CLAUDE.md (and a
  matching "never use `$(...)` substitution" rule) removed an entire class of
  drift (2026-05-17).
- Source root: CC couldn't find source on the first try because it didn't know
  everything lives under `src/`. One line in CLAUDE.md fixed it.
- Plan mode: CC was scanning the codebase before *every* plan, even for
  self-contained tasks like "break this story into issues" (2026-04-06). A
  short Plan Mode section in CLAUDE.md stopped the wasted exploration.

**How to apply:** Every time you catch CC running `git`, `gh`, or `find` to
learn something static, that's a signal to hard-code it.

---

## 4. Hooks enforce, instructions persuade

If something has to happen *every time* — formatting, linting, branch check,
re-staging — wire it as a hook in `settings.json`. Don't ask CC to remember.

**Where this showed up:** The `dotnet format && git add -u` PreToolUse hook on
`Bash(git commit*)` runs regardless of whether CC is paying attention to the
formatting rule that day. Before the hook (Phase 1), formatting drift kept
showing up in PRs. After the hook, it doesn't.

**How to apply:** Whenever you find yourself writing "always do X before Y" in
CLAUDE.md, ask whether X is mechanical enough to be a hook instead. Memory and
prompts drift; hooks don't.

---

## 5. Caution — keep a per-session log, and check `~/.claude` when CC defies you

The session log is the meta-practice that surfaced 1–4. Recording duration,
token %, friction, and what surprised you each session is the only way to
notice patterns across sessions.

Two specific traps the log caught that would otherwise be invisible:

- **Hidden memory overriding instructions** (2026-04-29). CC silently wrote a
  memory file in `~/.claude/projects/.../memory/` that contradicted the
  workflow doc. Updating CLAUDE.md had no effect until that memory was
  deleted. Rule of thumb: **when CC stubbornly does the wrong thing despite
  clear instructions, look in `~/.claude` before re-prompting.**
- **Quiet drift in tooling** (2026-04-26). CC gradually substituted different
  `gh` commands than the ones you'd permissioned, burning approval prompts on
  a fresh variant each session. Only visible because the friction was being
  logged.

**How to apply:** Keep the session log going. Note token % per session — it's
the cheapest signal that something is wrong with the setup.
