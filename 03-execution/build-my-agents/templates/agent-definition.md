# Agent Definition Template

Template for a single agent in the operator's stack. The meta-agent writes one of these per agent at `/workspace/agents/<agent-name>.md`.

```
# Agent - <Agent Name>

**Purpose:** <One sentence. What this agent does.>

**Funnel step:** <Step 1 / Step 3 / Step 4 / Cross-funnel>

**Status:** <active | paused | retired>

## Trigger

<One of: Cadenced | Event-driven | On-demand>

**Trigger detail:**

<For cadenced: cron expression + plain-English description.>
<For event-driven: the event signal that fires the agent (e.g., "proposal status moves to 'sent' AND no reply within 5 days").>
<For on-demand: the operator command that fires the agent (e.g., "tear down <competitor>").>

## Owner

**Human accountable:** <Name, role from team.md>
**Backup:** <Name, role>

## Mode

<Product-recursive | Tool-agnostic>

<For product-recursive: which capability of the operator's own product powers this agent.>
<For tool-agnostic: which tool from the agent taxonomy this agent uses, with a rationale referencing the operator's existing stack.>

## Inputs

### Files

- `<file path>` - <why>
- `<file path>` - <why>

### MCP data sources

- `<MCP name>` - <what data this agent reads from it>

### Operator-provided

- <What the operator hands to the agent at run time, if any>

## Skill invocation

The agent runs the canonical skill at `<skill path>`. To invoke manually:

> "<exact natural-language command the operator types in Claude Code>"

## Outputs

- `<output file path>` - <what is written>
- `<output file path>` - <what is written>

## Review logic

After the agent runs, the operator does the following before any output ships:

1. <Review action 1>
2. <Review action 2>
3. <Approval or edit step>

The agent never auto-publishes, auto-sends, or auto-commits. The operator is the human-in-the-loop.

## Run history

| Date | Outcome | Reviewer | Notes |
|---|---|---|---|
| <YYYY-MM-DD> | <success / failed / partial> | <name> | <one line> |

(Operator updates this table after each run. v0.2 will track this automatically.)

## Health

**Last successful run:** <YYYY-MM-DD>
**Next scheduled run:** <YYYY-MM-DD or "on-demand">
**Known issues:** <list, or "none">

## Notes

<Any operator-specific context. Edge cases, deal-specific behaviour, things that would surprise a future maintainer.>
```

## Notes for the meta-agent writing this template

- All bracketed placeholders must be filled before saving.
- The "Skill invocation" command must be a real command the operator can type. No abstractions.
- The "Outputs" section names actual paths under `/workspace/execution/`, not abstractions.
- The "Review logic" must be specific. "Review the output" fails. "Confirm the artefact data sourcing matches the spec, approve or edit the executive summary, ship via the distribution channels in the spec" passes.
- File name slug: lowercase, hyphenated, max 50 chars. Examples: `artefact-production-quarterly.md`, `nurture-stalled-prospects.md`, `teardown-on-demand.md`.
