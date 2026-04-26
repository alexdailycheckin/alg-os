# Capability Sync

Pulls from Anthropic docs, MCP registry, and the repo's own CHANGELOG. Two modes.

**Mode 1 (first-run calibration).** Runs invisibly during intake Phase 1. Calibrates the operator's recommendation engine and skill defaults to current platform reality at the moment they fork. The operator does not see a release log on day 1.

**Mode 2 (on-demand re-sync).** Operator runs manually when they ask "what's new" or equivalent. Surfaces material deltas filtered against their config. Default output: "nothing material since last run."

See `foundation.md` section 10.2.

## Files

| File | Purpose |
|---|---|
| `mode-1-calibration.md` | First-run calibration procedure. Runs silently during intake. |
| `mode-2-resync.md` | On-demand delta procedure. Runs when the operator explicitly asks for it. |
| `sources.md` | Canonical list of URLs and paths both modes read from. |

## Status

Build 1 v0.1 complete. Mode 1 runs during intake. Mode 2 is callable but has no prior snapshot to diff against until at least one mode 1 has run.

## Hard rules

- Mode 1 is silent. The operator does not see a release log on day 1.
- Mode 2 default output is "nothing material." Filtering is aggressive on purpose.
- Neither mode modifies framework files at runtime. Both write only to `/workspace/research/capability-snapshot.md`.
- No automatic background runs in v1. Mode 1 fires once during intake. Mode 2 fires when the operator asks.
