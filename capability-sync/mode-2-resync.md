# Capability Sync - Mode 2 (On-Demand Re-Sync)

Runs when the operator says "what's new," "any platform updates," or asks for a capability review. Surfaces material deltas filtered against the operator's config.

Default output is "nothing material since last run." That is the right answer most of the time. The signal stays high because the threshold is high.

## Procedure

### Step 1 - Read the previous snapshot

Load `/workspace/research/capability-snapshot.md` from the previous run. If no snapshot exists, run mode 1 first per `/capability-sync/mode-1-calibration.md`. Do not run mode 2 from cold.

### Step 2 - Pull current state

Run the same fetches as mode 1 step 2 to 4 (Anthropic, MCP registry, repo CHANGELOG).

### Step 3 - Compute delta

Compare current state against previous snapshot. Categorise every change into one of four buckets:

| Bucket | Action |
|---|---|
| Material to operator | Surface to operator with reasoning. |
| Future-relevant but not actionable today | Note in the new snapshot, do not surface. |
| Irrelevant to operator | Note in the new snapshot, do not surface. |
| No change | Skip. |

Material to operator means the change passes one of these three relevance gates:

1. A new Claude capability that affects an agent currently routed to a third-party tool in this operator's recommendation engine.
2. A new MCP connector that connects to a data source already in this operator's research plan or foundation files.
3. A canonical skill upgrade that affects work the operator has already shipped (e.g. a Proposal skill upgrade that changes output format, when the operator has already sent proposals using the previous format).

If none of those fire, output is "nothing material since last run."

### Step 4 - Write new snapshot

Overwrite `/workspace/research/capability-snapshot.md` with current state. The snapshot is now the new baseline for the next mode 2 run.

### Step 5 - Surface to operator (only if material)

```
Material updates since your last calibration on <date>:

1. <Change> - <Why this matters for your config> - <What it unlocks>
2. <Change> - <Why this matters> - <What it unlocks>
```

If the framework version has shifted, append:

```
Your fork is at v<X>. Latest is v<Y>. Run `./alg-upgrade` to pick up framework changes (workspace will not be touched).
```

If nothing material:

```
Nothing material since your last calibration on <date>.
```

## Hard rules

- Default output is "nothing material." Only surface real changes. Resist the urge to surface everything.
- Filter against the operator's config, not against the world. A new MCP for Slack does not matter if the operator has no Slack workflow.
- Do not run mode 2 automatically. Operator-initiated only.
- Do not paginate or expand the output. Keep it under 5 lines unless the operator asks for the full delta.

## When the operator asks for the full delta

If the operator says "show me everything that changed, not just material," dump the new snapshot in full. Do not filter. This is rare and explicit.
