# Capability Sync

Pulls from Anthropic docs, MCP registry, and the repo's own CHANGELOG. Two modes.

**Mode 1 (first-run calibration).** Runs invisibly during intake. Calibrates the operator's recommendation engine and skill defaults to current platform reality at the moment they fork. The operator does not see a release log on day 1.

**Mode 2 (on-demand re-sync).** Operator runs manually. Surfaces material deltas filtered against their config. Default output: "nothing material since last run."

See `foundation.md` section 10.2.

**Status:** v1 ships in Build 1 alongside intake so first-run calibration works from day 1.
