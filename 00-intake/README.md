# 00 Intake

The sparring layer. Structured intake that drives Layer 1 foundation generation.

This is the moat. Most "AI for GTM" tools accept whatever the user types. ALG OS refuses weak inputs and iterates until the quality bar is cleared.

See `foundation.md` section 7 for the design and section 12.1 for the build plan and validation rubric.

## Files

| File | Purpose |
|---|---|
| `intake.md` | Master orchestrator. Runs when the operator says "run intake" or equivalent. Eight-phase flow from voice calibration to foundation hand-off. |
| `sparring-rules.md` | The refusal logic. Refusal patterns for ICP, positioning, persona, signature artefact, services, GTM motion. |
| `questionnaire.md` | The structured question set used in Phase 4 (interactive intake). Nine sections plus voice. |
| `data-ingestion.md` | Phase 2 (file upload) and Phase 3 (online research) procedures. Defines the ingestion sequence that runs before interactive intake. |

## Status

Build 1 v0.1 complete. Testable end-to-end. Refinement comes from running it and observing failures against the validation rubric in `foundation.md` section 12.1.

## Validation rubric

1. Intake completes self-serve, no synchronous human support required.
2. Foundation files produced are vertical-specific.
3. Sparring layer rejects weak inputs.
4. Foundation files are internally coherent.
5. Operator can articulate their GTM motion shape in one paragraph after intake completes, and the foundation is defensible enough to run Build 2 skills against without Layer 1 rework.
