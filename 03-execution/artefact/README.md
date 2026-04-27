# Artefact Skill

The signature artefact generator. Takes an operator's business and helps them design THEIR signature artefact. Not a template. A diagnostic.

Reads the operator's foundation files plus the capability snapshot. Runs a fit diagnostic to pick the right pattern (A: signature named-entity index, B: state-of-category report, C: anonymised benchmark, D: industry diagnostic tool, E: honest no fit). Produces a complete spec at `/workspace/execution/artefact/<slug>-spec.md` that passes a 12-item quality checklist.

See `foundation.md` section 8 for the design.

## Files

| File | Purpose |
|---|---|
| `skill.md` | The orchestrator. Five-phase flow from fit diagnostic to spec hand-off. |
| `diagnostic.md` | The fit diagnostic logic. Four questions, five patterns, scoring matrix. |
| `quality-checklist.md` | The 12-item bar that every spec must clear before being written to `/workspace/execution/artefact/`. |
| `templates/spec.md` | The output template the skill writes per artefact. |

## Status

Build 2 v0.1 complete. The artefact skill is the most demanding skill in the framework per `foundation.md` section 12.2 and was built first in Build 2 per section 17 step 7.

## Validation

Run the skill against an operator who has completed intake. Expected:

1. Skill refuses to run if foundation files are missing or intake validation has not passed.
2. Fit diagnostic correctly identifies the pattern that fits the operator's business.
3. Three candidate artefacts proposed within the chosen pattern.
4. Operator picks one, skill produces a full spec.
5. Spec passes the 12-item quality checklist or has at most 2 documented exceptions.
6. Spec connects to step 2 (the buyer's natural next question) of the four-step funnel.
