# Marble

A Claude Code skill that keeps you on one phase instead of the whole project.

Projects start small — a marble. Then they grow into a galaxy and you lose the thread. Marble stops that. Every session stays anchored to the current phase, ideas get parked instead of chased, and the work actually ships.

---

Marble runs the session. It keeps you in the current phase, parks ideas without breaking flow, commits with discipline, and answers self-doubt with your actual numbers instead of empty validation. It also adds two things AI sessions don't have on their own: save points on disk that survive between sessions, and a memory layer that remembers you, your projects, and how you work.

The engineering work runs on the [superpowers](https://agentskills.io) skill suite. Marble is the layer on top — session structure, backlog triage, doubt interruption, and the marble-not-galaxy rule that keeps complexity from becoming paralysis.

### Who this is for

**Solo operators and small teams shipping real work** — people with actual projects (apps, ML pipelines, internal tools, businesses) who keep losing the thread to scope creep, doubt, or forgetting where they left off.

Not for: fully autonomous coding agents (marble doesn't write code, it routes you to the skills that do), big dev orgs that already have project management, or anyone looking for a kanban board (BACKLOG.md is a triage destination, not a board).

### What it does

**Today's Game Plan.** Every session opens with a quick orientation — recent shipped work in a table, plus your next action picked up verbatim from the previous session's wrap. No new work starts until that's acknowledged. Start any session by typing `hello`, `morning`, `morning [date]`, or `hi today is [date]` — any of those triggers the game plan. It's a small ritual that keeps every session oriented before work starts.

**Phase discipline.** Work splits into explicit layers with done definitions. New ideas that surface mid-session get triaged to a backlog instead of opening a second front. You stay on the current phase; the rest waits.

**Trigger-word commits.** Say "commit", "done for today", or "ship it" once. Auto-commit mode opens for the full session. Phase-prefixed messages, matching doc updates, no re-asking. The git log becomes a project narrative.

**Doubt handler.** When you say "this won't work" or "nobody cares" or "should I bother" — the skill doesn't validate you. It pulls up the actual numbers. Your model hit 0.84 mIoU. Your cost dropped from $49 to $1.67. Concrete metrics instead of empty validation, then back to the next action.

**Backlog triage.** Mid-phase idea? Acknowledged in one line, logged to BACKLOG.md, session continues. The idea doesn't disappear. The current phase doesn't either.

**Memory integration.** The skill writes durable memories about you (your role, working style, ambitions), your projects (goals, in-flight decisions, why-this-not-that), and your feedback patterns (what to avoid, what worked). Code and recent changes don't go to memory — those live in the files and in git. Memory is for what *isn't* in the files: who you are, what you're trying to do, how you want to collaborate. Sessions started months apart pick up like one continuous one.

**Session close.** Type `done for today` or `ship it` and the skill writes a state snapshot — what's pushed, what's frozen, what's blocked — plus a concrete next action for tomorrow that gets persisted into your `BUILD_PLAN.md` so the next session picks it up verbatim. The two halves of the session bookend bridge through that file. "We made good progress" is not a valid close — the next action has to be concrete.

### The save points

Memory drifts. Chat history disappears. AI sessions don't remember each other. Marble's answer is a trio of files that persist on disk between sessions — these are your save points, the project's state crystallized so the next session picks up exactly where the last one left off:

- `BUILD_PLAN.md` — forward-looking, live checkboxes by phase. The source of truth for what's done. Also carries the wrap → morning handoff line that yesterday's session writes for today's session to pick up — the literal save point that bridges sessions.
- `CLAUDE.md` — backward-looking architecture reference with a dated changelog. Updated in the same session as the change.
- `BACKLOG.md` — where ideas live when they're not in the current phase.

Open Claude Code in a new project directory and the skill notices the files are missing — it announces what it's about to do, creates the trio from the marble templates, and teaches you the session-start trigger phrases inline. No setup ceremony. Just open and go.

### Quickstart

Here's what marble looks like across two days on a real project.

**Day 1, morning.** You open Claude Code in a fresh project directory with one file in it (`idea.md` with a few sentences about what you want to build). You type:

```
hi
```

Marble fires. It notices the project files are missing and announces what it's about to do:

```
Hi — I noticed this is a new project. I don't see BUILD_PLAN.md,
BACKLOG.md, or CLAUDE.md yet, so I'm going to create them from the
marble templates.

Moving forward, you can start any session by saying any of:
- hello
- hi today is [date]
- morning [date]
- morning

Any of those triggers Today's Game Plan and gets us oriented for
the day.

Creating the files now.
```

The trio gets created. Marble routes you into `superpowers:brainstorming` to design what you're building. You spend the morning shaping the project. Your `BUILD_PLAN.md` now has Phase 1 / 2 / 3 with explicit done definitions and live checkboxes.

**Day 1, mid-session.** Working on Phase 1's first task, an idea pops up: *"oh actually, this should also export to JSON."* Without marble, you'd context-switch and start building it. With marble:

```
You: Wait, we should also support JSON export.

Claude: Good idea — logging to BACKLOG.md under Phase 3 (Export
Formats). Right now we're on Phase 1 task 2 (parse the input).
Continuing.
```

The idea doesn't disappear. The current phase doesn't either.

**Day 1, evening.** You're done for the day. You type:

```
ship it
```

Marble closes the session with a state snapshot, not a vague "good progress":

```
Session closed cleanly — 5/25/26. Final state:

| Item   | Status                                         |
|--------|------------------------------------------------|
| Branch | main @ a3f9c21, pushed                         |
| Tests  | 12 green / 0 failing                           |
| Phase  | 1 of 3 — Parse layer (2 of 4 tasks done)       |

Concrete next action for tomorrow (written down per marble
session-end ritual):

`pytest tests/test_parser.py::test_handles_multiline_input`

Good landing — got the multi-format parser working without
falling into the "what if we support YAML too" trap. Tomorrow
is just one focused test.
```

That literal next action gets persisted into `BUILD_PLAN.md` so tomorrow's session can read it back verbatim.

**Day 2, morning.** You open Claude Code, type:

```
morning
```

Marble fires Today's Game Plan and surfaces yesterday's handoff verbatim — no paraphrasing, no "let me figure out where we left off":

```
Hello — today is 5/26/26. Phase 1 — Parse layer.

| Recently shipped                              | When    |
|-----------------------------------------------|---------|
| Phase 1: multi-format parser scaffolding      | 5/25/26 |
| Phase 1: input validation + error messages    | 5/25/26 |

Today's focus:
- pytest tests/test_parser.py::test_handles_multiline_input
- (continues Phase 1 task 3; one focused test, no scope creep)
```

You pick up exactly where you left off. The two halves of the session bookend bridged through `BUILD_PLAN.md` automatically.

That's the loop. Open → orient → work → wrap → open → orient. Every session.

### Install

**As a plugin (recommended).** In Claude Code, add the marble marketplace and install:
```
/plugin marketplace add AlanSEncinas/marble
/plugin install marble@alan-encinas-plugins
```

Once marble is in Anthropic's community marketplace, you can also install it from there:
```
/plugin marketplace add anthropics/claude-plugins-community
/plugin install marble@claude-community
```

**As a bare skill (clone).** Drop it straight into your skills folder — no plugin system needed:

macOS / Linux:
```bash
cd ~/.claude/skills
git clone https://github.com/AlanSEncinas/marble.git
```

Windows (PowerShell):
```powershell
cd "$env:USERPROFILE\.claude\skills"
git clone https://github.com/AlanSEncinas/marble.git
```

Either way, restart Claude Code and marble fires on your next session.

Requires Claude Code. Pairs with the [superpowers](https://agentskills.io) plugin for the engineering handoffs — marble works standalone, but brainstorming, planning, TDD, debugging, and verification fall back to model defaults instead of the disciplined superpowers versions. Install both for the full experience.

### Adapting it

Fork it. Edit SKILL.md to match your voice, your projects, your workflow. The doubt handler examples are mine — replace them with your numbers. The routing table is opinionated — add rows for how you work. The templates are starting points. Make them yours.

### Contributing

Issues and PRs welcome. Suggest changes that solve real friction, not theoretical ones.

### License

MIT
