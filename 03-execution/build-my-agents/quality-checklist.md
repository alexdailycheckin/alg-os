# Build My Agents - Quality Checklist

Run this checklist in Phase 6 of the meta-agent skill, before writing the agent stack to `/workspace/agents/`. If any item fails, surface to the operator and fix.

## The bar

A defensible agent stack passes all 12 items. Any failure means the stack is not ready to ship.

## Items

### 1. Every agent maps to a funnel step

No agent exists without a clear funnel step from `gtm-motion.md`. Cross-funnel agents (teardown, capability sync) explicitly say "cross-funnel."

### 2. Every agent has a human owner

From `team.md`. Owner is a real named person, not "TBD" or "the team."

### 3. Every agent has a defined trigger

Cadenced (with cron expression and plain English), event-driven (with event signal), or on-demand (with operator command). No agent has "trigger TBD."

### 4. Every agent has explicit review logic

Specific actions the operator does after the agent runs. "Review the output" fails. Three concrete steps minimum.

### 5. Mode resolution per agent matches services.md

Product-recursive agents are powered by the operator's own product where the product genuinely supports the capability. Tool-agnostic agents reference the agent taxonomy and pick a tier 1 (native), tier 2 (specialist), tier 3 (custom orchestration), or tier 4 (third-party SaaS) tool.

If an agent is product-recursive but the operator's product cannot actually power that capability today (per the capability snapshot), surface the gap and route to tier 2/3/4.

### 6. MCP requirements are realistic

Every MCP listed in `mcp-blueprint.md` is in the agent taxonomy or in current MCP registry. No invented MCPs. No connections that do not exist.

### 7. Schedule has manual fallback

The schedule.md works without any infrastructure beyond Claude Code. Manual operator invocation runs the entire stack. Cron and launchd are optional, not required for v0.1.

### 8. No agent auto-publishes

Hard rule. Every agent's output lands in `/workspace/execution/` for operator review. No agent sends emails, publishes content, or commits to systems autonomously.

### 9. Dependencies are explicit

The agent stack overview lists which agents depend on which inputs. Hidden dependencies cause silent failures. Examples: proposal-drafter depends on a discovery transcript existing; nurture depends on a proposal being marked sent.

### 10. Health metrics are operator-readable

The agent stack overview includes what the operator watches to know the stack is working. Generic metrics ("track pipeline") fail. Specific metrics ("number of proposals reviewed in the last 7 days," "artefact production cadence vs spec") pass.

### 11. v0.1 limitations are stated honestly

The agent stack overview explicitly notes that v0.1 is documentation and definitions, not autonomous infrastructure. The operator runs each agent manually until v2 ships scheduling.

If the meta-agent claims v0.1 is autonomous, that is dishonest and fails the bar.

### 12. The four-step funnel still works end to end

The agent stack covers all four steps that have agents (1, 3, 4 if applicable, plus cross-funnel agents). The operator can trace a prospect from artefact reach to deployment using only agents in this stack.

If a step has no agent and that step is part of the operator's motion, surface the gap.

## Documented exceptions

The operator can override an item with explicit acceptance. Document the override at the top of `agent-stack.md` under "Accepted exceptions." Examples:

- "Item 5: agent X is product-recursive even though the product does not yet fully support the capability. Operator chose to keep the agent product-recursive and gap-fill via manual work until product capability ships. Accepted."
- "Item 11: operator already has cron set up and considers v0.1 autonomous on their end. Accepted."

Operators can override at most 2 items. If 3 or more fail, the stack is not ready. Re-run the relevant phases.

## What to do when the bar fails

Surface the failures to the operator:

> "The agent stack fails 4 items: 1, 5, 8, 9. Most load-bearing failure is item 8 (the proposal-drafter agent's review logic does not have an explicit operator approval step before send). Fix in this order: 8, 9, 5, 1. Confirm fixes and I re-run the checklist."

Do not soften. The agent stack runs the operator's motion. Weak agents produce weak outputs at scale.
