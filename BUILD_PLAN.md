# Build Plan — marble

> Forward-looking source of truth for what ships next on the skill itself. Update checkboxes in the same commit as the work. See `CLAUDE.md` §5 for backward-looking changelog. See `BACKLOG.md` for ideas not in the current layer.

**Current phase:** Layer 2 — Stability & Adoption
**Today's next action:** Use marble across more real sessions (TT orchestrator, Starmap, any active project) before writing Quickstart copy — the canonical example transcript should be grounded in real usage patterns, not a guess. Collect notes on what feels load-bearing vs friction. Quickstart section comes after that lived-in pass.

---

## Layer 1 — Foundation (SHIPPED)

**Done when:** Public repo exists, skill installs cleanly via `git clone`, skill auto-fires on session start in a real project.

- [x] Write SKILL.md v1 (routing table, morning call, idea triage, doubt handler, commit discipline, red flags) — `20f4708`
- [x] Write BUILD_PLAN.template.md + BACKLOG.template.md — `20f4708`
- [x] Write README.md (philosophy, install, requirements) — `20f4708`
- [x] MIT LICENSE — `20f4708`
- [x] `git init` + first commit on `main` — `20f4708`
- [x] Fix README install URL (correct GitHub username) — `2913e9b`
- [x] Push to GitHub repo at github.com/AlanSEncinas/phase-driven-shipping (later renamed to `marble`) — pushed at session 1
- [x] Tighten description for reliable auto-fire — `db092b8`
- [x] **User-verified:** auto-fire works in a fresh session — confirmed 2026-05-12 via Starmap test (fired Case B, routed to brainstorming)

---

## Layer 2 — Stability & Adoption (current)

**Done when:** Skill fires reliably across cold and warm starts, has been tested by at least one user other than the author, has a clear demo/example showing the morning-call flow.

- [x] Confirm auto-fire works after the description fix (manual test by Alan) — Starmap, 2026-05-12
- [x] Rebrand: `phase-driven-shipping` → `marble` — files + directory + GitHub repo + remote all renamed; commit `1225493` (2026-05-12)
- [x] After rename: verify `marble` fires under its new name in a fresh session — confirmed 2026-05-12
- [ ] Add a "Quickstart" section to README with a real example session (operator types → skill responds with morning call → operator types "commit" → skill commits + updates docs). New README is identity/story-focused; Quickstart is the missing operational walkthrough.
- [ ] Add screenshots or a short asciinema-style transcript to README so the experience is visible before install
- [ ] Flip GitHub repo public when polish is complete
- [ ] Publish the website blog post + LinkedIn post (drafts exist outside repo, holding until public re-launch)
- [ ] Get one external user to install and run a session — collect feedback on (a) does it fire, (b) is the morning call valuable, (c) any friction points
- [ ] Address top friction point from external feedback

---

## Layer 3 — Community & Multi-Domain (later)

**Done when:** Skill is discoverable, has community input, supports more than just code projects.

- [ ] Submit to a Claude Code skill marketplace if one exists by then
- [ ] Add domain variants or routing rules for non-code work (writing, design, data analysis, content)
- [ ] Add an `examples/` folder with sample BUILD_PLAN.md / BACKLOG.md for different project types (web app, ML project, blog, ops runbook)
- [ ] Set up an issue template / contribution guide
- [ ] Write a short post/announcement (X / r/ClaudeAI / LinkedIn) to gather initial users
- [ ] Hit 10+ stars on GitHub (loose marker that it's reaching real people)

---

## Demo Status

> Per the skill's own demo-always principle: a working version of the user-facing artifact must exist at every layer.

- **Current demo:** Install via `git clone https://github.com/AlanSEncinas/marble.git` into `~/.claude/skills/`, restart Claude Code, observe the skill firing. New README (marble-vs-galaxy story + features) is the static demo. Repo is private while polishing — install command works only for Alan until flipped public.
- **Last verified working:** 2026-05-12 (auto-fire confirmed in Starmap fresh-project test under the old name; post-rename verification pending after directory + repo rename)
- **Gap:** No video / asciinema / animated GIF showing the experience. Layer 2 task. Also no operational Quickstart in README — only the story/identity copy.

---

## Phase History

> One-line summary when a layer fully ships. Detail moves to `CLAUDE.md` §5.

- _Layer 1 — Foundation: SHIPPED 2026-05-12._ Public-shape repo exists, skill installs cleanly, skill auto-fires reliably (verified via Starmap fresh-project test). Layer 1 done definition met.
- _Layer 2 — Stability & Adoption: IN PROGRESS._ Rebrand to `marble` shipped (`1225493`, 2026-05-12) and verified firing under the new name; Quickstart, screenshots, public-flip, and external user feedback still pending.
