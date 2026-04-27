# RUNNING - Operator Quickstart

How to fork, install, and run ALG OS as an operator. Written for non-technical operators. No assumed knowledge of Claude Code, MCPs, or git internals.

If you have used Claude Code before and just want to run intake, the short version is: `git clone`, `cd`, `claude`, accept the permission prompts (recommended answers below), say "run intake."

## Prerequisites

You need three things before starting.

1. **A computer running macOS or Linux.** Windows works via WSL but is not the supported path in v1.

2. **Claude Code CLI.** The terminal interface ALG OS runs in. Install with:

   ```
   npm install -g @anthropic-ai/claude-code
   ```

   If `npm` itself is missing, install Node.js first from https://nodejs.org.

3. **Git.** Comes pre-installed on macOS. On Linux, `sudo apt install git` or your package manager equivalent.

## First-time setup

```
git clone https://github.com/<your-fork>/alg-os.git
cd alg-os
claude
```

When `claude` starts inside the folder, you will hit a sequence of permission prompts. The next section covers each one.

## Permission prompts and what to pick

ALG OS uses Claude Code's standard permission system. The prompts are normal and expected. Recommended answers below.

### Prompt: Trust the files in this folder?

**What it asks:** "Do you trust the files in this folder?"

**Pick: Yes, allow all sessions.**

Per-folder grant, not global. You reviewed (or wrote) the files when you forked, so this is safe. "Yes" alone works too but you will be re-prompted every time you `cd` back in. "No" blocks Claude from reading the framework and breaks intake.

### Prompt: Initialise a CLAUDE.md?

**What it asks:** Claude Code may offer to run `/init` and auto-generate a `CLAUDE.md` based on the codebase.

**Pick: No / Skip.**

ALG OS ships with a hand-crafted `CLAUDE.md` that orchestrates the framework. Auto-init would either overwrite it or layer generic docs on top, both of which break the orchestrator. Decline.

### Prompt: Allow tool access (web_fetch, web_search)?

**What it asks:** "Allow Claude to use the web_fetch tool?" or similar.

**Pick: Yes, allow all sessions.**

The framework runs `web_fetch` during capability sync (calibration to current Anthropic platform state) and `web_search` during online research (Phase 3 of intake). Without these, intake still completes but produces weaker output and capability sync falls back to "live calibration unavailable."

### Prompt: Create or edit a file (voice.md, brand.md, etc.)

**What it asks:** "Do you want to create `voice.md`?" or "Do you want to edit `<file>`?"

**Pick: Yes, allow all edits during this session.**

The intake writes 10 foundation files to `/workspace/foundation/` plus a snapshot to `/workspace/research/`. Without session-wide allow, you are prompted 12+ times in a single intake. Session-wide grants only apply until you exit `claude`.

The framework's hard rule: writes only happen inside `/workspace/`. Framework directories at the root are read-only at runtime. Session-wide edit permission is therefore scope-limited by the framework's own rules.

### Prompt: Run a shell command (git, mkdir, etc.)

**What it asks:** "Allow Claude to run `<command>`?"

**Pick: Yes (one-time) for first-run commands. Yes, allow all sessions for repeat commands like `mkdir -p workspace`.**

The framework occasionally needs to create directories or run light shell operations. None of them touch anything outside the repo. Use judgement: if a command looks unrelated to the framework, decline and tell us in a GitHub issue.

## Running intake

In the `claude` chat, say:

- "run intake"
- "set me up"
- "I want to start"
- or any equivalent

The orchestrator follows eight phases.

| Phase | What happens |
|---|---|
| 0 - Voice calibration | British or American English. One question, sets voice for everything downstream. |
| 1 - Capability sync | Silent. Reads Anthropic docs and MCP registry, calibrates the framework to current state. You see nothing here unless something is materially wrong. |
| 2 - File ingestion | You drop in existing brand, ICP, sales, or strategy docs. PDFs, Word, PowerPoint, markdown, plain text, CSV all accepted. Skip if you have nothing. |
| 3 - Online research | You provide your website URL, LinkedIn page, competitor sites. Claude scrapes and extracts signal. Skip if you have nothing public. |
| 4 - Interactive intake | Nine sections plus voice (Brand, Services, ICP, Personas, Positioning, Markets, Team, Pricing, GTM motion). Sparring layer refuses weak answers. |
| 5 - Coherence check | Cross-validates everything. Surfaces contradictions for you to fix before files get written. |
| 6 - GTM motion synthesis | You articulate your motion in one paragraph. This is the proof intake is complete. |
| 7 - Foundation files written | All 10 files appear in `/workspace/foundation/`. |
| 8 - Hand-off | Tells you what skills you can run next. Build 2 dependent. |

Total time depends on input quality and preparation. Plan for one focused session, or split across two or three sittings. The framework does not gate progression on time. The bar is output quality.

## After intake

Once Build 2 ships, you can say:

- "design my artefact" - signature artefact generator
- "run the teardown" - competitor and positioning analysis
- "draft a proposal" - post-discovery client document
- "write the handoff" - internal solutions team brief
- "nurture sequence" - post-proposal email sequence

Each skill reads `/workspace/foundation/` and produces output in `/workspace/execution/<skill>/`. Build 2 is in progress. Until then, the foundation produced by intake is the deliverable.

## Upgrading

When new framework versions ship:

```
./alg-upgrade
```

This pulls latest framework files. Workspace is never touched. Implementation pending Build 3, until then manual `git pull` works (review diffs first).

## Common issues

### "claude: command not found"

Claude Code CLI is not installed. Run `npm install -g @anthropic-ai/claude-code`. If `npm` is missing, install Node.js first from https://nodejs.org.

### Permission denied on git push

Your local git is authenticated as a different GitHub account than the one that owns the fork. Easiest fix: install the GitHub CLI (`brew install gh`) and run `gh auth login`. Pick HTTPS, "Login with a web browser," and sign in to the right account when prompted.

### Capability sync fails or skips

If `web_fetch` is blocked or unavailable, capability sync mode 1 falls back to "live calibration unavailable, defaults in use." Intake still completes. Skills will use the framework's shipped agent taxonomy without runtime adjustment.

### Foundation files feel too generic

The sparring layer refused too few weak inputs. Either re-run intake giving sharper answers, or edit specific files manually in `/workspace/foundation/`. If the same kind of weak output keeps slipping through, open a GitHub issue with the example. The sparring rules in `/00-intake/sparring-rules.md` can be sharpened.

### File written outside /workspace/

Framework violation. Open a GitHub issue immediately with the file path and the operator command that triggered it. The framework should never write outside `/workspace/`.

### Claude is freelancing instead of following CLAUDE.md

Tell Claude explicitly: "Read CLAUDE.md and follow it." Then re-run your command. If this keeps happening, your `CLAUDE.md` may have been altered or the session may not have loaded it. Restart `claude` from the repo root.

## Where things live

| Path | What it is |
|---|---|
| `/CLAUDE.md` | Orchestrator. Tells Claude how to route operator commands. |
| `/foundation.md` | The full brief (sections 1 to 18). Read this if you want to understand the whole framework. |
| `/00-intake/` | Sparring layer files. The intake reads from here. |
| `/01-foundation/` | Foundation file templates. Intake fills these into `/workspace/foundation/`. |
| `/02-research/` | MCP config, agent taxonomy. |
| `/03-execution/` | The five canonical skills. (Build 2 in progress.) |
| `/04-feedback/` | Feedback log templates. |
| `/capability-sync/` | Mode 1 (silent) and mode 2 (on-demand) calibration logic. |
| `/templates/` | Shared assets (PPT, email templates, doc templates). |
| `/workspace/` | YOUR content. Foundation files, generated skill outputs, research, feedback. Created at first intake. Never overwritten by `alg-upgrade`. |

## Where to give feedback

Open a GitHub issue at https://github.com/alexdailycheckin/alg-os/issues. Useful issue contents: the operator command you ran, the input you gave, the output you got, what you expected. The sparring rules and intake orchestrator improve from real failure examples.
