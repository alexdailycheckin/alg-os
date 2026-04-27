# Changelog

All notable changes to ALG OS. Format follows Keep a Changelog. Project uses semver.

## [Unreleased]

### Added
- Framework directory scaffold per `foundation.md` section 11.
- Root files: `CLAUDE.md` (orchestrator), `README.md`, `alg-upgrade` (stub), `.gitignore`.
- Foundation document at `foundation.md` (v0.4).
- **Build 1 v0.1 (sparring layer, foundation templates, capability sync v1):**
  - `/00-intake/intake.md` (master orchestrator, eight-phase flow).
  - `/00-intake/sparring-rules.md` (refusal logic by foundation area).
  - `/00-intake/questionnaire.md` (structured question set).
  - `/00-intake/data-ingestion.md` (file upload + online research procedures).
  - `/01-foundation/` templates: `voice.md`, `brand.md`, `services.md`, `icp.md`, `personas.md`, `positioning.md`, `markets.md`, `team.md`, `pricing.md`, `gtm-motion.md`.
  - `/capability-sync/mode-1-calibration.md` (silent first-run calibration).
  - `/capability-sync/mode-2-resync.md` (on-demand delta).
  - `/capability-sync/sources.md` (canonical source list).
  - `CLAUDE.md` updated to route operator commands into the new files.
  - Per-directory READMEs updated to reflect Build 1 v0.1 status.
- **Build 2 v0.1 (agent taxonomy + artefact skill):**
  - `/02-research/agent-taxonomy.md` (10 categories, four tiers per category, vendor-neutral named alternatives).
  - `/03-execution/artefact/skill.md` (five-phase orchestrator: fit diagnostic, three candidates, operator picks, full spec, hand-off).
  - `/03-execution/artefact/diagnostic.md` (four diagnostic questions, five patterns A to E, scoring matrix).
  - `/03-execution/artefact/quality-checklist.md` (12-item bar with documented exception logic, max 2 exceptions per spec).
  - `/03-execution/artefact/templates/spec.md` (output template the skill writes per artefact).
  - `RUNNING.md` (operator quickstart with permission-prompt guidance).
  - `CLAUDE.md` updated to route the artefact skill into the new files and to reflect Build 2 v0.1 status.
- **Build 2 v0.2 (three more canonical skills + structural reframe):**
  - `/03-execution/teardown/skill.md` (eight-phase competitor and positioning analysis).
  - `/03-execution/proposal/skill.md` (five-phase post-discovery client document).
  - `/03-execution/nurture/skill.md` (four-phase post-proposal email sequence with stall diagnosis).
  - Per-skill READMEs updated to Build 2 v0.2 status.
  - **Handoff dropped from canonical floor.** Operator testing showed handoff is situational (solo operators or motion types without a delivery team get no value). Demoted to operator-extension example. `/03-execution/handoff/` directory removed from the repo. Operators with delivery teams write their own in `/workspace/execution/handoff/`. The canonical floor is now four, not five.
  - `foundation.md` updated to reflect four canonical skills (sections 5.3, 11, 12.2, 16, 17).
  - **Build 3 reframed.** The original Build 3 spec was "tool-agnostic mode selector + recommendation engine + self-serve readiness." That scope is now subsumed inside a new spec: "build my agents," a meta-agent that ingests foundation + artefact spec + capability snapshot and produces working agent definitions, MCP connections, and scheduled triggers so the operator's motion runs autonomously. Detailed Build 3 spec lands in a separate session. `foundation.md` section 12.3 updated with the placeholder rubric.
  - `CLAUDE.md` updated to drop handoff routing and reflect Build 2 v0.2 status.

- **Build 2 v0.3 (artefact production):**
  - `/03-execution/artefact/production.md` (nine-phase production orchestrator: spec validation, data ingestion, analysis, drafting, voice and quality, distribution-ready formats, methodology, quality checklist, hand-off).
  - `/03-execution/artefact/skill.md` Phase 5 updated to add edition-1 branch (after spec is written, operator can produce edition 1 in the same session or run production later).
  - `/03-execution/artefact/README.md` updated to document spec + production modes.
  - `CLAUDE.md` updated with new operator commands ("produce my artefact edition," "ship edition <N>," etc.) and refined matching for spec vs production routes.
  - 10-item production-specific quality checklist with three-failure kill rule.
  - Edition numbering: sequential, zero-padded (01, 02, 03 ...). Suffix conventions for multi-cadence operators (Q1-2026, annual-2026, special-<slug>).
  - Distribution-ready formats per spec channel (web post, press release, LinkedIn personal, LinkedIn company, newsletter, X thread, partner template). Skip channels not in the spec; do not invent paths.
  - Methodology and data snapshot mandatory. Honest about limitations. Reproducible by future editions or audits.

- **Build 3 v0.1 (build my agents - the meta-agent):**
  - `/03-execution/build-my-agents/skill.md` (seven-phase orchestrator: map funnel to canonical skills, define each agent, MCP blueprint, schedule, stack overview, quality checklist, hand-off).
  - `/03-execution/build-my-agents/quality-checklist.md` (12-item bar with documented exception logic, max 2 exceptions).
  - `/03-execution/build-my-agents/templates/agent-definition.md` (per-agent definition template: trigger, owner, mode, inputs, skill invocation, outputs, review logic, run history, health).
  - `/03-execution/build-my-agents/templates/agent-stack.md` (operator-stack overview template: system-map narrative, funnel-step diagram, agent list, dependencies, review responsibilities, health metrics).
  - `/03-execution/build-my-agents/templates/mcp-blueprint.md` (MCP connection blueprint template: already-connected, required, recommended, not-yet-supported).
  - `/03-execution/build-my-agents/templates/schedule.md` (schedule template: manual default, optional cron/launchd, v0.2 placeholder).
  - `/03-execution/build-my-agents/README.md` (overview, status, what v0.1 is honest about, what v0.2 and v0.3 will add).
  - `CLAUDE.md` updated with new operator commands ("build my agents", "run the <agent name> agent") and Build 3 v0.1 status.
  - `/workspace/agents/` becomes a recognised workspace directory (joins `/workspace/foundation/`, `/workspace/research/`, `/workspace/execution/`, `/workspace/feedback/`).

### Honest scope flags for Build 3 v0.1

- v0.1 ships documentation and definitions, not autonomous infrastructure. The operator runs each agent manually via Claude Code on the schedule the framework defines. v0.2 ships hosted scheduling.
- v0.1 has no auto-test for MCP connections. Operators run each agent manually once to verify connections work.
- v0.1 has no agent observability. Run history is operator-maintained inside each agent definition.
- v0.1 has no operator-facing dashboard. The agent-stack.md document is the system map the operator reads.

### Coming next
- Build 3 v0.2: hosted scheduling. Agent observability. Agent extension framework (operators write their own agents in `/workspace/agents/custom/`). Connection auto-test.
- Build 3 v0.3: operator-facing dashboard. Capability sync auto-suggests stack updates on material platform deltas. Agent A/B framework.
- Build 1 patch queue items 1, 2, 3, 4 still open (terminal-language file ingestion, progress markers, task list sync, RUNNING.md gaps). Item 5 closed in `dd76150`. Item 6 (memory-saving) reframed: the meta-agent's run-history pattern handles a similar concern by giving each agent an operator-maintained log.

### Build 1 v0.1 patch queue (carried into Build 2 v0.2)
- "Drop in" file ingestion language is GUI-speak. Replace with terminal-appropriate.
- No progress markers during long operations. Add explicit progress lines.
- Task list display lags real phase transitions. Instruct Claude to update todos immediately on phase transition.
- `RUNNING.md` needs file-attachment-in-Claude-Code section and per-domain web_fetch prompt section.
- Orchestrator should refuse to offer features outside the current build status (Claude offered `/schedule` mode 2 which v1 explicitly excludes).
- Memory-saving behaviour fired but was not designed in. Decide whether to spec it or block it.

### Status
- Build 2 v0.1 complete: agent taxonomy and artefact skill shipped. Build 2 v0.2 (teardown, proposal, handoff, nurture) is next.

## [v0.4] - 2026-04-26 - Foundation

Foundation document established at v0.4 after a full QA pass against v0.3. Resolved items:

- Time-bound intake constraint replaced with quality bar.
- Capability sync split into first-run calibration and on-demand re-sync.
- Data ingestion sequence defined (file upload, online research, interactive intake with extraction and sparring).
- Framework versus workspace split architected for upgradability.
- Agent taxonomy made vendor-neutral end to end.
- Build validation rubrics reframed as framework quality gates rather than test-cohort outcomes.
