# Proposal Skill - Post-Discovery Client Document

This file runs when the operator says "draft a proposal," "write a proposal," "post-discovery doc," "proposal for <client>," or any equivalent.

The skill produces a lean, client-facing proposal from a discovery transcript or notes. It is not a long pitch document. It is the document a senior operator would write to a senior buyer who already had the discovery call.

Read in full before doing anything else.

## What this skill produces

A complete client-facing proposal at `/workspace/execution/proposal/<prospect-slug>-proposal.md` that includes:

- Executive summary (the prospect's situation as they described it).
- Diagnosis (the leak, the gap, the named numbers).
- Recommended engagement (which service tier, why, with named outcomes).
- The first 30 to 60 to 90 days.
- Pricing with the operator's anchor (against hiring, not against software, per the operator's pricing.md rules).
- The next step (one low-commitment action).

Length target: 800 to 1,500 words. Operator-tone. Customer-as-hero. Voice rules applied throughout.

## Inputs the skill reads

| File | Why |
|---|---|
| `/workspace/foundation/voice.md` | All output uses the operator's voice. |
| `/workspace/foundation/services.md` | The tier structure and outcomes the proposal recommends from. |
| `/workspace/foundation/pricing.md` | The pricing model and the anchor framing. |
| `/workspace/foundation/positioning.md` | The win axis the proposal leans on. |
| `/workspace/foundation/personas.md` | The buying committee shape. The proposal language addresses the right roles. |
| `/workspace/foundation/icp.md` | Confirms the prospect fits the operator's ICP. If they do not, the skill flags this. |
| `/workspace/foundation/gtm-motion.md` | The four-step funnel framing. The proposal sells step 3 or step 4. |

If foundation files are missing, refuse to run.

## Operator inputs

Ask:

1. **The prospect.** Company name, vertical, size band.
2. **The source material.** A discovery transcript (`@path/to/transcript.md`), discovery notes, or a summary the operator types or pastes. The skill needs raw discovery content. Do not invent details.
3. **The recommended engagement.** Which service tier from `services.md` is the operator proposing. If unclear, ask the operator to pick or recommend based on the discovery content.
4. **Optional context.** Any specific commercial constraints (timeline, budget cap, named blockers, named champion).

## Flow

### Phase 1 - Extract from discovery

Parse the source material. Extract:

- **Prospect snapshot.** Vertical, size, geography, named individuals on the call, their roles.
- **Trigger event.** What is happening in their world that makes this purchase relevant now. Quote them where possible.
- **Named pains.** Specific operational pains the prospect described. Quote them.
- **Quantified leaks.** Any numbers the prospect put on the leak (revenue at risk, hours spent, deals lost, calls missed). If the prospect did not quantify, flag this and ask the operator if they can.
- **Decision-makers and blockers.** Who signs, who blocks, who champions.
- **Stated objections.** Anything the prospect raised on the call.
- **Stated timeline.** When they need this live.
- **Stated budget posture.** Any signal on what they are willing to spend or have spent before.

If the source material is too thin to extract this, refuse to run. Tell the operator the discovery transcript is insufficient. List the specific gaps. Ask for more context before proceeding.

### Phase 2 - Fit check against ICP

Read `icp.md`. Confirm the prospect fits the primary or a secondary ICP. If they do not, surface this:

> "This prospect does not match your primary or secondary ICP. Primary ICP is <X>. Prospect is <Y>. Continue anyway?"

If the operator confirms, the proposal still gets drafted but the executive summary notes the fit gap honestly. Do not pretend the prospect is a perfect fit when the foundation files say they are not.

### Phase 3 - Recommend the engagement

If the operator already named a tier, validate against the discovery content (does the prospect's leak size, capacity, and budget match this tier).

If the operator did not name a tier, recommend one with reasoning. Map the prospect's quantified leak against `services.md` tiers and `pricing.md` ranges. Recommend the tier where the operator's typical landed deal value matches what the prospect's leak justifies.

### Phase 4 - Draft the proposal

Use the template below. Apply voice rules. Lengths:

- Executive summary: 3 to 5 sentences.
- Diagnosis: 3 to 5 sentences plus a bulleted leak list.
- Recommended engagement: 5 to 8 sentences plus a phased timeline.
- Pricing: clear table or bulleted breakdown.
- Next step: 1 sentence.

### Phase 5 - Quality checklist

Run the checklist below. Surface failures. Fix before writing to `/workspace/execution/proposal/`.

## Output template

```
# Proposal - <Prospect Company Name>

**Prepared for:** <Named decision-maker>, <Title>, <Company>
**Prepared by:** <Operator Name>
**Date:** <YYYY-MM-DD>

## Executive summary

<3 to 5 sentences. The prospect's situation in the prospect's own words where possible. The named trigger. The named leak. The recommended engagement in one line.>

## What we heard on the call

<Bulleted list of the named pains, named numbers, named blockers, named champion. Quote the prospect where the language is theirs. This proves the operator listened.>

## Diagnosis

<3 to 5 sentences. The diagnosis names what is leaking, where, and how much. References specific quotes from the call if possible. Connects the prospect's named pains to the operator's win axis from positioning.md.>

**Quantified leaks:**

- <Leak 1: where, how much, with source>
- <Leak 2: ...>
- <Leak 3: ...>

## What we recommend

<5 to 8 sentences. Names the recommended service tier from services.md. Explains why this tier matches the prospect's named leak. Avoids generic claims; uses the operator's actual proof points.>

### First 30 days

<2 to 3 sentences. The first 30 days are deliberately lower commitment. Set up, calibrate, surface initial outputs.>

### Days 30 to 60

<2 to 3 sentences. The first measurable wins land here. Specific outputs the prospect will see.>

### Days 60 to 90

<2 to 3 sentences. The motion is steady-state. Measurable revenue recovery or capacity addition.>

## Pricing

<Use the operator's pricing model from pricing.md. Anchor against hiring per the operator's anchor rules. Format as a clear table or bullet list.>

| Component | Cost | Comparison |
|---|---|---|
| <Component 1> | <Price> | <Anchor against hiring or operational cost> |
| <Component 2> | <Price> | <Anchor> |

**Total first-year value:** <Amount>
**Comparison anchor:** <e.g. "Less than the cost of one junior FTE all-in for 6 months">

## Next step

<One sentence. The lowest-commitment action that moves the deal forward. Often: "Confirm by <date> and we have <Phase 1 outcome> by <date>."

If the operator's GTM motion has a specific next-step convention (e.g. Implement AI's £500 30-day Command trial), use it.>
```

## Quality checklist

Six items. Three failures kill the proposal. Surface and fix.

1. **Customer-as-hero.** Every paragraph treats the prospect as the protagonist. The operator is the guide. If the proposal opens with operator history or capability, fail.
2. **Voice rules followed.** No banned words. Three sentences max per paragraph. Digits not words. British or American per `voice.md`.
3. **Specifics not adjectives.** Every claim about outcomes is quantified or sourced from a real proof point. No "industry-leading," no "best-in-class."
4. **Direct quotes from discovery.** The "What we heard" section quotes the prospect at least once. This proves listening.
5. **Pricing anchored against the right comparison.** Per `pricing.md`. Hiring cost for a labour-as-product operator. Software-cost only if that is the operator's stated anchor.
6. **Next step is genuinely low-commitment.** "Confirm by Friday and we have first output by next Wednesday" passes. "Schedule a 60-minute follow-up call" fails.

If 3 or more items fail, the proposal does not get written. Surface the failures and ask for what is needed.

## Hard rules

- Apply voice rules from `voice.md` to every word.
- Never invent quotes from the prospect. Every quote is sourced from the transcript.
- Never invent named outcomes or proof points. Use only what the operator's foundation files contain.
- If the discovery is too thin to write a defensible proposal, refuse and ask for more.
- Customer-as-hero: opening paragraph is about them, not the operator.

## Hand-off

After writing:

> "Proposal saved to `/workspace/execution/proposal/<slug>-proposal.md`. Suggested next moves: brief the solutions team for delivery (run 'write the handoff'), or set up the post-proposal nurture sequence in case the prospect goes quiet (run 'nurture sequence')."

Do not auto-run other skills.
