# MCP Blueprint Template

Template for the MCP connection blueprint. The meta-agent writes this to `/workspace/agents/mcp-blueprint.md`. It is the list of MCP connections the operator's agent stack needs.

The framework recommends. The operator connects.

```
# MCP Blueprint - <Operator Name>

**Generated:** <YYYY-MM-DD>
**ALG OS version:** <semver>

## Already connected

MCPs the operator confirmed are already connected at the time the meta-agent ran.

| MCP | Used by agents | Notes |
|---|---|---|
| <e.g. Fireflies> | <agents> | <e.g. owner: Alex; account-level connection> |
| <e.g. Gmail> | <agents> | ... |
| ... | ... | ... |

## Required (must connect to run the stack)

MCPs the agent stack requires that the operator does not yet have. Without these, certain agents cannot run.

| MCP | Used by agents | Why required | Alternatives |
|---|---|---|---|
| <e.g. CRM MCP> | <proposal-drafter, nurture> | <e.g. needed to detect proposal-sent and stalled-prospect events> | <2 to 3 named alternatives from agent-taxonomy.md> |
| ... | ... | ... | ... |

## Recommended (improves the stack but not blocking)

MCPs that would improve the stack's quality or coverage but are not blocking.

| MCP | Used by agents | Lift | Alternatives |
|---|---|---|---|
| <e.g. LinkedIn MCP> | <prospecting research, teardown> | <e.g. enriches teardown analysis with competitor's recent posts and hiring signals> | <2 to 3 alternatives> |
| ... | ... | ... | ... |

## Not yet supported

Categories where no MCP exists today that the agent stack needs. Capability sync mode 2 will flag when these become available.

| Capability | Agent that would benefit | Workaround today |
|---|---|---|
| <e.g. Vertical practice management software> | <ICP enrichment, market sizing> | <e.g. Manual data export, monthly upload> |
| ... | ... | ... |

## Connection workflow

For each MCP in "Required" above:

1. The operator opens Claude Code (or Claude Desktop) settings.
2. Adds the MCP using the connector from the MCP registry.
3. Authenticates with the relevant account.
4. Confirms connection by running the agent that uses it (the agent's definition file lists a manual-run command).
5. Updates this file's "Already connected" table.

## Connection security

Hard rules for any MCP connection:

- The framework never asks the operator to share credentials in conversation. Connection happens in Claude Desktop or Claude Code settings, not in chat.
- The framework never writes credentials to `/workspace/`. Anything credential-shaped that appears in conversation is flagged and refused.
- Operator-initiated only. The framework recommends; it does not auto-connect.

## v0.1 limitations

- v0.1 lists the MCP needs but does not auto-test connections. The operator runs each agent at least once to verify connections work.
- v0.2 will add a "test my connections" command that verifies the stack's MCP requirements.
- v0.2 will surface broken connections in the agent stack health metrics.

## Capability sync integration

When capability sync mode 2 surfaces a new MCP that an agent in this stack could benefit from, this file is updated on `alg-upgrade`. The new MCP appears under "Recommended" with the agents it would lift.

If a previously-required MCP is replaced by a better alternative (e.g., a new connector that does what two existing ones did combined), capability sync flags this as a material delta.
```

## Notes for the meta-agent writing this template

- "Required" is for connections without which agents cannot run at all. Use sparingly.
- "Recommended" is for connections that improve the stack. Most MCPs land here.
- "Not yet supported" is the honest list of gaps. This is where capability sync mode 2 has the most leverage.
- Alternatives must be 2 to 3 named options from the agent taxonomy. No single-vendor recommendations.
- The connection workflow should be as terse as possible while remaining accurate. Operators read this once, refer back rarely.
