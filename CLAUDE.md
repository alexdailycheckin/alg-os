# ALG OS - Orchestrator

**READ THIS FILE BEFORE RESPONDING TO ANY OPERATOR MESSAGE.**

This is the routing layer for the ALG OS framework. Operator commands MUST be routed via the table in the "Operator commands" section below. **Do not respond with generic clarifying questions to messages that match a routing pattern.** Do not freelance content (slide decks, one-pagers, generic copy) when the operator is asking for an ALG OS skill output. The framework defines the work; this file routes the request.

If you cannot determine which skill applies, ask "Which skill are you trying to run?" and list the available commands. Do not default to generic-assistant behaviour.

The full brief lives in `foundation.md`.

## What ALG OS is

Agent-Led Growth Operating System. A brand-neutral, tool-agnostic framework for building outreach machines where unit economics improve quarter on quarter because artefacts and data compound.

## Framework vs workspace

The repo splits into two halves.

**Framework directories** at the root contain logic, prompts, and templates. They ship with the canonical repo and are overwritten on `alg-upgrade`. Never write generated content into framework directories.

**`/workspace/`** holds operator content. Foundation files, generated artefacts, research outputs, feedback logs. Always write operator output here. If `/workspace/` does not exist, the first-run intake creates it from `/01-foundation/` templates.

## Operator commands

Match the operator's message against the patterns below. Be permissive: tolerate British and American spelling variants ("artefact"/"artifact"), synonyms (design/build/create/make/produce/generate), and natural paraphrasing. If the operator's message contains a recognised noun (intake / artefact / teardown / proposal / handoff / nurture) plus any verb implying action, route to the matching skill. Do NOT ask generic clarifying questions about format, audience, or content. Those questions live inside the skill flows.

| Operator triggers (any of) | Action |
|---|---|
| "run intake", "set me up", "I want to start", "start me up", "set up my foundation", "onboard me" | Read `/00-intake/intake.md` in full and follow it. The intake orchestrates voice calibration, capability sync mode 1, file ingestion, online research, interactive intake (using `/00-intake/questionnaire.md` and `/00-intake/sparring-rules.md`), coherence check, and writes to `/workspace/foundation/` using `/01-foundation/` templates. |
| Any message containing "artefact" or "artifact" plus a design or spec verb (design, build, spec, plan, develop, work on, help with) and not yet referencing an existing spec | Read `/03-execution/artefact/skill.md` in full and follow it. Six-phase flow: fit diagnostic, three candidates, operator picks one, full spec, quality checklist, edition-1 branch. Reads from `/workspace/foundation/` and `/workspace/research/capability-snapshot.md`. Writes spec to `/workspace/execution/artefact/<slug>-spec.md`. **Do not ask the operator what format the artefact is or who the audience is. Those are inside the skill flow.** |
| "produce my artefact edition", "produce edition <N>", "ship edition <N>", "run the artefact production", "publish the artefact" | Read `/03-execution/artefact/production.md` in full and follow it. Nine-phase flow: spec validation, data ingestion, analysis, drafting, voice and quality, distribution-ready formats, methodology, quality checklist, hand-off. Reads spec from `/workspace/execution/artefact/<slug>-spec.md`. Writes edition to `/workspace/execution/artefact/<slug>-edition-<NN>/`. Refuses to run if spec is missing. |
| "build my agents", "build my agent stack", "set up my agents", "automate my motion", "build my stack" | Read `/03-execution/build-my-agents/skill.md` in full and follow it. Seven-phase flow: map funnel to canonical skills, define each agent, MCP blueprint, schedule, stack overview, quality checklist, hand-off. Reads from `/workspace/foundation/`, `/workspace/execution/artefact/<slug>-spec.md`, `/workspace/research/capability-snapshot.md`, and `/02-research/agent-taxonomy.md`. Writes to `/workspace/agents/`. Refuses to run if foundation, artefact spec, or capability snapshot is missing. |
| "run the <agent name> agent" (where the agent exists in `/workspace/agents/`) | Read `/workspace/agents/<agent-name>.md` in full. Follow the agent's "Skill invocation" command, which routes to the underlying canonical skill. Update the agent's "Run history" table after completion. |
| "run the teardown", "competitor analysis", "tear down a competitor", "competitor positioning" | Read `/03-execution/teardown/skill.md` in full and follow it. Eight-phase flow: scrape, categorise claims, infer ICP, head-to-head, weak spots, recommendations, the wedge, write. Reads from `/workspace/foundation/`. Writes to `/workspace/execution/teardown/`. |
| "draft a proposal", "post-discovery doc", "write a proposal", "client proposal", "proposal for <client>" | Read `/03-execution/proposal/skill.md` in full and follow it. Five-phase flow: extract from discovery, fit check, recommend engagement, draft, quality checklist. Reads from `/workspace/foundation/`. Writes to `/workspace/execution/proposal/`. |
| "nurture sequence", "post-proposal emails", "follow-up sequence", "reactivate this prospect" | Read `/03-execution/nurture/skill.md` in full and follow it. Four-phase flow: diagnose stall, map to sequence shape, write, quality checklist. Reads from `/workspace/foundation/`. Writes to `/workspace/execution/nurture/`. |
| "what's new", "any platform updates", "capability sync", "what changed since last time" | Run capability sync mode 2 from `/capability-sync/mode-2-resync.md`. |
| "alg upgrade", "upgrade the framework", "pull the latest" | Tell the operator to run `./alg-upgrade` from terminal. |

## Routing rules

1. Always check the operator's message against the table above BEFORE generating any response. Routing is the first thing you do.
2. If a message matches multiple patterns, ask the operator which skill they meant. Do not silently pick one.
3. If a message does not match any pattern, ask "Which skill are you trying to run? Available skills: intake, artefact, teardown (pending), proposal (pending), handoff (pending), nurture (pending), capability sync." Do not default to generic-assistant behaviour.
4. Once routed, READ THE SKILL FILE IN FULL before producing any output. Skill files contain the complete flow; do not improvise around them.
5. Never offer features that are not in the framework spec. If the operator asks for something out of scope (scheduled background runs, external integrations not in the agent taxonomy, capabilities not in the current build status above), say so and stop. Do not freelance v2 features as if they exist in v1.

## Voice rules

Before generating any output for the operator, read `/workspace/foundation/voice.md`. That file is the source of truth for English variant, banned words, paragraph length, and tone. If the file does not exist (pre-intake), default to the rules in `foundation.md` section 18.

## Quality bar

Every skill enforces a quality checklist before completion. Skills that do not meet their checklist do not return output. They flag the gap and ask for what they need.

The intake refuses weak inputs. Apply the same quality bar to inferred content from file uploads and online research, not just to direct operator answers.

## Status

This repo implements the spec in `foundation.md` (v0.4).

- **Build 1 (sparring layer + foundation templates + capability sync v1):** v0.1 complete. The `run intake` command is fully wired and produces foundation files. Validated end to end on a real operator. Six known patches in the queue.
- **Build 2 (canonical execution skills):** v0.3 complete. Four canonical skills are wired: artefact (spec + edition production), teardown, proposal, nurture. Handoff was demoted from canonical (situational, not universal) and operators with delivery teams write their own in `/workspace/execution/handoff/`.
- **Build 3 v0.1 (build my agents):** complete. The meta-agent at `/03-execution/build-my-agents/` ingests foundation + artefact spec + capability snapshot + agent taxonomy and produces the operator's running agent stack as definitions, MCP blueprint, and schedule at `/workspace/agents/`. v0.1 ships documentation and definitions, not autonomous infrastructure - the operator runs each agent manually until v0.2 ships scheduling. Honest scope flag: this is not yet autonomous; it is a packaged motion the operator can run at the cadence the framework defines.
- **alg-upgrade:** stub. Manual `git pull` works for now.
