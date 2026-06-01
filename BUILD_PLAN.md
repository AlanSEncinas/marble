# Build Plan — marble

> Forward-looking source of truth for what ships next on the skill itself. Update checkboxes in the same commit as the work. See `CLAUDE.md` §5 for backward-looking changelog. See `BACKLOG.md` for ideas not in the current layer.

**Current phase:** Layer 2 — Stability & Adoption
**Today's next action:** Continue lived-in pass — use marble in active projects (Trend Tents orchestrator, others) to pressure-test both 5/25 ships across another testing window:

- `29315ee` — description hardening (preemptive close of first-turn bypass routes: front-loaded REQUIRED-invoke language, forbid IDE-file-read shortcut, add hi/hello/morning trigger words)
- `4653c1d` — marketplace-ready README expansion (4-act Quickstart walkthrough, Memory integration bullet, save-points reframe, Who-this-is-for / NOT-for framing)

If friction or rule gaps surface in lived-in usage → patch marble first thing using the same RED → GREEN pattern. If clean across the testing window → decide on flipping `github.com/AlanSEncinas/marble` public, which removes the install-only-works-for-Alan barrier and unblocks the last open Layer 2 done-definition gate (one external user). Process note for tomorrow-Claude: when reviewing screenshots, ask explicitly *when* they were captured before treating them as live evidence (lesson from today's phantom-debugging arc; see CLAUDE.md §5 for 29315ee).

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
- [x] Bookend persistence fix: wrap rule now mandates writing the "Concrete next action for tomorrow" into BUILD_PLAN.md's `Today's next action:` line; Case A morning surfaces that line verbatim; "Shipped since last session" column renamed to "Recently shipped". Caught live this session when the morning produced a plausible-but-wrong game plan. CLAUDE.md §5 has full diagnosis. (2026-05-20)
- [x] Onboarding pass: Case B becomes announce-and-act (creates the trio without asking), Case B trigger broadened to project-intent signals (`idea.md` / `src/` / `package.json` / etc.), Case C narrowed to "no project signals + casual ask", four session-start trigger phrases (`hello` / `hi today is [date]` / `morning [date]` / `morning`) documented in `When to Use` and taught inline by Case B output, BUILD_PLAN.template.md placeholder updated to name its role as the wrap→morning handoff slot. (2026-05-20)
- [x] README copy refresh: Today's Game Plan, Session close, and "three files" sections now reflect today's shipped behavior (table-and-bullets format, state-snapshot wrap, BUILD_PLAN.md persistence, four session-start trigger phrases, announce-and-act bootstrap). Operational Quickstart still pending separately. (2026-05-20)
- [x] Description hardening (preemptive): tightened SKILL.md description to (1) lead with strongest instruction (REQUIRED to invoke on first model response, before generating any text), (2) explicitly forbid the file-read-before-skill-check shortcut (before reading any IDE-opened files), (3) add greeting trigger words ("hi" / "hello" / "morning") inline. Closes two rationalization routes the model could theoretically take on edge-case openers; verified via cold-restart repro after a week of lived-in usage confirmed marble was already firing correctly. CLAUDE.md §5 has full context. (2026-05-25)
- [x] Add a "Quickstart" section to README with a real example session — shipped as part of the 2026-05-25 marketplace-readiness README expansion (Path B). Four-act walkthrough across two days: Day 1 morning bootstrap → mid-session idea triage → evening wrap → Day 2 morning handoff pickup. Also added Who-this-is-for / NOT-for framing, Memory integration bullet, renamed "The three files" → "The save points" + reframed lead. CLAUDE.md §5 has full context. (2026-05-25)
- [x] Package marble as a Claude Code plugin: added `.claude-plugin/plugin.json` + `.claude-plugin/marketplace.json` so the repo doubles as its own single-plugin marketplace (`/plugin marketplace add AlanSEncinas/marble` → `/plugin install marble@alan-encinas-plugins`). Additive — root SKILL.md preserved, so bare-clone install and this dev workspace's auto-fire are unchanged. `claude plugin validate .` passes clean. README install section rewritten (plugin primary, clone alternative). — `837bfd4` (2026-05-31)
- [ ] Flip GitHub repo public when polish is complete
- [ ] Submit marble to `anthropics/claude-plugins-community` marketplace via the submission form (claude.ai/settings/plugins/submit) — requires Alan's account + repo public first. Adds public discoverability + the `marble@claude-community` install path.
- [ ] Get one external user to install and run a session — collect feedback on (a) does it fire, (b) is Today's Game Plan valuable, (c) any friction points
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
- **Demo coverage:** Operational Quickstart in README (4-act walkthrough, shipped 5/25/26) is the text demo. Visual demo (screenshot/GIF/asciinema) deliberately dropped from scope — text Quickstart covers the "what does using marble look like" question for marketplace browsers.

---

## Phase History

> One-line summary when a layer fully ships. Detail moves to `CLAUDE.md` §5.

- _Layer 1 — Foundation: SHIPPED 2026-05-12._ Public-shape repo exists, skill installs cleanly, skill auto-fires reliably (verified via Starmap fresh-project test). Layer 1 done definition met.
- _Layer 2 — Stability & Adoption: IN PROGRESS._ Rebrand to `marble` shipped (`1225493`, 2026-05-12) and verified firing under the new name; Quickstart shipped (5/25/26); public-flip and external user feedback still pending.
