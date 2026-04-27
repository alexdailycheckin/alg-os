# 03 Execution

The four canonical skills.

- `/artefact` - signature artefact generator (the unit of compounding)
- `/teardown` - competitor and positioning analysis
- `/proposal` - post-discovery client document
- `/nurture` - post-proposal email sequence

Every skill reads from `/workspace/foundation/` and writes output to `/workspace/execution/<skill>/`. Every skill enforces a quality checklist before completion.

Operators extend this layer with their own skills inside `/workspace/execution/`. The four canonical skills are the floor, not the ceiling.

See `foundation.md` section 5.3 and section 12.2.

**Status:** Build 2 v0.2 complete. All four canonical skills are wired.

## Why four, not five

The original spec listed five canonical skills including a "handoff" skill (internal solutions team brief). Operator testing surfaced that handoff is situational, not universal: solo operators and motion types without a delivery team get no value from it. Per `foundation.md` section 5.3, the canonical floor is for skills that travel across operators. Handoff was demoted to an operator-extension example rather than canonical.

The canonical floor is now four. Operators with delivery teams can write their own handoff skill in `/workspace/execution/handoff/` per section 5.3's extension pattern.
