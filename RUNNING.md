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

**Important:** `claude` only auto-loads the framework's `CLAUDE.md` (the orchestrator) when you start it from inside the alg-os folder. If you start `claude` from your home directory or anywhere outside the repo, the orchestrator does not load and the operator commands below will not work. If you see Claude responding to "design my artefact" with generic content-creation questions instead of routing to the artefact skill, you are in the wrong directory. Exit and restart inside the repo.

### Verify the orchestrator is loaded

After permission prompts, before running any operator command, verify by typing:

> "What does CLAUDE.md say to do when I type 'design my artefact'?"

You should see Claude reference the routing rule from the orchestrator. If Claude says it does not see a CLAUDE.md or freelances a generic answer, you are in the wrong directory. Exit and restart inside the repo.

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

### Prompt: Allow web_fetch for a specific domain?

**What it asks:** "Do you want to allow Claude to fetch this content?" with options including "Yes, and don't ask again for `<domain>`."

**Pick: "Yes, and don't ask again for `<domain>`" for canonical sources.**

Canonical sources include `docs.claude.com`, `github.com/modelcontextprotocol`, the operator's own domain, the operator's competitors' domains during teardown, and any URL the operator explicitly handed to the framework. Per-domain allow saves friction across capability sync (mode 1 and mode 2), online research, and competitor teardowns.

For one-off URLs the operator wants to ingest just once, "Yes" alone is fine.

### Prompt: Allow reading files outside the repo?

**What it asks:** "Do you want to proceed with reading from `<path>`?" when the operator hands the framework a file outside the repo (e.g., a sales deck on Desktop).

**Pick: "Yes, allow reading from `<directory>` during this session."**

This grants read access to the directory for the rest of the session. Useful when the operator is going to hand multiple files from the same parent folder. Session-scoped, so it does not persist across new `claude` sessions.

### Prompt: Create or edit a file (voice.md, brand.md, etc.)

**What it asks:** "Do you want to create `voice.md`?" or "Do you want to edit `<file>`?"

**Pick: Yes, allow all edits during this session.**

The intake writes 10 foundation files to `/workspace/foundation/` plus a snapshot to `/workspace/research/`. Without session-wide allow, you are prompted 12+ times in a single intake. Session-wide grants only apply until you exit `claude`.

The framework's hard rule: writes only happen inside `/workspace/`. Framework directories at the root are read-only at runtime. Session-wide edit permission is therefore scope-limited by the framework's own rules.

### Prompt: Run a shell command (git, mkdir, etc.)

**What it asks:** "Allow Claude to run `<command>`?"

**Pick: Yes (one-time) for first-run commands. Yes, allow all sessions for repeat commands like `mkdir -p workspace`.**

The framework occasionally needs to create directories or run light shell operations. None of them touch anything outside the repo. Use judgement: if a command looks unrelated to the framework, decline and tell us in a GitHub issue.

## Attaching files in Claude Code

When the framework asks for files (intake Phase 2, proposal source material, edition data, etc.), three ways:

### 1. Drag from Finder onto the terminal

Find the file in Finder, drag it onto the Claude Code terminal window. macOS Terminal and iTerm paste the absolute path of the file as text. Hit enter, Claude reads the path.

### 2. Paste the absolute path directly

Type or paste the path: `/Users/alex88muresan/Desktop/sales-deck.pdf`. The skill reads the file.

### 3. Use `@path/to/file` shorthand

Claude Code supports `@` references with tab-completion. Type `@~/Desktop/sales-deck.pdf` and the skill reads the file.

### What if you have nothing

Tell the framework "I have nothing." It moves on without blocking. Most skills can still produce output if other inputs are available; the skill flags the gaps in the output.

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

You can now run any of the canonical skills:

- "design my artefact" - signature artefact generator (spec)
- "produce my artefact edition" - signature artefact production (edition shipping)
- "run the teardown" - competitor and positioning analysis
- "draft a proposal" - post-discovery client document
- "nurture sequence" - post-proposal email sequence

Or build the operator's full agent stack at once:

- "build my agents" - the meta-agent that produces the running stack at `/workspace/agents/`

Each skill reads `/workspace/foundation/` (and other workspace files as relevant) and produces output in `/workspace/execution/<skill>/` or `/workspace/agents/`.

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

Most common cause: `claude` was started from the wrong directory and CLAUDE.md never loaded. Verify with the test command in the "Verify the orchestrator is loaded" section above.

If CLAUDE.md is loaded but Claude is still freelancing, tell it explicitly: "Read CLAUDE.md and follow it." Then re-run your command.

If the freelancing persists, tell it specifically which skill to run: "Read /03-execution/artefact/skill.md in full and follow it." This bypasses any routing failure.

### Claude appears to be stuck (no output for 30+ seconds)

The framework's discipline rules require progress markers during long operations. If Claude has gone quiet for more than 30 seconds:

1. Wait another 30 seconds. File parsing and web scraping can take time.
2. If still silent, type "What are you doing?" Claude should report state.
3. If genuinely hung, Ctrl+C to interrupt, then say "Continue from where you were."

### The task list shows a phase as "in progress" after the work is done

Known issue (Build 1 patch 3). The task list display can lag the actual phase state. The phase IS done; the visible list just has not refreshed. The skill's actual output (in `/workspace/`) is the source of truth, not the visible task list.

## Where things live

| Path | What it is |
|---|---|
| `/CLAUDE.md` | Orchestrator. Tells Claude how to route operator commands. |
| `/foundation.md` | The full brief (sections 1 to 18). Read this if you want to understand the whole framework. |
| `/00-intake/` | Sparring layer files. The intake reads from here. |
| `/01-foundation/` | Foundation file templates. Intake fills these into `/workspace/foundation/`. |
| `/02-research/` | MCP config, agent taxonomy. |
| `/03-execution/` | The four canonical skills (artefact, teardown, proposal, nurture) plus the meta-agent (`build-my-agents`). |
| `/04-feedback/` | Feedback log templates. |
| `/capability-sync/` | Mode 1 (silent) and mode 2 (on-demand) calibration logic. |
| `/templates/` | Shared assets (PPT, email templates, doc templates). |
| `/workspace/` | YOUR content. Foundation files, generated skill outputs, research, feedback. Created at first intake. Never overwritten by `alg-upgrade`. |

## Where to give feedback

Open a GitHub issue at https://github.com/alexdailycheckin/alg-os/issues. Useful issue contents: the operator command you ran, the input you gave, the output you got, what you expected. The sparring rules and intake orchestrator improve from real failure examples.
