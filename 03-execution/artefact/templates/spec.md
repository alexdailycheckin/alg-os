# Artefact Spec Template

The output template the artefact skill writes to `/workspace/execution/artefact/<slug>-spec.md`.

Fill every section. Empty sections fail the quality checklist.

```
# Signature Artefact - <Operator Name>

## One-liner

<One sentence. Names the artefact and the truth it reveals.>

## Pattern

<A | B | C | D | E. From the diagnostic.>

## The external truth

<2 to 3 sentences. The specific, measurable truth the artefact reveals about the operator's market.>

## The data set

- **What data:** <bullet list of data types>
- **Sourced from:** <named sources, including operator-proprietary, public, partner, or aggregator>
- **Refresh cadence:** <how often the data gets re-collected>
- **Volume per edition:** <quantified, e.g. "100 calls across 50 locations" or "survey of 200 named buyers">

## Named entities

<For pattern A: list of named entities scored. Group by tier if the list is long.>

<For pattern B: aggregate categories surveyed.>

<For pattern C: anonymised segmentation logic that lets buyers self-identify.>

<For pattern D: the interactive tool's input fields and the trend report's aggregate dimensions.>

## Production cadence

<Quarterly | Monthly | Annual | Biannual.>

<2 sentences justifying the cadence given team capacity from team.md.>

## Production workflow

Step by step. Who does what.

1. <Step 1: data collection. Owner. Tools. Estimated effort.>
2. <Step 2: data analysis. Owner. Tools. Estimated effort.>
3. <Step 3: writing. Owner. Tools. Estimated effort.>
4. <Step 4: design. Owner. Tools. Estimated effort.>
5. <Step 5: review and sign-off. Owner.>
6. <Step 6: publication. Owner. Channels.>
7. <Step 7: distribution and amplification. Owners. Channels.>

Total effort per edition: <hours, or % of one FTE per edition>.

## Distribution plan

- **Operator domain:** <URL where the artefact lives>
- **Press release strategy:** <named distribution route, owner>
- **SEO targets:** <search terms the artefact ranks for>
- **AEO targets:** <queries LLMs answer using this artefact>
- **Social amplification:** <channels, owners, cadence>
- **Partner amplification:** <named partners, value exchange>
- **Paid amplification (if any):** <budget per edition, channels>

## Compounding mechanism

<3 to 5 sentences. What gets stronger after edition 2, 3, 4. Specifics, not abstractions.>

## The buyer's natural next question

<The question the buyer asks after reading the artefact. This is the bridge to step 3 of the four-step funnel.>

## How this connects to the operator's offer

<2 to 3 sentences. The link from "buyer asks the next question" to "operator's product or recommended tool answers it." References services.md.>

## Year-2 and year-3 vision

<3 to 5 sentences. What the artefact looks like at edition 4 to 12. Sister indices? Subscription product? Vertical expansion? Or "we keep doing it the same way."

If year-2 vision implies prerequisites (more data, more partners, hiring), name them.>

## Voice and tone

<Reference voice.md. Specific points where this artefact's tone differs from default operator content (e.g. more data-led, less narrative).>

## Risk register

<Things that could kill this artefact between editions.>

- <Risk: dependency on one data source, one team member, one partner.>
- <Risk: legal or regulatory exposure on naming entities.>
- <Risk: cadence slippage if production capacity tightens.>

## Accepted exceptions to the quality checklist

<List items from /03-execution/artefact/quality-checklist.md that the operator has accepted as known weaknesses. Maximum 2.>

## First edition launch plan

<One-page plan. Date target, pre-launch sequence, launch day distribution, post-launch follow-up. The first edition gets disproportionate attention because it sets the artefact's discoverability anchor.>

## Quality checklist for ongoing editions

A short version of /03-execution/artefact/quality-checklist.md the operator runs before publishing each future edition.

- [ ] Data set is fresh.
- [ ] Named entities reviewed and updated.
- [ ] Voice rules followed.
- [ ] Distribution plan executed.
- [ ] Year-on-year change surfaced where possible.
- [ ] Buyer's natural next question still landing.
- [ ] No regressions on the structural items (1, 2, 3, 7, 10) from the original spec.
```

## Notes for the artefact skill writing this template

- All bracketed placeholders must be filled before saving. Empty placeholders are a quality checklist fail.
- "Accepted exceptions" stays in the file even when empty (showing zero exceptions is itself useful).
- The "Quality checklist for ongoing editions" inside the spec is the operator's runbook for future editions. Make it operationally useful.
- File name slug: lowercase, hyphenated, max 50 chars. Example: `quarterly-customer-experience-index-spec.md`.
