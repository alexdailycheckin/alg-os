# Schedule Template

Template for the operator's agent schedule. The meta-agent writes this to `/workspace/agents/schedule.md`. It defines when each agent runs and how the operator triggers it.

```
# Schedule - <Operator Name>

**Generated:** <YYYY-MM-DD>
**ALG OS version:** <semver>

## Default execution path: manual

v0.1 ships without scheduling infrastructure. The operator runs each agent in Claude Code on the schedule defined below. v0.2 will add hosted scheduling that picks this up automatically.

The manual path is enough to get value from the framework today. The "what to run when" section below tells the operator exactly what to type into Claude Code on which day.

## What to run when

### Cadenced agents

Agents that run on a calendar schedule.

| Agent | Cadence | Next run | Manual command in Claude Code |
|---|---|---|---|
| <artefact-production-quarterly> | <Quarterly, first Monday of Q1/Q2/Q3/Q4 at 9:00 GMT> | <YYYY-MM-DD> | "Run the artefact production agent" |
| <capability-sync-quarterly> | <Quarterly, first Monday of Q1/Q2/Q3/Q4 at 9:30 GMT> | <YYYY-MM-DD> | "Run capability sync mode 2" |
| ... | ... | ... | ... |

### Event-driven agents

Agents that fire on a business event. The event is detected by the operator (or by an MCP-connected system) and the operator triggers the agent.

| Agent | Event signal | What to watch | Manual command |
|---|---|---|---|
| <proposal-drafter> | <Discovery call complete, prospect qualified> | <Calendar (post-call), CRM (qualified status)> | "Draft a proposal for <prospect>" |
| <nurture-stalled-prospects> | <Proposal sent and no reply within 5 days> | <CRM (proposal status), inbox (no reply)> | "Nurture sequence for <prospect>" |
| <teardown-on-demand> | <Operator decides to study a competitor> | <Operator-initiated> | "Tear down <competitor>" |
| ... | ... | ... | ... |

## Optional: cron / launchd setup (operator-driven)

For operators who want to schedule the cadenced agents without manual invocation, here are the cron expressions and launchd plists. The operator sets these up themselves; ALG OS does not write to system configuration files.

### Cron expressions

```
# artefact-production-quarterly: first Monday of Jan/Apr/Jul/Oct at 9am
0 9 * 1,4,7,10 1 [ "$(date +\%d)" -le 7 ] && claude --no-interactive "Run the artefact production agent" >> ~/alg-os-logs/artefact.log 2>&1

# capability-sync-quarterly: first Monday of Jan/Apr/Jul/Oct at 9:30am
30 9 * 1,4,7,10 1 [ "$(date +\%d)" -le 7 ] && claude --no-interactive "Run capability sync mode 2" >> ~/alg-os-logs/capability-sync.log 2>&1
```

The `--no-interactive` flag is illustrative. Confirm against current Claude Code CLI flags before deploying. Logs go to `~/alg-os-logs/` (operator creates this directory).

Hard rule: never run cron jobs that auto-publish or auto-send. Cron jobs run agent SKILLS only. Outputs land in `/workspace/execution/` for operator review.

### launchd (macOS)

For macOS operators, launchd plists at `~/Library/LaunchAgents/`. The framework does not write these. Operator creates them per Apple's launchd documentation.

## v0.2 placeholder

When v0.2 ships hosted scheduling, this file gains a third execution path: hosted. The operator's stack becomes truly autonomous. v0.2 will respect every event-driven agent's signal and every cadenced agent's cron expression.

## Triggering agents from inside Claude Code

For manual execution, the operator opens Claude Code in the repo root and types the manual command listed in each agent's row above. Examples:

- "Run the artefact production agent" - the orchestrator routes to `/03-execution/artefact/production.md`.
- "Draft a proposal for <prospect>" - the orchestrator routes to `/03-execution/proposal/skill.md`.
- "Tear down <competitor>" - the orchestrator routes to `/03-execution/teardown/skill.md`.

The orchestrator's routing rules (in CLAUDE.md) handle these triggers. Each command corresponds to an existing canonical skill.

## Review windows

The operator should hold a review window for each cadence:

- Daily review (5 minutes): glance at /workspace/execution/ for any new outputs from event-driven agents (proposals, nurture sequences) that need same-day action.
- Weekly review (30 minutes): all agent outputs from the week. Approve, edit, ship, or reject each.
- Quarterly review (2 hours): re-read the foundation, the artefact spec, the agent stack overview. Re-run "build my agents" if anything changed.

These are the human-in-the-loop checkpoints. They are not automated.

## Schedule freshness

This file is a snapshot. Re-run "build my agents" if:

- The operator's tooling changes (new MCPs, different cadence preferences).
- The artefact spec's cadence changes.
- A new agent enters the stack (operator extension or framework upgrade).
```

## Notes for the meta-agent writing this template

- The "Manual command" column must be the actual natural-language command the operator types. Verify against CLAUDE.md routing.
- "Next run" dates are computed from "Generated" plus cadence. Update on each meta-agent run.
- Cron expressions are illustrative. The operator owns deploying them.
- The hard rule about no auto-publish in cron is non-negotiable. Mention it explicitly.
