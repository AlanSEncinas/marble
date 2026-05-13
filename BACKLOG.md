# Backlog — marble

> Destination for ideas that surface during skill development but aren't in the current layer. Items get promoted to `BUILD_PLAN.md` when their phase opens. **Anything in this file is "not now."** Don't open a second front.

---

## Layer 2 — Stability & Adoption (next, items not yet promoted)

- _(promote items from below as Layer 2 work progresses)_

---

## Layer 3 — Community & Multi-Domain (later)

- **Domain variants of the skill.** A `marble-data-science` variant with routing rules for notebooks/experiments/papers. A `marble-content` variant for writers. Same core philosophy, different routing rows.
- **Marketplace submission.** When agentskills.io or similar Claude Code skill marketplaces accept submissions, package this for distribution.
- **Issue / PR templates** in `.github/`.
- **Contributing guide** explaining the test-by-pressure-scenario discipline (per `superpowers:writing-skills`).

---

## Post-Ship / Stretch

- **Auto-bootstrap helper.** A small script (PowerShell + bash) that takes a project name and generates a `BUILD_PLAN.md` + `BACKLOG.md` + `CLAUDE.md` from the templates with sensible defaults filled in (Layer 1/2/3 names, project description). Reduces friction on session 1 of a new project.
- **Pre-commit hook template.** Drop-in soft pre-commit hook (parallel to Trend Tents' drift guard) that warns when a commit touches code without updating `BUILD_PLAN.md` or `CLAUDE.md`. Could ship in a `hooks/` subdir of this repo.
- **Subagent-tested SKILL.md.** Per `superpowers:writing-skills` discipline, run baseline pressure scenarios (subagent without skill → document rationalizations → write skill counter-language → verify compliance) so the skill is bulletproof under adversarial use rather than just well-intentioned use.
- **An anti-pattern showcase.** A short page in the README showing what the skill does NOT do — e.g., it doesn't replace TDD, doesn't replace brainstorming, doesn't make decisions for you. Counters the "magic productivity skill" misread.
- **Telemetry / opt-in usage stats.** If users adopt this, rough sense of which trigger words are used most, which routes hand off most, which red flags fire. None of this is high-value enough to build now.

---

## Parked / Decided Against

> Ideas considered and explicitly chosen to skip. Keep them here so they don't keep coming back as "new" ideas. Include the reason.

- **Megaskill (squash superpowers + this into one giant SKILL.md).** Decided against on 2026-05-01 — would break upstream updates from Anthropic, balloon load tokens 5-10x, and lose the testing/maintenance leverage that comes from superpowers being a separately-maintained skill suite. The router pattern (current implementation) gives the same single-front-door feel without the cost. See conversation-1 design notes if reasoning needs revisiting.
- **Forking superpowers entirely into AlanSEncinas namespace.** Same reasoning as above — high ongoing maintenance burden, no real benefit.
- **A "morning call" Claude Code hook.** Tempting (would force the morning call to fire every session via settings.json), but hooks run regardless of context and would annoy on casual / one-off conversations. Skill-based auto-fire with the 3-case morning call (A/B/C) handles this better.
