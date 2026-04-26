# ALG OS - Orchestrator

This file tells Claude how to behave when an operator opens this repo in Claude Desktop or Claude Code. The full brief lives in `foundation.md`.

## What ALG OS is

Agent-Led Growth Operating System. A brand-neutral, tool-agnostic framework for building outreach machines where unit economics improve quarter on quarter because artefacts and data compound.

## Framework vs workspace

The repo splits into two halves.

**Framework directories** at the root contain logic, prompts, and templates. They ship with the canonical repo and are overwritten on `alg-upgrade`. Never write generated content into framework directories.

**`/workspace/`** holds operator content. Foundation files, generated artefacts, research outputs, feedback logs. Always write operator output here. If `/workspace/` does not exist, the first-run intake creates it from `/01-foundation/` templates.

## Operator commands

Recognise these natural-language patterns and route accordingly.

| Operator says | Action |
|---|---|
| "run intake", "set me up", "I want to start" | Read `/00-intake/intake.md` in full and follow it. The intake orchestrates voice calibration, capability sync mode 1, file ingestion, online research, interactive intake (using `/00-intake/questionnaire.md` and `/00-intake/sparring-rules.md`), coherence check, and writes to `/workspace/foundation/` using `/01-foundation/` templates. |
| "design my artefact", "run the artefact skill" | Read `/03-execution/artefact/`. Read `/workspace/foundation/` and `/workspace/research/capability-snapshot.md`. Output to `/workspace/execution/artefact/`. (Skill body pending Build 2.) |
| "run the teardown", "competitor analysis" | Read `/03-execution/teardown/`. Same input/output pattern. (Pending Build 2.) |
| "draft a proposal", "post-discovery doc" | Read `/03-execution/proposal/`. Same pattern. (Pending Build 2.) |
| "write the handoff", "brief the solutions team" | Read `/03-execution/handoff/`. Same pattern. (Pending Build 2.) |
| "nurture sequence", "post-proposal emails" | Read `/03-execution/nurture/`. Same pattern. (Pending Build 2.) |
| "what's new", "any platform updates" | Run capability sync mode 2 from `/capability-sync/mode-2-resync.md`. |
| "alg upgrade" | Tell the operator to run `./alg-upgrade` from terminal. |

## Voice rules

Before generating any output for the operator, read `/workspace/foundation/voice.md`. That file is the source of truth for English variant, banned words, paragraph length, and tone. If the file does not exist (pre-intake), default to the rules in `foundation.md` section 18.

## Quality bar

Every skill enforces a quality checklist before completion. Skills that do not meet their checklist do not return output. They flag the gap and ask for what they need.

The intake refuses weak inputs. Apply the same quality bar to inferred content from file uploads and online research, not just to direct operator answers.

## Status

This repo implements the spec in `foundation.md` (v0.4).

- **Build 1 (sparring layer + foundation templates + capability sync v1):** v0.1 complete. The `run intake` command is fully wired and produces foundation files. Refinement pending real-operator usage.
- **Build 2 (five canonical execution skills):** not started. Skill commands above return "not yet built."
- **Build 3 (tool-agnostic layer, recommendation engine, self-serve readiness):** not started.
- **alg-upgrade:** stub. Manual `git pull` works for now.
