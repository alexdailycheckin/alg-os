# Capability Sync - Mode 1 (First-Run Calibration)

Runs invisibly during Phase 1 of intake. Calibrates the operator's recommendation engine and skill defaults to current platform reality at the moment they fork. The operator does not see a release log. They see a framework that knows what is currently available.

This file describes the procedure. Read in full before executing.

## What mode 1 produces

A snapshot file at `/workspace/research/capability-snapshot.md` containing:

- Current Claude model in use, with its capabilities relevant to ALG OS skills.
- Current MCP connectors available in the public registry.
- Current ALG OS framework version (read from repo `CHANGELOG.md`).
- A short "what this unlocks" note that downstream skills can read for context.

## Procedure

### Step 1 - Confirm the operator has working web access

If `web_fetch` and `web_search` are not available in the current Claude session, log that in the snapshot and proceed with the framework's default taxonomy. Mode 1 still completes, just with a "no live calibration available" note.

### Step 2 - Anthropic state

`web_fetch` these:

- `https://docs.claude.com/en/docs/about-claude/models/overview` (current Claude model lineup and capabilities)
- `https://docs.claude.com/en/release-notes/overview` (recent changes)

Extract:

- Current default model (e.g. Sonnet 4.6, Opus 4.7).
- Native capabilities relevant to ALG OS skill categories: web research, file handling, code execution, computer use, structured output, vision, voice.
- Any deprecations or model changes the operator should know about.

### Step 3 - MCP registry state

`web_fetch` the MCP connector registry. Extract:

- Connectors available for the data sources ALG OS operators commonly use: calendar, email, CRM, transcripts, docs, project management, file storage.
- Notable additions in the last 90 days.

If the registry endpoint is not accessible, fall back to the connector list documented in `/02-research/agent-taxonomy.md` (once that file is built in Build 1's second priority).

### Step 4 - Framework state

Read `CHANGELOG.md` at the repo root. Extract:

- Current ALG OS version.
- Recent skill upgrades.
- Any required operator actions noted in recent releases.

### Step 5 - Snapshot

Write `/workspace/research/capability-snapshot.md` with the structured output below. This file is what the recommendation engine and skills will read during their work. Keep it terse, factual, machine-readable.

```
# Capability Snapshot - <YYYY-MM-DD>

## Anthropic platform

- Default model: <model name and version>
- Relevant native capabilities: <bulleted list>
- Recent changes: <bulleted list, last 90 days>
- Deprecations: <if any>

## MCP connectors

- Available connectors relevant to ALG OS: <bulleted list>
- Recent additions: <bulleted list, last 90 days>

## ALG OS framework

- Current version: <semver>
- Recent skill upgrades: <bulleted list>
- Required operator actions: <if any>

## What this unlocks

<3 to 5 sentences. Specific to what the operator's foundation work and downstream skills will benefit from. Keep this concrete: "Native voice agents are not yet in Claude, so the recommendation engine will route voice work to a third-party provider for now." Avoid generic platitudes.>
```

### Step 6 - Notify only on material change

If this is the first intake run for the operator (no prior snapshot exists), do nothing visible. Just write the file.

If this is a re-calibration (mode 2 territory, but mode 1 logic still applies on re-runs), see `/capability-sync/mode-2-resync.md`.

## Hard rules

- Mode 1 is silent. The operator does not see a "what's new" wall on day 1. Section 10.2 of the foundation doc is explicit on this.
- Mode 1 does NOT modify framework files. The agent taxonomy, the skill files, the templates are read-only at runtime. Mode 1 only writes to `/workspace/research/capability-snapshot.md`.
- If web access fails, mode 1 still completes by writing a snapshot that says "live calibration unavailable, defaults in use." Intake continues.
- Mode 1 runs once at intake. Do not re-run on every operator command. Use mode 2 for explicit re-syncs.

## What downstream skills do with the snapshot

Skills in `/03-execution/` read `/workspace/research/capability-snapshot.md` before they run. The recommendation engine in Build 3 reads it to filter the agent taxonomy against current platform reality. If the snapshot says "Claude now has native voice," the recommendation engine no longer routes voice work to an external provider by default.

Until Build 2 and Build 3 are complete, the snapshot is captured for future use. It does not change skill behaviour today because skills do not yet exist.
