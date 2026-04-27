# Build My Agents - The Meta-Agent

The framework's autonomous-motion layer. Reads the operator's foundation, artefact spec, capability snapshot, and agent taxonomy. Produces a working agent stack: definitions, MCP blueprint, schedule, and a system-map overview.

This is Build 3 v0.1. The original Build 3 spec was a tool-agnostic recommendation engine. Operator testing during Build 2 surfaced a sharper need: not "which tools should I pick" but "build me the running agent stack that makes my motion autonomous." This skill is that.

See `foundation.md` section 12.3.

## Files

| File | Purpose |
|---|---|
| `skill.md` | Meta-agent orchestrator. Seven-phase flow: map funnel to canonical skills, define each agent, MCP blueprint, schedule, stack overview, quality checklist, hand-off. |
| `quality-checklist.md` | The 12-item bar that the agent stack must clear before being written. |
| `templates/agent-definition.md` | Per-agent definition template. The meta-agent writes one of these per agent in the operator's stack. |
| `templates/agent-stack.md` | Operator's stack overview template. The system map. |
| `templates/mcp-blueprint.md` | MCP connection blueprint template. The list of MCPs the operator's stack needs. |
| `templates/schedule.md` | Schedule template. When each agent runs and how to trigger. |

## Status

Build 3 v0.1 complete. Documentation and definitions, not autonomous infrastructure. The operator runs each agent manually via Claude Code until v0.2 ships scheduling.

## What v0.1 is honest about

- The meta-agent does not run the operator's stack. It builds the stack as definitions and a runbook.
- v0.1 has no scheduling infrastructure. Operators with cron or launchd skills can deploy the cadenced agents themselves; the schedule template provides the cron expressions.
- v0.1 has no auto-test for MCP connections. Operators run each agent manually once to verify connections.
- v0.1 has no agent observability. Run history is operator-maintained inside each agent definition.

## What v0.2 will add

- Hosted scheduling. The stack runs autonomously without operator manual invocation.
- Agent observability. Per-agent run history, success rate, review queue depth, surfaced in the stack overview.
- Agent extension framework. Operators can write their own agents in `/workspace/agents/custom/` using the same definition template.
- Connection auto-test. A "test my connections" command that verifies the stack's MCP requirements.

## What v0.3 will add

- Operator-facing dashboard. UI summarising stack status and pending reviews.
- Capability sync integration that auto-suggests agent stack updates when material platform deltas surface.
- Agent A/B framework so operators can run two versions of an agent (e.g., two proposal drafters with different framings) and pick the winner.

## Validation

Run the meta-agent against an operator who has completed intake AND has at least an artefact spec. Expected:

1. Refuses to run if foundation files, artefact spec, or capability snapshot are missing.
2. Confirms the four-step funnel with the operator.
3. Confirms current MCP and tooling reality.
4. Maps the funnel to canonical skills.
5. Produces 5+ agent definitions (artefact production, proposal drafter, teardown on-demand, nurture, capability sync, plus optional handoff if the operator has a delivery team).
6. Produces a complete MCP blueprint with required, recommended, and not-yet-supported sections.
7. Produces a schedule with manual, cron, and v0.2-placeholder paths.
8. Produces a stack overview with the system-map narrative, funnel-step diagram, dependencies, review responsibilities, and health metrics.
9. Quality checklist passes 12 of 12, or has at most 2 documented exceptions.
10. The operator can run any agent from its definition file using the manual command listed.
