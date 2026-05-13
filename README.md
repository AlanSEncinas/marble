# Marble

A Claude Code skill for builders who spiral.

You know the feeling. You start with a marble — small, clear, you can see every angle of it. You're excited. Then it grows. More context, more edge cases, more possibilities. It becomes a galaxy. And suddenly you can't hold the full shape of it anymore. The momentum dies. The doubt moves in. Somewhere between the marble and the galaxy, you stop.

I built this skill because I was the problem I kept running into.

I'm a solo operator running an international manufacturing company across 14 markets. I build real things alongside that — multi-agent sales systems, mobile apps, ML pipelines. But I kept hitting the same wall: get deep enough into a project, lose the thread, spiral into "is this even worth it," and stall out. The work was real. The self-doubt wasn't. I just couldn't tell the difference in the moment.

So I built a skill that could.

---

**Marble** is a universal Claude Code skill that acts as a conductor for your development sessions. It keeps you in the current phase, captures ideas without breaking flow, commits with discipline, and counters self-doubt with actual project metrics instead of empty validation.

It builds on the [superpowers](https://agentskills.io) skill suite for the engineering work and adds the human layer on top: the session structure, the backlog triage, the doubt interruption, and the marble-not-galaxy discipline that keeps complexity from becoming paralysis.

### What it does

**Today's Game Plan.** Every session opens with three lines: where you are, what shipped last, what's next. No new work starts until that's acknowledged. It sounds simple. It changes everything.

**Phase discipline.** Work splits into explicit layers with done definitions. New ideas that surface mid-session get triaged to a backlog instead of opening a second front. You stay on the marble. The galaxy waits.

**Trigger-word commits.** Say "commit", "done for today", or "ship it" once. Auto-commit mode opens for the full session. Phase-prefixed messages, matching doc updates, no re-asking. The git log becomes a project narrative.

**Doubt handler.** When you say "this won't work" or "nobody cares" or "should I bother" — the skill doesn't validate you. It pulls up the actual numbers. Your model hit 0.84 mIoU. Your cost dropped from $49 to $1.67. The work is real. Keep going.

**Backlog triage.** Mid-phase idea? Acknowledged in one line, logged to BACKLOG.md, session continues. The idea doesn't disappear. The current phase doesn't either.

**Session close.** Every session ends with one concrete next action written down. "We made good progress" is not a valid close. Ambiguity feeds doubt.

### The three files

Every project gets a trio:

- `BUILD_PLAN.md` — forward-looking, live checkboxes by phase. The source of truth for what's done.
- `CLAUDE.md` — backward-looking architecture reference with a dated changelog. Updated in the same session as the change.
- `BACKLOG.md` — where ideas live when they're not in the current phase.

Memory fails. Chat history disappears. The files don't.

### Install

**macOS / Linux:**
```bash
cd ~/.claude/skills
git clone https://github.com/AlanSEncinas/marble.git
```

**Windows (PowerShell):**
```powershell
cd "$env:USERPROFILE\.claude\skills"
git clone https://github.com/AlanSEncinas/marble.git
```

Requires Claude Code and the [superpowers](https://agentskills.io) plugin for the engineering handoffs.

### Adapting it

Fork it. Edit SKILL.md to match your voice, your projects, your spiral patterns. The doubt handler examples are mine — replace them with your numbers. The routing table is opinionated — add rows for your workflow. The templates are starting points. Make them yours.

### Contributing

Issues and PRs welcome. Suggest changes that solve real friction, not theoretical ones.

### License

MIT
