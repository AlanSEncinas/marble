# CLAUDE.md — marble (skill development workspace)

> Auto-loaded by Claude Code when you open a session in this directory. Distinct from any project that *uses* the skill — this is the workspace where we *develop and maintain* it. Last updated: 2026-05-20.

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
3. Open Claude Code in any test directory (often best to open a fresh empty folder so case B/C of Today's Game Plan gets exercised)
4. Send an opening message and observe whether the skill fires
5. If it fires correctly → commit + push. If not → diagnose, edit, re-test.

**Red flag:** If `SKILL.md` was edited but the old version is still firing, you forgot to fully restart Claude Code. The hot-reload path doesn't pick up frontmatter changes.

---

## 4. How the skill works (one-paragraph refresher)

The skill is auto-discovered by Claude Code via its description — it lists "Use when..." triggering conditions. When the model sees a matching condition (session start, trigger words, mid-phase ideas, doubt language, session end), it invokes the skill via the `Skill` tool, loads the body, and follows the rules. The body has a routing table that hands off engineering work to the right superpowers skill (brainstorming, TDD, debugging, verification, etc.). The three rules the skill owns directly: Today's Game Plan (session bookend), idea triage (BACKLOG), commit discipline (phase-prefixed messages, same-session doc updates).

---

## 5. Recently shipped

**2026-05-31 — `Layer 2`: package marble as an installable plugin + tone down README + scope cuts to BUILD_PLAN**
- Pre-public-flip session. Alan's direction evolved across the session: "make this live, no extra stuff" → "update the readme so it's not so emo" → "make the readme in my tone more" → "lets make this live and also live in claude." Threads: (1) trim Layer 2 scope, (2) de-emotionalize + re-voice the README, (3) make marble installable as a plugin / in the community marketplace.
- **Plugin packaging (`837bfd4`) — the headline change.** "Live in claude" resolved (via two claude-code-guide research passes) to: make the repo a valid Claude Code plugin + submit to the community marketplace. Critical finding from research: **a root-level `SKILL.md` is a valid plugin skill location**, so the change is fully additive — no files move. Added `.claude-plugin/plugin.json` (plugin manifest; root SKILL.md auto-discovered, namespaces as `/marble:marble` when plugin-installed) + `.claude-plugin/marketplace.json` (repo doubles as its own single-plugin marketplace, `source: "./"`). Because SKILL.md stays at root, three install paths now coexist: (a) plugin via repo-marketplace (`/plugin marketplace add AlanSEncinas/marble`), (b) community marketplace once submitted (`marble@claude-community`), (c) bare clone into `~/.claude/skills/marble` (unchanged). Crucially this means **this dev workspace keeps firing marble as a personal skill exactly as before** — the plugin manifest doesn't disturb the personal-skill loader. Avoided bug #44120 (a `.claude/` dir inside a plugin breaks skill discovery — marble has none). `claude plugin validate .` passes clean (after adding `metadata.description` to clear a warning). Privacy default taken: used GitHub URL, not Alan's personal email, in the public manifests. Routed through `superpowers:brainstorming` (structural change) → design approved → implemented directly rather than full writing-plans ceremony, since it's a 2-JSON + README change where `claude plugin validate` IS the meaningful verification (not TDD). Still pending (Alan's manual steps): flip repo public, submit to `anthropics/claude-plugins-community` via claude.ai/settings/plugins/submit.
- **README tone pass (`c0ef7ba`):** cut the "for builders who spiral" tagline, the doubt confessional in the opening ("the momentum dies, the doubt moves in," "I was the problem I kept running into," "is this even worth it," "the work was real, the self-doubt wasn't"), and the punchy emotional one-liners scattered through the feature list ("It sounds simple. It changes everything.", "You stay on the marble. The galaxy waits.", "The work is real. Keep going.", "Ambiguity feeds doubt."). Kept: the marble→galaxy metaphor (it's the name/identity), the brief factual origin (solo manufacturing op across 14 markets + software side projects, recurring lose-the-thread failure mode), all feature descriptions, the Quickstart, install, and the "Memory drifts. Chat history disappears." triad (punchy but factual, not emo). Net −4 lines. Presentation copy → no `superpowers:writing-skills` handoff (same logic as all prior README copy passes).
- **Blunt-builder voice pass (`f20cc26`):** Alan then asked for the README "in my tone more." Offered three tonal directions as AskUserQuestion previews (Blunt builder / Plainspoken personal / Tight-minimal); he picked **Blunt builder**. Rewrote the intro block, the conductor paragraph, and who-this-is-for in that voice — shorter sentences, less gloss, "keeps you on one phase instead of the whole project," "I built the thing that keeps me moving." Feature bullets + Quickstart were already concrete/on-voice, left as-is. Tone reference for future README work: blunt, confident, no fluff, matches how Alan talks in chat.
- **Scope cuts to BUILD_PLAN.md (`eafdc18`):** dropped two Layer 2 tasks Alan no longer wants gating the layer — the visual demo (screenshots/asciinema/GIF; text Quickstart shipped 5/25 covers the demo gap) and the polished blog/LinkedIn launch. Cleaned the dangling references in Demo Status + Phase History so the file stays coherent. Layer 3's broader "gather initial users" announcement item (which also mentions LinkedIn) deliberately left intact per Alan ("no need" to cut it).
- **What's left on Layer 2:** flip `github.com/AlanSEncinas/marble` public (the one remaining gate Alan is actively pushing on this session — blocked on `gh` not being authenticated locally; handed to Alan to flip via browser Settings → Danger Zone, or `gh auth login` then I flip it), get one external user, address top friction point from external feedback.

**2026-05-25 — `Layer 2 docs`: README expansion for Anthropic Claude Skills marketplace readiness (Path B: three originally-proposed edits + Who-this-is-for + Quickstart)**
- Alan asked whether the README covers what marketplace browsers will need before submitting marble to Anthropic Claude Skills. Audit surfaced four real gaps: no concrete walkthrough showing what using marble actually looks like, no Who-this-is-for / NOT-for framing, no Memory mention anywhere, save-points framing underplayed (only one line at the end of "The three files" section).
- Three-option offer made (A: minimum viable, B: marketplace-ready with Quickstart, C: full polish with visuals). Alan picked B. Path B was framed as the highest-leverage single addition because Quickstart is what actually converts curiosity to install on a marketplace; screenshots can come from a future external user.
- **Five additions in README.md:**
  1. **Two-pillars sentence in intro paragraph.** "Underneath, it adds two things AI sessions typically lack: durable save points on disk that bridge every session, and a structured memory layer that remembers you, your projects, and how you work." Names the two structural features beyond anti-spiral discipline.
  2. **New "Who this is for" mini-section** between the intro paragraph and "What it does." Solo operators and small teams shipping real work. Explicitly NOT for: fully autonomous coding agents (marble routes to engineering skills, doesn't write code itself), enterprise dev orgs with existing process, kanban-board seekers. Sets expectations before reader invests in deep-dive.
  3. **New Memory integration bullet in "What it does."** Closes the gap where the previous README never mentioned memory at all. Names what marble writes to memory (user / projects / feedback patterns) and what it doesn't (code, recent changes — those live in files/git).
  4. **"The three files" renamed to "The save points" + reframed.** Lead with "Memory drifts. Chat history disappears. AI sessions don't remember each other." instead of burying it as the closer. Names them explicitly as save points. BUILD_PLAN.md's handoff line called out as "the literal save point that bridges sessions."
  5. **New Quickstart section** between "The save points" and "Install." Four-act concrete walkthrough across two days: Day 1 morning (Case B bootstrap with verbatim output), Day 1 mid-session (idea triage to BACKLOG), Day 1 evening (wrap state snapshot + handoff persistence), Day 2 morning (Today's Game Plan picks up handoff verbatim). Uses realistic-feeling examples (Python parser CLI, pytest test names, real-feeling commit hash and phase structure) so the "what does using marble actually look like" question is answerable from the README alone.
- **Closes Layer 2 BUILD_PLAN.md checkbox:** "Add a 'Quickstart' section to README with a real example session."
- **What's still open in Layer 2:** screenshots/asciinema transcript (visual demo is a separate task; Quickstart in text form covers the demo gap for now), flip GitHub repo public, publish blog post + LinkedIn post, get one external user, address top friction point from external feedback.
- **Layer 2 done-definition status:** "skill fires reliably across cold and warm starts" ✅ (verified across week of lived-in usage), "has a clear demo/example showing the morning-call flow" ✅ (Quickstart now provides this in text), "has been tested by at least one user other than the author" ❌ (still requires getting an external user). Two of three subcriteria met; the external-user gate is what remains before Layer 2 fully ships.
- **No `superpowers:writing-skills` handoff** — README is presentation copy, not skill rules. Same logic applied to the 5/20 README copy refresh (`80f9e18`).

**2026-05-25 — `Layer 2`: harden marble description to close first-turn bypass routes (preemptive tightening after a week of lived-in usage)**
- Context: the 5/20 changes (`0d057aa` bookend persistence, `8ab728e` onboarding pass with Case B announce-and-act, `80f9e18` README refresh) shipped just before a multi-day testing window. The 5/20 wrap's handoff was "test the patches in real projects; patch marble first thing if lived-in usage surfaces a rule gap." A week of lived-in usage followed and marble fired correctly. No current bug.
- Took the opportunity to preemptively close two rationalization routes the model could theoretically take on edge-case openers (one-word greetings + visible IDE files), even though no current failure was forcing them.
- **Three structural edits to the description (SKILL.md frontmatter line 3, only):**
  1. **Lead with the strongest instruction.** Moved the strict invocation requirement to the front: "REQUIRED to invoke via the Skill tool on the first model response, before generating any text". Closes the bypass route where "starting any conversation" can get interpreted as a soft trigger that waits until intent is clear.
  2. **Forbid the file-read-before-skill-check shortcut explicitly.** Added "before reading any IDE-opened files". Closes the route where IDE context with a visible project file could bias the model toward direct engagement instead of skill check.
  3. **Greeting trigger words added.** "hi" / "hello" / "morning" added to the explicit trigger-word list alongside the existing "commit" / "done for today" / "ship it". Gives the model substring-match paths to fire marble on casual openers.
- **What we deliberately did NOT touch:** the body of SKILL.md (Today's Game Plan rule, Case A/B/C dispatch, routing table, all other rules). Description-only edit; behavior of marble once fired is unchanged.
- **Verification:** Alan ran a cold-restart repro (full Claude Code exit, fresh project dir with one `idea.md`, typed "hi"). Marble fired Case B announce-and-act before any other response. GREEN confirmed the tightened description still triggers correctly in the working case; rationalization-route closures don't change observable behavior in cases that were already working.
- **`superpowers:writing-skills` invoked** per marble's routing rule that description changes ARE rule changes. RED was hypothetical bypass routes the previous description left open; GREEN was the post-edit cold-restart test.
- **Process note for future me:** during this session I temporarily mistook an old screenshot from earlier in the week for a fresh real-session failure and built an unnecessary systematic-debugging arc around it. The description tightening landed anyway and was verified working, so the file edits stayed. The §5 entry above was rewritten from the misframed "fresh bug caught today" framing to this honest preemptive-hardening framing before the commit went out. Lesson: when a user shares a screenshot, ask explicitly *when* it was captured before treating it as live evidence.

**2026-05-20 — `Layer 2 docs`: README copy refresh — Today's Game Plan + Session close + "three files" sections now reflect today's shipped behavior**
- Closing the open item flagged in the previous §5 entry ("README.md lines 21 + 31 still describe the bookend in older terms"). Alan said "update readme and then push" — explicit directive to finalize the README pass before publishing today's commits.
- Three surgical edits in README.md:
  - **Today's Game Plan bullet** rewritten from the older "three lines" framing to a table-and-bullets description with verbatim-handoff language. Also lists the four session-start trigger phrases (`hello` / `morning` / `morning [date]` / `hi today is [date]`) inline so new operators learn the openers without leaving the README.
  - **Session close bullet** now names the state-snapshot format and the BUILD_PLAN.md persistence step explicitly ("a concrete next action for tomorrow that gets persisted into your BUILD_PLAN.md so the next session picks it up verbatim. The two halves of the session bookend bridge through that file."). The principle line stays.
  - **"The three files" section** gets a new paragraph naming the announce-and-act bootstrap behavior: "Open Claude Code in a new project directory and the skill notices the files are missing — it announces what it's about to do, creates the trio from the marble templates, and teaches you the session-start trigger phrases inline. No setup ceremony. Just open and go." Plus a clause added to the BUILD_PLAN.md description naming its handoff role.
- **Deliberately NOT touched** (still scoped to the open Layer 2 Quickstart task): the README still lacks an operational Quickstart section showing a real example session (operator types → skill responds → commit → docs update). The Quickstart will be written once enough lived-in sessions have accumulated to give us a real recent session as the example. README copy refresh ≠ Quickstart write.
- **No `superpowers:writing-skills` handoff:** README is presentation copy, not skill rules. Same logic that's applied to the 2026-05-20 UX format edits and the morning-call rename.
- **Why this is its own commit:** Could have folded into `8ab728e` but didn't, because the previous commit explicitly named "deliberately not touched" — overwriting that decision in the same commit would have made the log harder to read. One commit per closed decision is cleaner.

**2026-05-20 — `Layer 2 UX`: Case B becomes announce-and-act, session-start trigger phrases taught inline, Case C narrowed to "no project signals" + template placeholder polish**
- Companion change to the bookend persistence fix shipped earlier today (`0d057aa`). Same session, same dev arc — once the persistence layer was in place, the next gap was operator-side: how does a brand-new project actually GET into the marble flow in the first place?
- Triggered by a real-session signal. Alan paste-quoted a Case C-ish output from a different session ("Hello! No BUILD_PLAN.md detected yet — treating this as a casual start. I see you've got `idea.md` open... Want me to read it and help you turn it into a real project?") and named the gap: the response was too tentative for a clear new-project signal. He wanted the response to be more like *"Hi, I noticed this is a new project. I don't see BACKLOG or the necessary files. In order to get started, I'm gonna create these. Moving forward you can either just say hello / hi today is / morning + date / morning, and that'll start every session. In the meantime, I'll get started on creating these new files."* Announce + act + teach openers, not ask permission.
- **Five edits in SKILL.md and one in BUILD_PLAN.template.md:**
  - `When to Use` list: added a new bullet for the four session-start trigger phrases (`hello` / `hi today is [date]` / `morning [date]` / `morning`) that explicitly invoke Today's Game Plan. Separated semantically from the existing auto-commit trigger words (`commit` / `done for today` / `ship it`) — distinct purposes, distinct phrases.
  - Case B trigger broadened: now fires on *signals of project intent* (explicit build/plan/design/code asks OR visible project-flavored artifacts like `idea.md`, `src/`, `package.json`, `*.ipynb`, a real `README.md`) — not only on the previous narrow "user explicitly asks to build" trigger.
  - Case B behavior changed from "propose bootstrapping" → "announce and act." Output is a verbatim template that includes operator education for the trigger phrases inline. After the announcement, Claude immediately copies the templates and generates a minimal `CLAUDE.md` stub, then routes to brainstorming (or to writing-plans if a written spec already exists per A1 spec-exists override).
  - Case B closing line documents the design intent: "when project intent is visible, the trio is a known precondition for everything else marble does, so asking permission is ceremony."
  - Case C trigger narrowed from "no `BUILD_PLAN.md` + casual ask" → "no `BUILD_PLAN.md` + **no project signals** + casual ask." Closing parenthetical makes the boundary explicit: "Case C is the narrow case: bare directory, casual ask. The moment a project signal appears, you're in Case B."
  - `BUILD_PLAN.template.md` line 6 placeholder updated to name its load-bearing role as the wrap → morning handoff slot. Future operators bootstrapping the trio now see *why* that line exists rather than treating it as boilerplate.
- **What we deliberately did NOT touch this round:** `README.md` lines 21 (Today's Game Plan) and 31 (Session close) still describe the bookend in older "three lines" terms. They're not technically wrong at the principle level, but they're now downstream of the table-and-bullets + persistence-layer changes shipped today. Holding the README copy refresh for the still-pending Layer 2 "Add Quickstart to README" task, which will rewrite README user-facing copy in one coherent pass with real example sessions. Flagging here so we don't forget.
- **RED signal:** Alan paste-quoting the prior session's response and explicitly contrasting it with his preferred shape ("I wanted to do is actually be more like..."). Same pattern as `0d057aa`, `d4427c2`, `0450e0e` — user-comparing-output-to-reference is the strongest baseline RED data marble's track record has. No subagent test (declined the same way the bookend persistence fix did).
- **Why this is one commit with the template polish:** the template line 6 update is a small housekeeping item from the persistence-layer dimension we shipped earlier today, and bundling it with the Case B/C wording change keeps the commit log coherent ("here's what closed out today's Layer 2 onboarding pass"). Could have been two commits; one is fine and reads better.
- **REFACTOR plan:** lived-in pass — the next time anyone opens Claude Code in a fresh project directory with `idea.md` or similar visible, Case B should fire correctly with the new output shape. Watch for: (a) does the broadened trigger fire too eagerly (e.g., directories with stray files that aren't really project intent), (b) do operators understand the trigger phrases or do they need explicit teaching elsewhere too, (c) does the announce-and-act posture ever create files the user didn't want.

**2026-05-20 — `Layer 2 fix`: bookend persistence — wrap→morning handoff now writes through BUILD_PLAN.md**
- Real-session bug caught live. Opening turn of this session, marble's Case A morning produced a plausible-looking game plan that completely missed the actual handoff: the previous session's wrap (in chat scrollback) had a literal "Concrete next action for tomorrow" in a copy-pasteable code block, but the new session had no read-path back to it. I dutifully read BUILD_PLAN.md / git log / memory (the three sources Case A pointed me at) and surfaced a paraphrased stale "Today's next action:" line from BUILD_PLAN.md as if it were today's focus. Alan caught it ("this isn't correct"), pasted yesterday's actual wrap screenshot, and asked what was wrong in the code.
- Three connected defects in SKILL.md, all real:
  - **D1: The wrap → morning handoff was unwritten anywhere readable.** The wrap rule (shipped earlier today in `d4427c2`) put "Concrete next action for tomorrow" in chat only. Chat dies between sessions; the morning has no access to it. The two halves of the bookend literally lived in different storage layers.
  - **D2: Case A didn't surface the handoff even if it had existed.** Step 1 said "Read `BUILD_PLAN.md` — what phase / current task?" — vague enough that I paraphrased rather than surfacing the `Today's next action:` line verbatim.
  - **D3: "Shipped since last session" had no session-boundary signal.** The rule asked me to filter for "what's actually new since last session" without providing any mechanism to know where last session ended. On a fresh-morning thread with zero new commits, the table mechanically fell back to "most recent 3-5 commits" and mislabeled prior-session work as new.
- **Fix applied — six edits total in SKILL.md, plus this CLAUDE.md entry and a BUILD_PLAN.md tickbox:**
  - Case A step 1 rewritten: explicit instruction to read `Today's next action:` line verbatim, with cross-reference to the wrap rule explaining why.
  - Case A output template: column renamed `Shipped since last session` → `Recently shipped` (state, not delta), and first focus item must be the verbatim handoff line, bold.
  - Case A trailing paragraph: "do not paraphrase" mandate is now explicit; if the handoff is stale, surface verbatim *and* note the shift as second focus item (don't silently rewrite); "Recently shipped" framing made explicit as snapshot-not-delta.
  - Wrap rule: new "**Persist the handoff — REQUIRED**" block mandates overwriting BUILD_PLAN.md's `Today's next action:` line with the wrap's concrete next action, in the same commit as the wrap. Explains why (chat dies, BUILD_PLAN.md persists).
  - Wrap "Why this shape" extended with a second paragraph naming the bookend-via-BUILD_PLAN.md design — two halves of the bookend talk through BUILD_PLAN.md, not chat.
  - Red Flags table: two new rows ("write the wrap to chat and skip the BUILD_PLAN.md update", "paraphrase the `Today's next action:` line").
- **RED data:** the failure was live, observable, in this session. Alan-as-user comparing the output to his actual wrap screenshot and explicitly asking "something has to be wrong in the code" is the strongest possible RED signal — exactly the same pattern as `00f0a7e` (A1+A2 rules from other-Claude real-session feedback). No subagent baseline run because the live in-the-wild failure is better evidence than any synthetic test. Marble's track record: real-session-RED + lived-in-pass-REFACTOR is the established pattern here.
- **Why this is a rule change, not a format change:** unlike the 2026-05-20 UX edits earlier today (table layouts), this changes *what the rules say to do* — Case A acquires a verbatim-surface mandate, the wrap acquires a mandatory persistence step. Per the established split, rule changes route through `superpowers:writing-skills` (invoked); format edits don't.
- **REFACTOR plan:** lived-in pass through next several real-session morning/wrap cycles. Watch for new rationalizations ("the line in BUILD_PLAN.md is *obviously* stale, I'll just rewrite it" is the predicted next loophole). If observed → add to Red Flags table.

**2026-05-20 — `Layer 2 UX`: session wrap becomes a state snapshot (supersedes wrap portion of earlier entry today)**
- Refined the session-wrap format spec within the same session it was first added — same-day RED-GREEN-REFACTOR cycle. Earlier entry today (commit `0450e0e`) shipped a "Change / Where" wrap table that listed commits. Alan saw it, then pasted a screenshot from a different session showing the format he actually wanted: an "Item / Status" *state snapshot* (branch, tests, gates, artifacts, frozen state) + concrete next action in a code block + optional honest-read closing line. Strongest possible RED signal: the user explicitly comparing my output to his preferred reference and pointing at the gap.
- The new shape splits morning and wrap by *semantic function*: morning = action log ("what happened while I was away"), wrap = state snapshot ("what's currently true so tomorrow-me can pick up"). Tomorrow-you doesn't need yesterday's commit subjects (git log has those); tomorrow-you needs to know what's pushed, what's blocking, and the literal next command.
- Format: "Session closed cleanly — M/D/YY. Final state:" header → Item/Status table (always: Branch with push/merge status, Tests if project has them; conditional rows for material changes — artifacts, experiments, gates, deploys, anything frozen) → "Concrete next action for tomorrow" in a copy-pasteable code block → optional one-line honest read when substantive.
- Required state-gathering commands: `git status`, `git log origin/[branch]..HEAD --oneline`, project's test command if recently run. Don't guess values.
- **Psychological design intent (explicit per Alan's framing):** concrete state replaces "we made progress" with facts (pairs with the Doubt handler rule), and the honest-read line names real accomplishments explicitly when they exist — counter to the "did I do anything today" spiral. The wrap format is part of marble's anti-doubt architecture, not just visual polish.
- Date format: chose option 2 from the proposed slate ("Session closed cleanly — 5/20/26") — gives a temporal anchor without needing a session-counter mechanism marble doesn't have.
- `superpowers:writing-skills` handoff skipped — same logic as the previous UX entries today: this is a presentation-format change, not a discipline-rule change. The RED signal here was the user himself comparing formats in-session, which is the strongest possible baseline data.
- This entry partially supersedes the next entry (the original "Layer 2 UX: Today's Game Plan + session wrap adopt table-and-bullets format" from earlier today). The morning-call portion of that entry still stands as-shipped; only the wrap portion is replaced by this snapshot format.

**2026-05-20 — `Layer 2 UX`: Today's Game Plan + session wrap adopt table-and-bullets format (Case A only)**
- Format change to how marble *presents* the session bookends. No discipline rule changed: still 3-line equivalent content (where we are / what shipped / next action), still blocks new work until acknowledged, still requires at least one concrete next action.
- Triggered by direct user observation: Alan saw both the terse 3-line morning call AND the table-style "What landed this session" summary I produced at session wrap (commit `00f0a7e`), and stated the table format was easier to scan and more presentable. Strongest possible RED signal — the user himself comparing formats in-session.
- New format for Case A morning call: "Hello — today is M/D/YY. [Phase line]" header + Shipped-since-last-session table (3-5 most recent commits with dates) + "Today's focus:" bullet list (lead with primary next action).
- New format for session wrap (triggers `ship it` / `done for today` / explicit wrap): "Session wrap." + Shipped-this-session table (commit subject + files/scope) + "Next:" bullet list (one concrete action required).
- Cases B and C deliberately unchanged — they stay lightweight. Case B has no project data yet (table would be empty placeholders); Case C is a casual one-off where a table would be ceremony. Same principle as the A1 spec-exists rule on a different surface: only invoke the heavier format when there's something to populate.
- Date format: US (`5/20/26`). Matches Alan's own opener convention this session.
- `superpowers:writing-skills` handoff skipped — this is a presentation-format change, not a discipline-rule change. Same logic as the "Morning call" → "Today's Game Plan" rename (2026-05-12). The skill suite is built for rule design + adversarial testing, not output formatting.

**2026-05-20 — `Layer 2 rules`: spec-exists override + workflow-blockers override + honest superpowers dependency**
- Three connected changes driven by 8 days of real-session usage feedback from another Claude running marble in Alan's actual project work.
- **A1 — Spec-exists override on the brainstorming handoff (SKILL.md routing table).** Real-session failure mode observed: the other Claude invoked `superpowers:brainstorming` for a one-line URL polish that was already designed in BACKLOG, and for an EPCO gating fix where the user had already specified the design. Ceremony where none was warranted. New rule: if a written design exists (BACKLOG entry, operator's report, prior session's plan, written ticket, user's own spec), skip brainstorm and route directly to `writing-plans` or TDD. The gate is *"does a written spec exist?"* — not *"is this small?"* — which keeps a written-spec requirement intact while removing the loophole.
- **A2 — Workflow-blockers override the phase rule (SKILL.md Phase-Driven Discipline).** Real-session failure mode observed: when a UI element was broken-looking, marble pushed the other Claude to "finish current phase first" before fixing the blocker. Alan correctly overrode with "just fix the blocker." The user-instructions-priority-1 rule worked once invoked, but the default skew was too disciplined. New rule explicitly documents that blockers override phase as the *norm*, not an exception. Idea triage applies to *new ideas*, not to obstacles preventing forward motion.
- **A3b — Honest superpowers dependency in README.** The README previously said "Requires Claude Code and the [superpowers] plugin." A subagent test (dispatched 2026-05-20) confirmed marble actually works without superpowers — engineering handoffs degrade to model defaults but the project-conductor layer stays intact, and Claude naturally warns the user about missing skills (Skill tool's meta-rules + marble's red-flag list produce graceful behavior already). "Requires" overstated the dependency. New wording: "Requires Claude Code. Pairs with the superpowers plugin for the engineering handoffs — marble works standalone, but brainstorming/planning/TDD/debugging/verification fall back to model defaults instead of the disciplined superpowers versions. Install both for the full experience."
- **A3a — Graceful-degradation rule was proposed and dropped.** A subagent test showed the missing-skill case was already handled gracefully by existing rules (Skill tool's "only invoke skills in your available list" meta-rule + marble's red-flag list). Iron Law applied: no rule without observed failure. Adding A3a would have been hypothetical-case clutter.
- `superpowers:writing-skills` handoff invoked for A1 + A2 (real rule changes). RED phase was the other Claude's real-session feedback — exact baseline failures quoted in commit message. GREEN = the new rules. REFACTOR happens in next live sessions where the rules get pressure-tested in real use.

**2026-05-12 — `Layer 2 terminology`: rename "Morning call" → "Today's Game Plan"**
- UX terminology change to the session-start ritual. No behavioral rule changed — still 3 lines (where we are / what shipped / next action), still the 3-case A/B/C dispatch on `BUILD_PLAN.md` presence, still blocks new work until acknowledged.
- Triggered by a real-session observation: a "5/11/26 10:34pm" opener exposed that "morning call" has a time-of-day bias that breaks immersion for night-work. "Today's Game Plan" is time-agnostic and reads more like solo-operator language.
- Scope: forward-facing text only. Updated SKILL.md (§Overview, When to Use, section heading + body, Case C language), README.md (feature description), BUILD_PLAN.md (Quickstart task + external-user-feedback question), BACKLOG.md (the "why not a hook" rationale entry), and CLAUDE.md §3 testing protocol + §4 refresher.
- Out of scope (intentionally preserved as historical record): §5 changelog entries that shipped *under the name* "morning call" — they describe what existed at that time and shouldn't be rewritten.
- `superpowers:writing-skills` handoff skipped intentionally — it's built for designing rules + adversarial testing, not copy-edits.

**2026-05-12 — `Layer 2 rebrand`: phase-driven-shipping → marble**
- Renamed the skill from `phase-driven-shipping` to `marble`. Identity rebrand around the "marble vs galaxy" metaphor: every session anchored to one phase (the marble) rather than the full project (the galaxy), so complexity doesn't become paralysis.
- SKILL.md frontmatter (`name: marble`) and heading updated. No behavioral rules changed — routing table, morning call, doubt handler, commit discipline all identical.
- README.md fully rewritten: story-first ("builders who spiral"), personal context (solo operator, 14 markets), feature descriptions in plain language. Replaces the previous philosophy-first version.
- All internal references in CLAUDE.md / BUILD_PLAN.md / BACKLOG.md updated.
- Drafts of a website blog post ("I Built a Dev Skill to Stop My Own Brain from Sabotaging My Work") and a LinkedIn announcement exist outside this repo — not active yet, holding until public re-launch is ready.
- Commit `1225493` lands the file changes. Follow-up actions (local dir rename, GitHub repo rename, `git remote set-url`, post-rename auto-fire verification) all completed same day, 2026-05-12. Layer 2 rebrand item in `BUILD_PLAN.md` ticked.

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
