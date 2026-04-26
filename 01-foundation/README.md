# 01 Foundation

Templates for Layer 1 (context layer). Brand, ICPs, services, markets, positioning, team, stakeholders, budgets, pricing, personas, banned words, voice rules, GTM motion.

Templates here are framework property. The operator's filled-in foundation files live in `/workspace/foundation/` and are never overwritten by `alg-upgrade`.

See `foundation.md` section 5.1.

## Templates

| File | Produces in /workspace/foundation/ |
|---|---|
| `voice.md` | English variant, banned words, paragraph rules, tone. Read by every skill. |
| `brand.md` | One-liner, mission, core promise, what we are not. |
| `services.md` | Mode (product-recursive vs tool-agnostic), tiers, pricing per tier, delivery model. |
| `icp.md` | Vertical, revenue band, geography, trigger event, named pain, anti-ICP. |
| `personas.md` | Decision-maker, blocker, champion. Buying committee shape. |
| `positioning.md` | Competitor set, win axis, concession axis, one-line positioning statement. |
| `markets.md` | Geographies, verticals, segments, channel mix, out-of-scope. |
| `team.md` | Commercial, delivery, artefact-production owners. Decision rights. Gaps. |
| `pricing.md` | Floor, ceiling, typical mid-tier, model, discounting policy. |
| `gtm-motion.md` | The four-step funnel instantiated for this operator. The proof of intake completion. |

## Quality bar

Each template has a quality bar at the bottom of the file. The intake refuses to write any template to `/workspace/foundation/` until that template's bar is cleared. See `/00-intake/sparring-rules.md` for the refusal patterns applied during interactive intake.

## Status

Build 1 v0.1 complete. Templates are populated. Intake reads them as the shape it produces.
