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

### Status
- Build 1 v0.1 complete and testable end-to-end. Build 2 (five canonical execution skills) starts next.

## [v0.4] - 2026-04-26 - Foundation

Foundation document established at v0.4 after a full QA pass against v0.3. Resolved items:

- Time-bound intake constraint replaced with quality bar.
- Capability sync split into first-run calibration and on-demand re-sync.
- Data ingestion sequence defined (file upload, online research, interactive intake with extraction and sparring).
- Framework versus workspace split architected for upgradability.
- Agent taxonomy made vendor-neutral end to end.
- Build validation rubrics reframed as framework quality gates rather than test-cohort outcomes.
