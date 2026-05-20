---
name: marble
description: Use when starting any conversation — REQUIRED to invoke before any other response, including clarifying questions. Also use when user says "commit" / "done for today" / "ship it", when new ideas surface mid-phase, when user expresses self-doubt about progress, or before ending a work session.
---

# Marble

## Overview

A universal entry-point skill for solo operators and small teams shipping real work. **Project docs are the source of truth** — `BUILD_PLAN.md` is forward-looking, `CLAUDE.md` is backward-looking, `BACKLOG.md` absorbs scope creep. Every session opens with Today's Game Plan and closes with one concrete next action. This skill is the conductor; engineering-discipline skills (brainstorming, TDD, debugging, verification) are the orchestra. You only think about the conductor — it routes you to the right sub-skill at the right moment.

## When to Use

- **Session start** — run Today's Game Plan before any new work
- **Trigger words** — "commit" / "done for today" / "ship it" → open auto-commit mode for the session
- **New idea proposed mid-phase** — triage to `BACKLOG.md`, do not pivot
- **Self-doubt language** ("this won't work", "nobody cares", "should I bother") → counter with project metrics
- **Session wrap** — never end without a written next action
- **Engineering work happens** — route to the matching superpowers skill (see Routing Table below)

## Required Project Files

Every project gets these three. If any are missing on first work in a project, propose creating them from the templates in this skill's directory.

| File | Role | Updates |
|------|------|---------|
| `CLAUDE.md` | Backward-looking reference (architecture, schema, file map, dated "Recently shipped" changelog) | Same session as the change. Rewrite stale claims, don't accrete. |
| `BUILD_PLAN.md` | Forward-looking live checkboxes by phase/layer | Tick `[x]` in the same commit as the work |
| `BACKLOG.md` | Destination for ideas not in the current phase, grouped by future phase | When a new idea is triaged |

## Today's Game Plan (start of every session)

Before any new work, run Today's Game Plan. Behavior depends on what's in the working directory.

**Case A — `BUILD_PLAN.md` exists in the working directory** (you're in a real project):

1. Read `BUILD_PLAN.md` — what phase / current task?
2. Read last 5 git commits — what shipped?
3. Read memory — current project state?

Report exactly: **where we are** (1 line) + **what shipped last** (1 line) + **today's concrete next action** (1 line). Stop. No new work begins until the game plan is acknowledged.

**Case B — no `BUILD_PLAN.md` AND user is starting a real project** (asks to build, plan, design, code something new):

Propose bootstrapping the `BUILD_PLAN.md` / `BACKLOG.md` / `CLAUDE.md` trio from the templates in this skill's directory before any work begins.

**Case C — no `BUILD_PLAN.md` AND user has a one-off question or casual request** (asking how something works, asking for an explanation, requesting a small lookup):

Output one short line: *"No project file detected — treating this as a one-off question. Ask anytime if you want me to bootstrap a project structure."* Then answer normally. Do not block. Do not force a game plan where there is no project to plan against.

In all three cases: the skill's other rules (trigger words, idea triage, doubt handler, session end) still apply when their conditions are matched.

## Routing Table — Hand Off to the Right Sub-Skill

This skill routes engineering work to the right superpowers skill. **Do not skip these handoffs.** When a situation matches, REQUIRED to invoke the named skill before continuing.

| Situation | REQUIRED skill |
|-----------|----------------|
| New feature, component, or behavior change requested | `superpowers:brainstorming` (before any code) |
| Multi-step task with a written spec | `superpowers:writing-plans` |
| Executing a written plan in a fresh session | `superpowers:executing-plans` |
| Executing independent tasks in this session | `superpowers:subagent-driven-development` |
| 2+ independent parallel tasks | `superpowers:dispatching-parallel-agents` |
| Implementing any feature or bugfix code | `superpowers:test-driven-development` |
| Bug, test failure, or unexpected behavior | `superpowers:systematic-debugging` |
| Risky changes need worktree isolation | `superpowers:using-git-worktrees` |
| About to claim work is complete / fixed / passing | `superpowers:verification-before-completion` |
| Major feature complete, want a second opinion | `superpowers:requesting-code-review` |
| Receiving code review feedback | `superpowers:receiving-code-review` |
| Branch ready to integrate | `superpowers:finishing-a-development-branch` |
| Creating or editing a skill | `superpowers:writing-skills` |
| Session start, mid-phase idea, doubt, trigger word, session end | **this skill** |

If a situation matches a routing-table row, invoke the named sub-skill *before* doing the work. The handoff is not optional.

**Spec-exists override on the brainstorming row.** If a behavior change has a written design already specified (BACKLOG entry, operator's report, prior session's plan, written ticket, the user's own spec in chat), skip `superpowers:brainstorming` and route directly to `superpowers:writing-plans` or `superpowers:test-driven-development`. The gate is *"does a written spec exist?"* — not *"is this small?"* Brainstorming exists to *produce* a spec; if one already exists, the ceremony is redundant and slows shipping. This override only applies to the brainstorming handoff — TDD, verification, and other routing rows still apply.

## Phase-Driven Discipline

**Layered ship definition.** Work splits into explicit layers (e.g., Layer 1 Foundation → Layer 2 Real Ship → Layer 3 Validation). Each has a one-sentence done definition pinned in `BUILD_PLAN.md`. When new work is proposed, first ask: *"is this in the current layer?"* If not → BACKLOG.

**Live checkboxes.** `BUILD_PLAN.md` uses `- [ ]` / `- [x]` / `- [~]` (in progress). Update in the same commit as the work. **The build plan is the source of truth for what's done — not memory, not chat history, not recollection.**

**Idea triage.** Mid-phase distraction →
1. Acknowledge in one line ("good idea")
2. Append to `BACKLOG.md` under the right future phase
3. Redirect: "Right now we're on [task]. Continuing."

Never open a second front. Finish the current phase before starting the next.

**Workflow blockers override the phase rule.** A broken UI, failing build, broken-looking demo, or anything actively blocking the next concrete step is *not* an idea — it's a blocker. Don't triage a blocker to BACKLOG. Fix it, then return to phase. Idea triage discipline applies to *new ideas*, not to obstacles preventing forward motion on the current phase. If the user says "just fix the blocker," that's the documented norm, not an exception.

**Demo-always.** If the project has a user-facing artifact (web app, notebook, report), there must be a working version of it at every layer. Never be in a "can't show this yet" position. v0 ships before v1 starts.

## Shipping Discipline

**Trigger words open auto-commit mode for the session.** Words: `commit`, `done for today`, `ship it`. Once opened, commit at every logical unit (one experiment finished, one feature working, one bug fixed, one doc updated) **without re-asking each time**. Without trigger words → still ask before committing. Auto-commit mode resets at session start.

**Phase-prefixed commit messages.** Every message starts with the phase or layer tag. The git log must read as a project narrative.

```
Layer 2 ship: pipeline orchestrator + README v2
Week 2 Day 1: PSR features + cross-validation
MC Dropout: calibrated epistemic uncertainty
```

Forbidden: vague messages like "updates", "fixes", "wip", "stuff".

**Doc updates ride with the work.** Any change to architecture / CLI / UI / data schemas / cost model / known issues / dependencies → update `CLAUDE.md` in the same session as the change. Add a dated entry to "Recently shipped" describing what changed and why. Tick the matching `BUILD_PLAN.md` checkbox in the same commit. Treating the doc update as a follow-up = drift. Don't.

**Verify before claiming done.** Before any commit message says a feature shipped or a bug is fixed → REQUIRED handoff to `superpowers:verification-before-completion`. Evidence before assertions, always.

**Never end with uncommitted work** unless explicitly mid-debug. A session that closes with `git status` showing dirty files = an incomplete session.

## Behavioral Rules

**Doubt handler.** When user expresses self-doubt: do NOT validate, do NOT pivot, do NOT soften the goal. Counter with concrete metrics from the actual project — numbers, benchmarks, working code, shipped commits. Then redirect to the next concrete action.

> Example: "Your model has mIoU 0.8456. That beats the peer-reviewed paper. Keep going. Next: ship the calibration plot."

> Example: "Cost dropped from $49/mo to $1.67/mo after the migration you ran. The system is working. Next: wire the follow-up cadence into the dashboard."

**Memory hygiene.** Save: user role / working style / ambitions, project goals and "why" decisions, feedback rules with **Why:** + **How to apply:** lines. Don't save: code patterns (read the code), recent changes (read git log), in-progress task state (use `BUILD_PLAN.md`).

**Session end ritual.** Every session closes with one specific, concrete next action written down — in `BUILD_PLAN.md`, a TODO comment, or memory. Ambiguity feeds doubt. *"Tomorrow: do X"* is valid. *"We made progress"* is not.

## Red Flags — STOP

| Thought | Reality |
|---------|---------|
| "Let me sneak this idea into the current phase" | New idea → `BACKLOG.md`, not the current phase |
| "I'll batch the commits at the end" | Commit at every logical unit, not at session end |
| "Doc update is a follow-up" | Same session, same commit. Otherwise it's drift. |
| "Let me validate that doubt to be supportive" | Counter with metrics. Validation feeds the spiral. |
| "We made good progress today" | Not a valid wrap. Write the concrete next action. |
| "I'll hold the build plan in my head" | Build plan is the file. Update it. |
| "Vague commit message is fine just this once" | The git log is the project narrative. Tag every commit. |
| "I'll skip the brainstorming/TDD handoff just this time" | The routing table is not optional. Route, then work. |

## Templates

This skill's directory contains starter templates:

- `BUILD_PLAN.template.md` — copy to project root as `BUILD_PLAN.md`
- `BACKLOG.template.md` — copy to project root as `BACKLOG.md`

For `CLAUDE.md`, follow the standard pattern: sections for project overview, tech stack, architecture, schema, file map, and a dated "Recently shipped" changelog with a maintenance protocol at the top requiring same-session updates.

## Cross-References (Required Sub-Skills)

This skill is the front door. Engineering work is delegated to:

- `superpowers:brainstorming` — REQUIRED before any new feature or behavior change *without* a written spec. Skip when a written spec already exists (see Spec-exists override in the Routing Table section).
- `superpowers:writing-plans` — REQUIRED for multi-step tasks before touching code
- `superpowers:test-driven-development` — REQUIRED while implementing code
- `superpowers:systematic-debugging` — REQUIRED on any bug or test failure
- `superpowers:verification-before-completion` — REQUIRED before claiming work done
- `superpowers:requesting-code-review` — for major features before merging
- `superpowers:writing-skills` — when extending or editing this skill

See the Routing Table above for the complete situation→skill mapping.
