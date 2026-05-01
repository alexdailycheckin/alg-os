# Artefact Quality Checklist

Run this checklist in Phase 4 of the artefact skill, before writing the spec to `/workspace/execution/artefact/`. If any item fails, surface to the operator and fix.

## The bar

A defensible signature artefact spec passes all 12 items. Any failure means the spec is not ready. Do not write to `/workspace/execution/artefact/` until all 12 pass or the operator explicitly accepts a documented exception.

## Items

### 1. The external truth is concrete

The spec names a specific external truth the artefact reveals. "Industry insights" fails. "60-70% of UK multi-site dental groups miss inbound calls between 9am and 11am" passes.

### 2. The data set is real

The spec names where the data comes from and how it is gathered. "Public sources" fails. "Mystery shopping calls run by Implement AI's growth team across publicly listed locations, supplemented by Trustpilot review analysis" passes.

The operator can actually produce or source this data on the stated cadence. If the team chapter shows artefact production with no owner or as a single point of failure, the cadence proposed must reflect that constraint.

### 3. Named entities the buying committee cares about

The spec names the entities scored or measured. "Industry leaders" fails. "Bupa Dental, Genesis Health Ltd, Quality Dental Group, Townhouse, plus aggregate stats across 435 UK dental practices" passes.

If the pattern is C (anonymised) or D (interactive tool), this item is satisfied by the segmentation logic instead. The benchmark must let buyers self-identify their position credibly.

### 4. Production cadence is realistic

The cadence matches the operator's actual production capacity. If `team.md` shows artefact production owned by one person who already runs sales, content, and podcast, quarterly might be the ceiling. Monthly is unrealistic.

If the operator pushes for a faster cadence than the team can sustain, surface the conflict. Either the cadence drops or the team chapter needs to surface a hiring plan.

### 5. Distribution plan is specific

The spec names where the artefact lives, how it gets seen, and which roles promote it. "We will publish on our blog" fails. "Lives at the operator's domain (e.g., operator.tld/dental-phone-performance), press release through the operator's PR retainer, LinkedIn amplification by the operator's senior brand voices (Head of Growth, Chairman, CEO as applicable), partner amplification through PE/VC operating partners, and a ranked-results page Google indexes for the relevant head terms" passes.

### 6. SEO and AEO targets are explicit

For patterns A, B, C: the spec names the search terms the artefact targets. The first edition takes time to rank; subsequent editions inherit ranking. Without explicit search targets, distribution depends entirely on paid amplification.

For pattern D: AEO matters more than SEO (LLMs surface the diagnostic tool when buyers ask the underlying question). Spec names the LLM-targeted query patterns.

For pattern E: this item is N/A.

### 7. Compounding mechanism is named

The spec describes what gets stronger after edition 2, 3, 4. Generic compounding answers fail. Concrete answers pass:

- "By edition 2 we have year-on-year change for every named location, which becomes the lead headline."
- "By edition 4 the dataset is the only longitudinal source in the UK, which becomes a paid subscription."
- "By edition 6 partner organisations submit their own data to be included, which expands coverage without our cost going up."

### 8. The artefact extends positioning

The spec is consistent with `positioning.md`. The win axis defined in positioning shows up in what the artefact measures. The concession axis is honoured (the artefact does not accidentally compete on the operator's deliberate concession).

### 9. The artefact lands with the named ICP

The spec is consistent with `icp.md`. The named entities in the artefact are companies, people, or peers the ICP buying committee actually pays attention to. Naming the wrong entities (out-of-vertical, out-of-geography, out-of-segment) loses leverage.

### 10. The buyer's natural next question is identified

The spec names what the buyer asks after reading the artefact. This is the bridge to step 3 of the four-step funnel.

If the artefact does not produce a natural next question, the funnel breaks. Reject the candidate.

### 11. Production workflow is step-by-step

The spec lists the steps to produce one edition. Who does what, in what order, with what tools. Vague production plans cause artefact projects to die between editions.

The workflow is realistic against `team.md` and the capability snapshot at `/workspace/research/capability-snapshot.md`.

### 12. Year-2 and year-3 vision is documented

The spec sketches what the artefact looks like at edition 4 to 12. This forces the operator to think about whether the artefact is a one-off campaign or the unit of compounding for the next 3 years.

If year-2 vision is "we keep doing it the same way," that is fine but worth surfacing. If year-2 vision is "we expand to a sister index in an adjacent vertical," the spec should note the prerequisites.

## Documented exceptions

The operator can override an item with explicit acceptance. Document the override inside the spec under an "Accepted exceptions" section. Examples:

- "Item 7 compounding mechanism is partially weak because we are running a single-edition campaign tied to a product launch. Accepted by the operator."
- "Item 5 distribution plan currently has no partner amplification because we have no partners. Accepted, with the note that this becomes the year-2 expansion target."

Operators can override at most 2 items. If 3 or more items fail, the spec is not ready. The skill does not write to `/workspace/execution/artefact/` until items pass or the override count is at or below 2.

## What to do when the bar fails

Surface the failures to the operator clearly:

> "The spec fails 4 items: 2, 5, 7, 11. Item 2 is the most load-bearing failure (data set is unclear). Fix in this order: 2, 11, 5, 7. Confirm fixes and I re-run the checklist."

Do not soften. Do not ship a weak spec. The artefact is the foundation of the four-step funnel. If it is weak, the rest of the motion is weak.
