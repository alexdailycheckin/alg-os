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
