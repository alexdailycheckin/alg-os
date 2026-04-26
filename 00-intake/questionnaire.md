# Questionnaire - Interactive Intake (Phase 4)

The structured question set for interactive intake. Run this after Phases 0 to 3 (voice, capability sync, file ingestion, online research) have populated working memory with whatever they could.

This is not a form to dump on the operator. It is a guide for Claude to interleave free-form extraction (when the operator is ramble-rich) and targeted sparring (when the operator is gap-rich or weak).

Every question section has a quality bar. Apply `/00-intake/sparring-rules.md` until the bar is cleared. Move to the next section only when the current section is defensible.

## Section A - Brand and mission

**Goal:** A defensible one-line summary of what the operator does and why.

Questions to ask if not inferred from Phases 2 and 3:

1. In one sentence, what does the company do.
2. What measurable outcome do you produce for buyers.
3. Why does this company exist (mission, the bit beyond making money).

**Bar:** The one-liner names the unit of value, not the category. "We help companies grow" fails. "We turn customer-experience leaks into a quarterly index our prospects benchmark themselves against" passes.

## Section B - Services and product

**Goal:** A defensible map of what is sold, how it is delivered, at what price.

Questions:

1. What is the smallest unit of value you sell. Name it, price it, describe its delivery cadence.
2. What are the next two units up the ladder, with the same detail.
3. Is this a product company (recursive product available to power agents) or a service company (no recursive product). This determines the mode in section 6.2 of the foundation doc.

**Bar:** Each unit is named, priced, and has a delivery model. "Consulting" fails. "A 6-week customer-experience audit, fixed price 30k GBP, delivered as a final report plus 3 implementation sessions" passes.

## Section C - ICP

**Goal:** Defensible ideal customer profile. Vertical + revenue band or company size + trigger event + one named pain.

Questions:

1. Pick the vertical you serve best.
2. Pick the revenue band or company size where you have the strongest case studies.
3. What event in the buyer's world makes this purchase relevant (regulatory, competitive, growth-stage, post-funding, board pressure).
4. Name the one operational pain that survives every discovery call.

**Bar:** All 4 fields populated. No "mid-market," no "growing companies," no abstractions. See sparring rules for refusal patterns.

If multiple ICPs exist, pick the dominant one. Note the secondary in a "secondary ICPs" subsection but do not let multiplicity weaken the primary.

## Section D - Personas

**Goal:** The buying committee. Decision-maker, blocker, champion.

Questions:

1. Who signs (role, seniority, reports to whom).
2. Who blocks (role, what objection do they raise, what would unblock them).
3. Who champions internally (role, what makes this purchase career-positive for them).
4. What metric is the decision-maker measured on this quarter.

**Bar:** Each role named with their motivation and friction. "C-level" fails. "VP of Customer Experience reporting to the COO, measured on NPS and time-to-resolution this quarter, blocked by IT compliance" passes.

## Section E - Positioning

**Goal:** Measurable differentiation from a named competitor set.

Questions:

1. Name your three closest competitors.
2. Pick one measurable axis on which you outperform them. Quantify the gap.
3. Pick one axis where you deliberately concede ground. State why.

**Bar:** Both 1 and 2 are concrete and named. The "concede" answer in 3 is a sign of honest positioning. If the operator claims to win on every axis, the bar fails (no positioning is total).

Apply sparring rules ruthlessly here. "Quality," "expertise," "service" all fail. A measurable proof point against a named competitor passes.

## Section F - Markets

**Goal:** Geographies, verticals, segments served.

Questions:

1. Which geographies (country level, not "global").
2. Which verticals (named, not "all industries").
3. Which segments inside each (enterprise / mid-market / SMB, with revenue bands).

**Bar:** Specificity. "Global" fails. "UK, Ireland, Netherlands, focused on financial services and higher-ed mid-market 50m to 500m turnover" passes.

## Section G - Team

**Goal:** Decision-makers and key people inside the operator's organisation.

Questions:

1. Who runs commercial functions (CRO, VP Sales, founder).
2. Who runs delivery (CDO, head of services, ops).
3. Who runs the artefact production (data, content, design ownership).
4. Are there gaps where the framework's expectations require headcount or tooling.

**Bar:** Real people named with roles. Vague answers like "we have a team" fail. "Alex (founder, runs commercial), Maria (head of delivery, owns implementation)" passes.

## Section H - Pricing

**Goal:** Pricing structure, anchor points, ranges.

Questions:

1. What is the price floor (smallest deal that is worth running).
2. What is the price ceiling (largest deal closed in last 12 months).
3. What is the typical mid-tier engagement.
4. Is pricing fixed, time-and-materials, retainer, or outcome-based.

**Bar:** Numbers named. "Variable" fails. "Floor 15k GBP, ceiling 250k GBP, typical 40 to 80k GBP, fixed-fee" passes.

## Section I - GTM motion shape

**Goal:** The four-step funnel from `foundation.md` section 4.3, instantiated for this operator. This is the proof of intake completion.

Questions, asked sequentially:

1. What signature artefact will reveal an external truth your buyers care about.
2. What is the natural next question a buyer asks after reading the artefact.
3. What low-commitment first step does your product or a recommended tool offer that answers the question.
4. What is the full deployment that closes the gaps the first step surfaced.

**Bar:** All 4 steps named with concrete content. The artefact has a data set the operator can produce. The next question is what a real buyer would ask. The first step is genuinely low-commitment. The full deployment is what the operator already sells.

If the operator cannot articulate this in one paragraph at the end, intake is not complete. Loop back to whichever section is weakest and re-spar.

## Voice and banned words

**Goal:** Set the operator's brand voice, banned words, paragraph rules.

Questions:

1. Confirm the English variant chosen in Phase 0.
2. Are there words or phrases your brand bans (industry jargon, terms competitors own, internal taboos).
3. Any deviation from the framework defaults (no em dashes, three sentences per paragraph, digits not words, operator tone, no "that's not X, that's Y" reframing).

**Bar:** voice.md fully populated. Banned-word list is honest (not "we ban nothing"). Default rules confirmed or overridden with reasoning.

## After all sections clear

Run Phase 5 (coherence check) and Phase 6 (GTM motion synthesis) per `intake.md`. Then write to `/workspace/foundation/`.
