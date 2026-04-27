# Artefact Skill

The signature artefact generator. Two modes:

1. **Spec.** Reads the operator's foundation files plus the capability snapshot. Runs a fit diagnostic to pick the right pattern (A: signature named-entity index, B: state-of-category report, C: anonymised benchmark, D: industry diagnostic tool, E: honest no fit). Produces a complete spec at `/workspace/execution/artefact/<slug>-spec.md` that passes a 12-item quality checklist.

2. **Production.** Takes the spec plus operator-provided data and produces an actual edition at `/workspace/execution/artefact/<slug>-edition-<NN>/`. Canonical markdown, methodology, distribution-ready formats per the spec's distribution plan. Operator reviews and ships.

Spec and production can run in the same session (after the spec is written, the skill asks if the operator wants to produce edition 1) or independently (operator runs "produce my artefact edition" at any later time).

See `foundation.md` section 8.

## Files

| File | Purpose |
|---|---|
| `skill.md` | Spec orchestrator. Six-phase flow: fit diagnostic, three candidates, operator picks, full spec, quality checklist, edition-1 branch. |
| `diagnostic.md` | The fit diagnostic logic. Four questions, five patterns, scoring matrix. |
| `quality-checklist.md` | The 12-item bar that every spec must clear before being written. |
| `templates/spec.md` | The output template the spec writes per artefact. |
| `production.md` | Production orchestrator. Nine-phase flow from spec validation through data ingestion, analysis, drafting, voice, distribution formats, methodology, quality, hand-off. |

## Status

Build 2 v0.3 complete. Spec and production both wired. The artefact skill is the most demanding skill in the framework per `foundation.md` section 12.2 and the only one with both spec and production phases in v1. Other skills (teardown, proposal, nurture) produce a single output type each.

## Validation

Spec phase:

1. Skill refuses to run if foundation files are missing.
2. Fit diagnostic correctly identifies the pattern.
3. Three candidates proposed, operator picks one.
4. Spec passes the 12-item quality checklist.
5. Operator can choose to produce edition 1 in the same session or stop at the spec.

Production phase:

1. Skill refuses to run if no spec exists.
2. Operator's data is parsed and validated against the spec's data set definition.
3. Edition follows the spec's pattern (A/B/C/D).
4. Voice rules applied throughout.
5. Methodology is honest and reproducible.
6. Distribution formats match the spec's distribution plan.
7. Operator reviews and ships. Skill never auto-publishes.
