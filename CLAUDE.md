# CLAUDE.md — marble (skill development workspace)

> Auto-loaded by Claude Code when you open a session in this directory. Distinct from any project that *uses* the skill — this is the workspace where we *develop and maintain* it. Last updated: 2026-05-12.

---

## 1. What this project is

This is the development repo for the **marble** Claude Code skill (formerly `phase-driven-shipping`). The skill itself is a universal entry-point/router that delegates engineering work to the [superpowers](https://agentskills.io) suite while owning session bookends, commit triggers, idea triage, doubt handling, and same-session doc updates.

**Purpose of THIS project:**
- Maintain and improve `SKILL.md`, the templates, and the README
- Track issues, fixes, and feature ideas for the skill
- Ship updates to the GitHub repo at github.com/AlanSEncinas/marble (currently private — going public when polish is complete)

**NOT the purpose:**
- Using the skill on a real product (that's what the skill enables, not what this project does)
- Documenting Trend Tents / Albert (that's at `trend-tents-orchestrator/CLAUDE.md`)

---

## 2. Path map (important — easy to confuse)

| Path | Role |
|------|------|
| `C:\Users\encin\.claude\skills\marble\` | **This directory.** It IS three things at once: the dev workspace, the local install Claude Code reads at session start, AND the git working copy of the GitHub remote. |
| `https://github.com/AlanSEncinas/marble` | Canonical GitHub repo (currently private). `git push` from here updates it. |
| Any other project on this machine (e.g. TT orchestrator) | The skill auto-fires there when triggered, but those projects are NOT the dev workspace. Skill edits made elsewhere wouldn't load. |

The key insight: edits made here are *immediately live* (Claude Code reads SKILL.md from this exact path on session start). No copy/sync step. After a session restart, your new skill version is what fires.

---

## 3. How to test changes

1. Edit `SKILL.md` (or templates) in this directory
2. **Close Claude Code completely** (the skill registry is read at session start — running sessions cache the old version)
3. Open Claude Code in any test directory (often best to open a fresh empty folder so case B/C of the morning call gets exercised)
4. Send an opening message and observe whether the skill fires
5. If it fires correctly → commit + push. If not → diagnose, edit, re-test.

**Red flag:** If `SKILL.md` was edited but the old version is still firing, you forgot to fully restart Claude Code. The hot-reload path doesn't pick up frontmatter changes.

---

## 4. How the skill works (one-paragraph refresher)

The skill is auto-discovered by Claude Code via its description — it lists "Use when..." triggering conditions. When the model sees a matching condition (session start, trigger words, mid-phase ideas, doubt language, session end), it invokes the skill via the `Skill` tool, loads the body, and follows the rules. The body has a routing table that hands off engineering work to the right superpowers skill (brainstorming, TDD, debugging, verification, etc.). The three rules the skill owns directly: morning call (session bookend), idea triage (BACKLOG), commit discipline (phase-prefixed messages, same-session doc updates).

---

## 5. Recently shipped

**2026-05-12 — `Layer 2 rebrand`: phase-driven-shipping → marble**
- Renamed the skill from `phase-driven-shipping` to `marble`. Identity rebrand around the "marble vs galaxy" metaphor: every session anchored to one phase (the marble) rather than the full project (the galaxy), so complexity doesn't become paralysis.
- SKILL.md frontmatter (`name: marble`) and heading updated. No behavioral rules changed — routing table, morning call, doubt handler, commit discipline all identical.
- README.md fully rewritten: story-first ("builders who spiral"), personal context (solo operator, 14 markets), feature descriptions in plain language. Replaces the previous philosophy-first version.
- All internal references in CLAUDE.md / BUILD_PLAN.md / BACKLOG.md updated.
- Drafts of a website blog post ("I Built a Dev Skill to Stop My Own Brain from Sabotaging My Work") and a LinkedIn announcement exist outside this repo — not active yet, holding until public re-launch is ready.
- Pending user actions after this commit: close Claude Code, rename local directory `phase-driven-shipping\` → `marble\`, rename GitHub repo to `marble`, run `git remote set-url origin https://github.com/AlanSEncinas/marble.git`, reopen Claude Code, verify the renamed skill fires.

**2026-05-12 — `Layer 1 verified`: auto-fire confirmed in fresh project**
- User opened Claude Code in a clean `Starmap/` directory with only an empty `idea` file. The skill fired correctly and routed to Case B of the morning call (no `BUILD_PLAN.md` + real-project intent → hand off to `superpowers:brainstorming` before scaffolding). This closes the open verification item from the `db092b8` description fix. Layer 1 is fully shipped.

**2026-05-01 — `Layer 2 setup`: project meta-files for skill development workspace** (`6c39a77`)
- Added `CLAUDE.md`, `BUILD_PLAN.md`, `BACKLOG.md` to this dev workspace so the skill eats its own dogfood — the repo that maintains the skill follows the discipline the skill prescribes.

**2026-05-01 — `Layer 1 fix`: tighten skill description for reliable auto-fire** (`db092b8`)
- Real-world test in a fresh project showed `superpowers:using-superpowers` fired but `phase-driven-shipping` did not — the description was too soft.
- Description now uses "REQUIRED to invoke before any other response, including clarifying questions" — matching the authority level of `superpowers:using-superpowers` so the model treats it as priority-1.
- Trigger broadened from "any work session" → "any conversation" so it fires regardless of how the user opens.
- Morning-call body restructured into 3 cases (A: BUILD_PLAN.md exists → full call; B: no plan, real project → bootstrap proposal; C: no plan, casual question → brief acknowledgment, don't block).

**2026-05-01 — `Layer 1 polish`: fix README install URLs (encinas88 → AlanSEncinas)** (`2913e9b`)
- Initial README used the local git config username (`encinas88`) instead of the actual GitHub username (`AlanSEncinas`). Install commands updated.

**2026-05-01 — `Layer 1 init`: phase-driven-shipping skill v1** (`20f4708`)
- First public release. SKILL.md (routing table + rules + red flags), BUILD_PLAN.template.md, BACKLOG.template.md, README.md (philosophy + install), LICENSE (MIT). Pushed to https://github.com/AlanSEncinas/phase-driven-shipping (later renamed to `marble`).

---

## 6. Known issues / current concerns

- **No automated test suite** — testing is still manual ("close Claude Code, open in fresh dir, observe"). The `superpowers:writing-skills` skill prescribes baseline-pressure-scenario testing with subagents, which we have not yet done. The rebrand was a pure rename (no behavioral rule changes), so the existing rules remain untested under adversarial pressure. Promote to Layer 2 BUILD_PLAN if we want this skill bulletproof rather than just well-intentioned.
- **Description vs `superpowers:using-superpowers` overlap** — both say "REQUIRED to invoke on any conversation start." That's intentional (we want both to fire) but may cause confusion or one to suppress the other on cold loads. Starmap test confirmed both fire correctly in at least one scenario; watch for regressions on different conversation openings.
- **Repo currently private** — install commands in README point to `github.com/AlanSEncinas/marble` which won't resolve for anyone but Alan until the repo is flipped public. Acceptable while polishing, but the README is written for a public audience — don't share install instructions externally until the repo is public.

---

## 7. CLAUDE.md maintenance protocol (this file)

Same rule as the skill prescribes for every project: any change to the skill itself (SKILL.md, templates, README) → add a dated entry to §5 in the same session as the change. Don't let this drift.
