# Capability Sync - Sources

Canonical list of sources both modes read from. If a source moves, update here once and both modes inherit.

## Anthropic

| Source | URL | Used by |
|---|---|---|
| Models overview | `https://docs.claude.com/en/docs/about-claude/models/overview` | Mode 1, Mode 2 |
| Release notes | `https://docs.claude.com/en/release-notes/overview` | Mode 1, Mode 2 |
| Capabilities reference | `https://docs.claude.com/en/docs/build-with-claude/overview` | Mode 1, Mode 2 |
| Tool use | `https://docs.claude.com/en/docs/build-with-claude/tool-use` | Mode 1 (capability inventory) |

## MCP

| Source | URL | Used by |
|---|---|---|
| MCP registry | `https://github.com/modelcontextprotocol` | Mode 1, Mode 2 |
| MCP servers index | `https://github.com/modelcontextprotocol/servers` | Mode 1, Mode 2 |

## ALG OS

| Source | Path | Used by |
|---|---|---|
| Framework CHANGELOG | `/CHANGELOG.md` | Mode 1, Mode 2 |
| Agent taxonomy | `/02-research/agent-taxonomy.md` | Mode 1 (cross-reference), Mode 2 (delta computation) |

## Failure modes

- If a URL returns 404, log in the snapshot under "source unavailable" and continue. Do not block intake on a missing source.
- If the MCP registry GitHub repo is rate-limited, retry once with a 5-second delay. If still failing, fall back to the local agent taxonomy.
- If `web_fetch` is not available in the Claude session, log "live calibration unavailable, defaults in use" and continue. Intake still completes.

## When sources change

Anthropic and MCP both reorganise their docs occasionally. If a fetch returns unexpected content (no recognisable model list, no recognisable connector list), log a warning to the snapshot and the operator. The framework should not silently calibrate on stale or wrong content.
