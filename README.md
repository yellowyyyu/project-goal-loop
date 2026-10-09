# Project Goal Loop

A "thinking partner" skill for **Claude Code** and **Codex**. Instead of acting as a silent
implementation worker, the agent keeps the whole project visible — where it came from, where it
stands, and what happens next — and never lets a long project degrade into a chronological pile
of disconnected status reports.

## What it does

The skill has two entry modes and chooses one before doing anything else.

- **New project — plan backwards.** Starting from the final deliverable (paper, dataset, model,
  API, working feature), the agent derives the route backwards: what evidence each claim needs,
  which experiments or implementations produce that evidence, and which risks to test first. The
  result is a small phased blueprint, executed one gated phase at a time.
- **Project already in progress — reconstruct the chain.** The agent surveys the existing reports,
  data inventories, logs, and code, rebuilds the few big stages that produce the final deliverable,
  places every existing piece of work under the stage it serves (never in date order), locates the
  current stage, and presents a takeover report — then deliberately stops and waits for your
  confirmation before doing any execution work.

## The path diagram

Every report starts with a short vertical diagram: one stage per line, top to bottom, joined by
`↓`. A big stage may list its sub-steps indented directly below it. Each item carries a mark:

| Mark | Meaning |
| --- | --- |
| ✓ | finished |
| ● | current stage ("you are here") |
| ○ | not started |
| ✗ | denied or abandoned (kept in place) |

```text
✓ data collection
   ✓ manual collection
   ✓ programmatic collection
↓
● model training (you are here)
   ✓ data cleaning
   ✗ method B (denied)
   ● parameter tuning
↓
○ evaluation
↓
○ delivery
```

The diagram is **append-only**: once an item has been shown it is never removed, and a denied or
abandoned item stays in place marked ✗, because deleting it would hide the project's history. The
diagram is refreshed only when the user explicitly asks. Stage names use your own language and
your own vocabulary.

## Report format

Every delivery or progress update is exactly three parts, and nothing else:

```text
<path diagram>
Done: <one short summary of the work completed>
Next: <one short line: what happens next, or the decision needed from you>
```

No explanations, no reminders, no closing pleasantries — extra detail is given only when asked.

## Install

**Claude Code** — clone into your personal skills directory:

```bash
git clone https://github.com/yellowyyyu/project-goal-loop.git ~/.claude/skills/project-goal-loop
```

**Codex** — clone into the Codex skills directory:

```bash
git clone https://github.com/yellowyyyu/project-goal-loop.git ~/.codex/skills/project-goal-loop
```

Both agents read `SKILL.md`; `agents/openai.yaml` supplies the Codex interface metadata (display
name, short description, default prompt).

On Windows, `~/.claude/skills/` is `%USERPROFILE%\.claude\skills\` and `~/.codex/skills/` is
`%USERPROFILE%\.codex\skills\`.

## Usage

Just work on a multi-step project as usual; the skill activates for experiments, research,
refactoring, debugging, and any work that spans sessions. In Codex you can also invoke it
explicitly with `$project-goal-loop`. It is not intended for one-shot answers or tiny edits.

## License

MIT — see [LICENSE](./LICENSE).
