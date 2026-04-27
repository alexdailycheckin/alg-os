# Agent Stack Template

Template for the operator's full agent stack overview. The meta-agent writes this to `/workspace/agents/agent-stack.md`. It is the system map. Operators read this first.

```
# Agent Stack - <Operator Name>

**Generated:** <YYYY-MM-DD>
**ALG OS version:** <semver from CHANGELOG.md>
**Mode:** <Product-recursive | Tool-agnostic>

## How your motion runs

<3 to 5 sentences. Plain-English narrative of how the operator's four-step funnel runs autonomously. Names each agent, when it fires, what it produces. The paragraph the operator can repeat to a co-founder, board member, or hire to explain the system.>

## Funnel-step diagram

```
Step 1: Signature artefact (cadenced)
   └── <artefact-production agent name> runs <cadence>
        ↓ produces /workspace/execution/artefact/<slug>-edition-<NN>/
        ↓ operator reviews and ships

Step 2: Buyer reads the artefact
   └── (buyer's action; not autonomous)
        ↓ buyer asks the natural next question
        ↓ buyer engages with operator (inbound, demo request, etc.)

Step 3: Low-commitment first step
   └── <proposal-drafter agent name> runs on event
        ↓ produces /workspace/execution/proposal/<prospect-slug>-proposal.md
        ↓ operator reviews and sends

Step 4: Full deployment
   └── <handoff agent name, if applicable> runs on event
        ↓ produces /workspace/execution/handoff/<client-slug>-handoff.md
        ↓ delivery team executes

Cross-funnel: positioning sharpness
   └── <teardown agent name> runs on demand
        ↓ produces /workspace/execution/teardown/<competitor-slug>-teardown.md

Cross-funnel: deal recovery
   └── <nurture agent name> runs on event
        ↓ produces /workspace/execution/nurture/<prospect-slug>-nurture-sequence.md

Cross-funnel: platform calibration
   └── <capability-sync agent name> runs <cadence>
        ↓ updates /workspace/research/capability-snapshot.md
```

## Agents

| Agent | Funnel step | Trigger | Owner | Definition |
|---|---|---|---|---|
| <Agent 1> | Step 1 | Cadenced (<cadence>) | <Owner> | `<file>.md` |
| <Agent 2> | Step 3 | Event-driven | <Owner> | `<file>.md` |
| ... | ... | ... | ... | ... |

## Dependencies

Some agents depend on outputs from others. The dependency graph below tells the operator what must run first.

- `<artefact-production agent>` depends on the artefact spec at `/workspace/execution/artefact/<slug>-spec.md` existing.
- `<proposal-drafter agent>` depends on a discovery transcript existing for the prospect.
- `<nurture agent>` depends on a proposal having been sent (the agent is event-triggered by stall).
- All agents depend on the foundation files in `/workspace/foundation/` being current.

## Operator review responsibilities

The human-in-the-loop checkpoints. Every agent has these.

| Agent | What you review | Cadence |
|---|---|---|
| <Agent 1> | <specific review action> | <weekly / per-run / monthly> |
| ... | ... | ... |

## Health metrics

What to watch to know the stack is working.

- **Foundation freshness.** Are `/workspace/foundation/` files reviewed at least quarterly?
- **Artefact cadence.** Is the artefact production agent shipping editions on the cadence the spec defined?
- **Pipeline-to-artefact link.** Are inbound prospects citing the artefact in early conversations? If not, distribution is weak.
- **Agent run history.** Each agent definition has a run-history table. Sparse history suggests the operator is not invoking the agent on cadence.
- **Review queue depth.** How many agent outputs are sitting unreviewed? Anything over a week is a backlog.

## When to upgrade

Run `alg-upgrade` when:

- Capability sync mode 2 surfaces material changes (Claude ships a capability that affects an agent currently routed to a third-party tool, MCP ships a connector for a data source you use, a canonical skill upgrade changes output shape).
- The framework version in `CHANGELOG.md` advances.

After upgrading, re-read `agent-stack.md` for any auto-generated update notes (the meta-agent rewrites this file when run again).

## When to re-generate the stack

Re-run "build my agents" when:

- The foundation changes materially (new ICP, new positioning, new pricing, new mode).
- The artefact spec changes.
- The operator's tooling reality changes (new MCP connections, different third-party tools).
- Quarterly health check (a regular re-build keeps the stack current with capability sync findings).

## v0.1 limitations

The agent stack v0.1 is documentation and definitions, not running infrastructure. The operator runs each agent manually via Claude Code. v0.2 ships hosted scheduling.

Until then, the operator's job is to:

1. Read this stack overview.
2. Connect the MCPs in `mcp-blueprint.md`.
3. Run each agent at the cadence in `schedule.md` (manually, in Claude Code).
4. Review outputs before they ship.

This is enough to get value from the framework today. v0.2 makes it autonomous.
```

## Notes for the meta-agent writing this template

- The funnel-step diagram must reflect the operator's actual agents, not generic placeholders.
- Health metrics must be specific to this operator. Generic metrics like "track pipeline" fail.
- The "How your motion runs" paragraph is the most important piece. It is the operator's elevator pitch for their own automated system.
- Dependencies must be explicit. Hidden dependencies cause silent failures.
