# 02 Research

Layer 2 of the four-layer system: research and reach. MCP config, data source schemas, intel templates.

Houses `agent-taxonomy.md`, the catalogue the recommendation engine reads from. Operators wire their own MCPs (Fireflies, Slack, Microsoft 365, monday.com, Gmail, Calendar, Drive, Airtable, plus whatever they bring).

See `foundation.md` sections 5.2 and 9.

## Files

| File | Purpose |
|---|---|
| `agent-taxonomy.md` | The catalogue. 10 agent categories, four tiers per category (native, specialist, custom orchestration, third-party SaaS), with named alternatives at every tier. The recommendation engine in Build 3 reads this. |

## Status

`agent-taxonomy.md` shipped in Build 2 v0.1. MCP config templates and data source schemas are pending and will land alongside Build 3 (the recommendation engine).

## Vendor neutrality

The taxonomy is vendor-neutral by design. Three or more named alternatives per tier where alternatives exist. No tier 4 entry has a single vendor unless the category has only one usable provider. ALG OS does not prefer any single shop, including any company Alexandru is associated with.
