# Build My Agents - Meta-Agent Orchestrator

This file runs when the operator says "build my agents," "build my agent stack," "set up my agents," "automate my motion," or any equivalent.

The meta-agent constructs the operator's running agent stack. It reads the operator's foundation, the artefact spec, the capability snapshot, and the agent taxonomy. It produces working agent definitions, an MCP connection blueprint, and a schedule that runs the operator's four-step funnel autonomously.

Read in full before doing anything else.

## What v0.1 ships

The meta-agent v0.1 produces the operator's agent stack as documentation and agent definition files. It does not yet schedule or run agents autonomously. The operator runs each agent themselves (via Claude Code or Claude Desktop) on the schedule defined.

v2 will add scheduling infrastructure (cron, launchd, hosted scheduler, GitHub Actions). v0.1 is honest about what ships: a packaged motion the operator can run manually until v2 lands.

## What this skill produces

A complete agent stack at `/workspace/agents/` that includes:

- `agent-stack.md` - the system map. Lists every agent in the operator's stack, their purpose, their interconnections, the four-step funnel mapping.
- `mcp-blueprint.md` - all MCP connections required across the stack. What the operator already has, what they need to add.
- `schedule.md` - the schedule for cadenced agents (artefact production, capability sync). The trigger logic for event-driven agents.
- `<agent-name>.md` - one definition file per agent. Each defines trigger, inputs, the canonical skill it invokes, outputs, review logic.

## Inputs the skill reads

| File | Why |
|---|---|
| `/workspace/foundation/voice.md` | All output uses the operator's voice. |
| `/workspace/foundation/services.md` | Mode (product-recursive vs tool-agnostic) drives which agents run on the operator's own product vs recommended tools. |
| `/workspace/foundation/icp.md` | The agents serve this ICP. |
| `/workspace/foundation/personas.md` | The buying-committee shape drives event triggers (proposal sent, prospect quiet, champion engaged). |
| `/workspace/foundation/positioning.md` | The win axis informs which agents are highest-leverage. |
| `/workspace/foundation/team.md` | Owners. Each agent has a human owner who reviews outputs before they ship. |
| `/workspace/foundation/gtm-motion.md` | The four-step funnel. Each agent maps to one of the four steps. |
| `/workspace/execution/artefact/<slug>-spec.md` | The artefact production agent runs against this spec. |
| `/workspace/research/capability-snapshot.md` | Current platform reality. The agent stack respects what is and is not natively available. |
| `/02-research/agent-taxonomy.md` | The catalogue. Tier resolution per agent capability. |

If any input is missing, refuse to run. Tell the operator what is missing and which step (intake, artefact spec) needs to be completed first.

## Operator inputs

Ask:

1. **Confirm the four-step funnel.** Read `gtm-motion.md` back to the operator in one paragraph. Confirm this is still the motion. If the operator wants to revise, route to intake or the artefact skill.
2. **Confirm the operator's tooling reality.** Which MCPs are connected today (Fireflies, Slack, M365, Gmail, Calendar, Drive, Airtable, monday.com, plus anything else)? Which third-party tools does the operator already pay for? This shortens the "tools you need to add" list.
3. **Confirm the operator's review cadence.** How often do they want to review agent outputs? Weekly is the v0.1 default. Daily is also supported. Less than weekly tends to surface stale outputs.

## Flow

### Phase 1 - Map the four-step funnel to canonical skills

Read `gtm-motion.md`. Produce the mapping:

| Funnel step | Canonical skill | Agent type |
|---|---|---|
| Step 1 - Signature artefact | Artefact production | Cadenced (per spec's cadence) |
| Step 2 - Buyer asks the question | None (buyer's action) | N/A |
| Step 3 - Low-commitment first step | Proposal | Event-triggered (qualified prospect) |
| Step 4 - Full deployment | Proposal + Handoff (if operator has a delivery team) | Event-triggered (deal moves) |
| Cross-funnel | Teardown | On-demand |
| Cross-funnel | Nurture | Event-triggered (proposal sent and quiet) |
| Cross-funnel | Capability sync mode 2 | Cadenced (quarterly default) |

Every operator gets some version of this mapping. The shape is universal; the components are specific.

### Phase 2 - Define each agent

For each agent in the mapping, produce a definition file at `/workspace/agents/<agent-name>.md`. Use the template at `/03-execution/build-my-agents/templates/agent-definition.md`.

Each agent definition includes:

- **Purpose.** What this agent does in one sentence.
- **Funnel step.** Which step it serves.
- **Trigger.** Cadenced (with frequency), event-driven (with event signal), or on-demand.
- **Owner.** Human accountable. Sourced from `team.md`.
- **Inputs.** Files it reads, MCP data sources, operator-provided data.
- **Skill invocation.** Which canonical skill it runs.
- **Outputs.** Files it writes to `/workspace/execution/`.
- **Review logic.** What the operator does after the agent runs (review, approve, edit, reject, ship).
- **Mode.** Product-recursive (powered by operator's own product) or tool-agnostic (recommended tool from agent taxonomy). Per `services.md`.
- **MCP requirements.** Connections this agent needs.

Default agents in v0.1:

1. `artefact-production-<cadence>.md` - runs the artefact production skill on the spec's cadence. Quarterly by default for pattern A.
2. `proposal-drafter.md` - runs the proposal skill when the operator triggers it after a discovery call.
3. `teardown-on-demand.md` - runs the teardown skill when the operator triggers it for a named competitor.
4. `nurture-stalled-prospects.md` - runs the nurture skill when the operator marks a proposal as stalled.
5. `capability-sync-quarterly.md` - runs capability sync mode 2 every 90 days.

The meta-agent extends or contracts this default list based on the operator's foundation. Operators with a delivery team also get a handoff agent.

### Phase 3 - MCP blueprint

Read `/02-research/agent-taxonomy.md` and the capability snapshot. For each agent in Phase 2, list:

- The MCP connections it needs.
- Whether the operator already has them (from operator confirmation in Phase 0).
- For missing connections, name 2 to 3 alternatives from the agent taxonomy.

Write `/workspace/agents/mcp-blueprint.md` using the template at `/03-execution/build-my-agents/templates/mcp-blueprint.md`. The blueprint is operator-controlled. The framework recommends, the operator connects.

### Phase 4 - Schedule

Read each agent's trigger. Compile the schedule.

| Trigger type | Schedule format |
|---|---|
| Cadenced | Cron-like syntax + plain-English description (e.g., "first Monday of every quarter at 9:00 GMT") |
| Event-driven | Event signal description (e.g., "proposal status field in CRM moves to 'sent' AND no reply within 5 days") |
| On-demand | Operator command in Claude Code (e.g., "tear down <competitor>") |

Write `/workspace/agents/schedule.md` using the template at `/03-execution/build-my-agents/templates/schedule.md`. Include three execution paths:

1. **Manual (v0.1 default).** Operator runs each agent in Claude Code on the schedule. Lowest friction, no scheduling infrastructure.
2. **Cron / launchd (operator-set-up).** For operators comfortable with cron or macOS launchd, the schedule.md provides the cron expressions and launchd plists.
3. **Hosted scheduling (v2 placeholder).** Will be filled in when v2 ships hosted scheduling.

### Phase 5 - Stack overview

Write the system map at `/workspace/agents/agent-stack.md` using the template at `/03-execution/build-my-agents/templates/agent-stack.md`. The stack overview includes:

- One-paragraph narrative of how the operator's motion runs autonomously.
- Funnel-step diagram (text-based).
- Agent list with one-line per agent.
- Dependencies (e.g., proposal drafter depends on the artefact existing in /workspace/execution/artefact/).
- The operator's review responsibilities (the human-in-the-loop checkpoints).
- Health metrics (what to watch to know the stack is working).

### Phase 6 - Quality checklist

Run the checklist at `/03-execution/build-my-agents/quality-checklist.md`. Surface failures. Fix before writing to `/workspace/agents/`.

### Phase 7 - Hand-off

Tell the operator:

> "Agent stack saved to `/workspace/agents/`. Files:
> - `agent-stack.md` (the system map - read this first)
> - `mcp-blueprint.md` (MCP connections to set up)
> - `schedule.md` (when each agent runs)
> - `<agent>.md` x N (one definition per agent)
>
> Next steps:
> 1. Connect any MCPs in `mcp-blueprint.md` you do not already have.
> 2. Set up scheduling per `schedule.md` (manual via Claude Code is fine for v0.1).
> 3. Run each agent at least once to test (commands listed in each agent's definition).
> 4. Review outputs at the cadence you set in Phase 0.
>
> When v2 ships hosted scheduling, your stack picks it up via `alg-upgrade` without rework."

Do not auto-run agents. Operator decides next.

## Hard rules

- Apply voice rules from `voice.md` to every operator-facing message.
- Refuse to run if foundation files, artefact spec, or capability snapshot are missing.
- Never invent MCP connections. Use only those listed in the agent taxonomy.
- Never auto-schedule agents in v0.1. The operator runs them manually until v2.
- Honour the framework vs workspace split. Write only to `/workspace/agents/`. Never modify framework directories.
- The operator owns the human-in-the-loop. Every agent has explicit review logic. No agent ships output without operator review.
- Mode resolution per agent (product-recursive vs tool-agnostic) follows the operator's `services.md`. Do not silently swap modes.

## What v0.2+ will add

Honest scope flags so the operator knows what is missing today.

- v0.2: hosted scheduling. The stack runs autonomously without operator manual invocation.
- v0.2: agent observability. Per-agent run history, success rate, review queue depth.
- v0.2: agent extension framework. Operators can write their own agents in `/workspace/agents/custom/` using the same definition template.
- v0.3: agent dashboard. Operator-facing UI summarising stack status and pending reviews.

## Hand-off integration

The meta-agent's outputs become the operating manual for the operator's motion. Future framework upgrades (`alg-upgrade`) will check the agent definitions and recommend updates when:

- A canonical skill upgrade changes input/output shape.
- A new MCP connection becomes available that an agent could benefit from.
- The agent taxonomy updates a tier (e.g., Claude ships native voice, voice-related agents shift from tier 2 to tier 1).

These updates are surfaced via capability sync mode 2 and applied via `alg-upgrade`.
