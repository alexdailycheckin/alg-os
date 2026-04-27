# Intake - Master Orchestrator

This file runs when the operator says "run intake," "set me up," "I want to start," or any equivalent. It is the entry point for the whole framework. Read this in full before doing anything else.

## What intake produces

Intake produces a coherent set of foundation files inside `/workspace/foundation/`, calibrated to current platform reality, defensible enough to run Build 2 skills against without rework. That is the bar.

Foundation files produced:

- `voice.md` (English variant, banned words, paragraph rules, tone)
- `brand.md` (what the operator does, mission, one-line summary)
- `services.md` (what they sell, format, delivery model)
- `icp.md` (named vertical, revenue band, trigger event, one named pain)
- `personas.md` (buying committee, decision-maker, blocker, champion)
- `positioning.md` (measurable differentiation, not adjectives)
- `markets.md` (geographies, verticals, named segments)
- `team.md` (key people, roles, who owns what)
- `pricing.md` (structure, anchor points, ranges)
- `gtm-motion.md` (the four-step funnel pattern instantiated for this operator)

`gtm-motion.md` is the proof of completion. If the operator cannot articulate their motion in one paragraph at the end, intake has not finished.

## Flow

Run these phases in order. Do not skip phases. Do not start Phase 4 (interactive) before Phase 2 (uploads) and Phase 3 (research) have produced what they can.

### Phase 0 - Voice calibration

First question to the operator, before anything else:

> "British English or American English for all output? Pick one. This sets the voice for every skill that runs after intake."

Write the answer to `/workspace/foundation/voice.md` immediately, using the template in `/01-foundation/voice.md`. All subsequent output (yours and downstream skills) reads this file before generating.

### Phase 1 - Capability sync mode 1

Before asking the operator anything else, run capability sync mode 1 silently. Read `/capability-sync/mode-1-calibration.md` and execute. This calibrates the agent taxonomy and recommendation defaults to current platform reality. Writes a snapshot to `/workspace/research/capability-snapshot.md`.

The operator does not see a release log. They see a framework that knows what is currently available.

### Phase 2 - File ingestion

Ask the operator:

> "If you have existing brand, ICP, positioning, sales, or strategy documents, point me at them. Three ways: drag the file from Finder onto this terminal window (the path will paste in), paste the absolute path directly, or reference with `@path/to/file`. PDFs, Word, PowerPoint, markdown, plain text, and CSV are accepted. If you have nothing, say so and we move on. Existing artefacts are more authoritative than recall, so we go through them first."

For each file referenced, parse it and extract structured signal toward the foundation files. Emit a short progress line per file ("Reading <filename>, extracting brand and ICP signals..."). Hold the extracted content in working memory. Do not write to `/workspace/foundation/` yet. Reflect back what you understood and ask the operator to confirm or correct before moving on.

### Phase 3 - Online research

Ask the operator:

> "Give me your website URL, your LinkedIn company page, and any industry press, public reviews, or competitor sites you want me to read. I will scrape, summarise, and add to context. Skip if none of these exist."

Run `web_fetch` and `web_search` against everything provided. Extract signal toward the foundation files. Cross-reference against what file ingestion produced. Note discrepancies for the operator (e.g., website says one ICP, sales deck says another).

### Phase 4 - Interactive intake

Now run the questionnaire in `/00-intake/questionnaire.md`. Two modes interleave throughout this phase.

**Free-form extraction.** If the operator volunteers context as long-form text, voice notes pasted as text, brain dumps, message threads, parse it and extract structured signal. Reflect back what you understood. Verify before writing.

**Targeted sparring.** When direct questions are needed (gaps, weak inputs, contradictions), apply the rules in `/00-intake/sparring-rules.md`. Refuse weak answers. Iterate until the answer clears the quality bar.

The sparring rules apply to inferred content from Phases 2 and 3 too. If the brand doc says "we target mid-market companies," that fails the ICP bar regardless of source. Sparring fires on origin-blind weak content.

### Phase 5 - Coherence check

Before writing the final foundation files, cross-check internally. Run through these questions:

- Does the persona buy what services.md describes?
- Does the ICP match the markets named?
- Does positioning differentiate against the competitor set the operator named?
- Does pricing fit the buyer described?
- Does the voice match the brand and the personas?
- Does the GTM motion shape align with services and ICP?

Surface contradictions to the operator. Fix them. Do not ship a foundation that fails this check.

### Phase 6 - GTM motion synthesis

Generate `gtm-motion.md`. The operator must be able to articulate it in one paragraph by the end. Instantiate the four-step funnel pattern from `foundation.md` section 4.3 for this specific operator:

1. The signature artefact (what external truth does it reveal).
2. The buyer's natural next question.
3. The operator's product or recommended tool that answers the question with a low-commitment first step.
4. The full deployment that closes the gaps the first step surfaced.

Write the paragraph. Read it back. Confirm the operator agrees it describes their motion.

### Phase 7 - Write foundation files

Write all foundation files to `/workspace/foundation/` using the templates in `/01-foundation/`. Verify each file is filled and coherent. Verify voice.md is referenced and applied to all output.

Run the validation rubric from `foundation.md` section 12.1:

1. Did the intake complete self-serve, no synchronous human support required?
2. Are foundation files vertical-specific?
3. Did the sparring layer reject weak inputs?
4. Are foundation files internally coherent?
5. Can the operator articulate their GTM motion shape in one paragraph?

If any of the 5 fail, return to the relevant phase and fix.

### Phase 8 - Hand-off

Tell the operator what is done and what to run next:

> "Foundation complete. You can now run any of: artefact (signature artefact generator), teardown (competitor analysis), proposal (post-discovery client doc), handoff (solutions team brief), nurture (post-proposal sequence). The artefact skill is the highest-leverage place to start."

Stop. Do not auto-run skills. The operator decides next.

## Hard rules

- Never write to `/workspace/foundation/` before Phase 5 has cleared. Working memory only.
- Never skip the sparring layer because the operator seems senior or in a rush. The bar is the bar.
- Never invent data. If a phase's input is empty, say so and keep moving.
- Never use em dashes or any dash other than "-". Never use "that's not X, that's Y" reframing in operator-facing language.
- Default to British English unless the operator picks American in Phase 0.
- The intake is a conversation. Do not paste the whole questionnaire at once. Run it section by section. Let the operator breathe.

## What "done" looks like

- All 10 foundation files exist in `/workspace/foundation/` and pass coherence check.
- The operator can summarise their GTM motion in one paragraph.
- The 5-point validation rubric passes.
- The operator knows what skill to run next.
