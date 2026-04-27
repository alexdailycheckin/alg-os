# Artefact Production - Edition Generator

This file runs when:

- The artefact skill (`skill.md`) is in Phase 6 and the operator confirmed they want to produce edition 1 alongside the spec, OR
- The operator says "produce my artefact edition," "produce edition <N>," "ship edition <N>," "run the artefact production," or any equivalent.

The skill produces the actual artefact (the index, report, benchmark, diagnostic) ready for review and publication. Not just the spec. The thing the operator ships.

Read in full before doing anything else.

## What this skill produces

A complete artefact edition at `/workspace/execution/artefact/<slug>-edition-<NN>/` that includes:

- `edition-<NN>.md` - the canonical markdown edition.
- `methodology.md` - the data sources, sampling, calculation logic.
- `distribution/` - ready-to-send formats per the spec's distribution plan (press release, LinkedIn post, newsletter, etc.).
- `data/` - the underlying data the edition was produced from (snapshot, in case sources change later).

The edition is operator-reviewed before publication. The skill produces, the operator approves and ships.

## Inputs the skill reads

| File | Why |
|---|---|
| `/workspace/foundation/voice.md` | All output uses the operator's voice. The edition itself follows operator brand voice. |
| `/workspace/foundation/brand.md` | Naming convention discipline. The edition is published under the operator's brand. |
| `/workspace/foundation/positioning.md` | The win axis the edition reinforces. |
| `/workspace/foundation/markets.md` | Geographic and vertical scope of the edition. |
| `/workspace/execution/artefact/<slug>-spec.md` | The spec is the brief for this edition. Data set, named entities, production cadence, distribution channels all live here. |
| `/workspace/research/capability-snapshot.md` | Production tools currently available. |

If the spec is missing, refuse to run. Tell the operator to run "design my artefact" first to produce the spec.

If multiple artefact specs exist, ask the operator which one to produce.

## Operator inputs

Ask:

1. **Which edition.** Edition number. If this is the first edition produced, default to 01. If editions 01 to 04 already exist, default to 05. Operator can override.
2. **The data.** The spec defines the data set. The operator provides it now. Acceptable formats:
   - File paths (`@~/path/to/data.csv`).
   - Pasted data (CSV-like, JSON, structured text).
   - URLs to scrape (e.g., for public data the spec defined).
   - A combination.
3. **Refresh date.** When this data was collected. Determines the edition's "as of" date.
4. **Optional override on production cadence.** If the spec said quarterly but the operator wants to ship a one-off edition for a specific reason (a launch, a partner request), note this and proceed.

If the operator's data does not match the shape the spec defined, surface the gap and ask. Do not silently substitute.

## Flow

### Phase 1 - Spec validation

Read `/workspace/execution/artefact/<slug>-spec.md` in full. Verify:

- The data set definition is clear.
- The named entities are listed (or the segmentation logic, depending on the artefact pattern A/B/C/D).
- The production workflow is defined.
- The distribution channels are listed.
- The methodology can be applied to the operator's data.

If anything in the spec is too vague to apply, surface to the operator. Refuse to produce a weak edition because the spec was thin.

### Phase 2 - Data ingestion

Take the operator's data. For each format:

- **CSV / structured data:** parse columns, validate against the spec's expected fields, flag any missing fields.
- **Pasted text:** parse, surface what was extracted, ask for confirmation.
- **URLs:** `web_fetch` and parse. For lists of named entities (e.g., 50 dental groups to mystery-shop), confirm coverage matches the spec.
- **File uploads:** parse per `/00-intake/data-ingestion.md` rules.

After ingestion, summarise to the operator:

> "Data parsed. <N> named entities, <Y> data points, refreshed <date>. Coverage gaps: <list>. Continue, or fix the gaps first?"

Wait for operator confirmation.

### Phase 3 - Analysis

Apply the spec's analysis logic. For pattern A (signature named-entity index):

- Compute the metric for each named entity per the spec's calculation.
- Rank or score entities.
- Identify outliers (best, worst, surprising).
- Compute aggregate stats (mean, median, distribution).
- For edition 02+: compute year-on-year or quarter-on-quarter change against prior editions. Read prior editions from `/workspace/execution/artefact/<slug>-edition-<previous>/`.

For pattern B (state-of-category report):

- Aggregate the data into the categories the spec defined.
- Surface trends and percentages.
- Compute distribution.

For pattern C (anonymised benchmark):

- Segment data per the spec's segmentation logic.
- Compute benchmarks per segment.
- Generate self-identification logic so readers can place themselves.

For pattern D (interactive diagnostic tool):

- Aggregate prospect-run data into trend metrics.
- Surface category-wide patterns.

For pattern E (no fit): production was never appropriate for this operator. Refuse to run.

### Phase 4 - Drafting

Write the edition using the operator's voice. Structure depends on pattern.

**Default structure (pattern A, B, C):**

1. Title and metadata (edition number, as-of date, publication date).
2. Executive summary (3 to 5 sentences, the key finding upfront).
3. Headline numbers (the 3 to 5 most striking findings).
4. Methodology summary (one paragraph, full version in methodology.md).
5. Detailed findings (per named entity / per segment / per category).
6. Named entities ranked or scored (with year-on-year change for edition 02+).
7. What this means (operator's commentary, 5 to 8 sentences linking findings to actionable implications for the buying committee).
8. About the producer (one paragraph on the operator).
9. How to claim or update your entry (specific instructions if the artefact is named-entity).
10. Next edition (when, what changes).

**Pattern D structure:**

The aggregate report on tool-runs. Same shape but the "named entities" become aggregated user segments.

### Phase 5 - Voice and quality

Apply voice rules from `/workspace/foundation/voice.md` throughout. Run the edition's quality checklist (the one inside the spec under "Quality checklist for ongoing editions") plus the general voice checks:

- No banned words.
- Three sentences max per paragraph.
- Digits not words.
- British or American per voice.md.
- No "shocking" or "stunning" hyperbole on findings.
- Methodology section is honest about limitations.
- Customer-as-hero where applicable.

### Phase 6 - Distribution-ready formats

Read the spec's distribution plan. For each channel listed, produce the channel-specific format and save under `/workspace/execution/artefact/<slug>-edition-<NN>/distribution/`.

| Channel | Format | File |
|---|---|---|
| Operator domain | Markdown for the canonical post | `web-post.md` |
| Press release | Press-release-format text | `press-release.md` |
| LinkedIn (founder personal) | Under-200-word LinkedIn post format | `linkedin-founder.md` |
| LinkedIn (company page) | Company-tone LinkedIn format | `linkedin-company.md` |
| Newsletter | Email-formatted post (respect operator's email constraints, e.g. no removed merge tags) | `newsletter.md` |
| X / Twitter | Thread format if relevant | `x-thread.md` |
| Partner amplification | Templated email or one-pager partners can forward | `partner-template.md` |

Skip channels not listed in the spec. Do not invent distribution paths.

### Phase 7 - Methodology and data snapshot

Write `methodology.md` with full transparency:

- Data sources (URLs, dates, providers).
- Sample size and selection logic.
- Calculation method per metric.
- Known limitations.
- What changed since prior editions (for edition 02+).

Save the parsed data in `data/` so future editions or audits can reproduce the analysis.

### Phase 8 - Quality checklist

Run the production checklist below before declaring the edition complete.

### Phase 9 - Hand-off

Tell the operator:

> "Edition <NN> ready at `/workspace/execution/artefact/<slug>-edition-<NN>/`. Files: edition-<NN>.md (canonical), methodology.md (full method), distribution/ (channel formats). Review the canonical first, then approve each distribution format. Publish per the spec's distribution plan."

Do not auto-publish. Do not auto-send. The operator reviews and ships.

## Quality checklist - Production-specific

10 items. Three failures kill the edition. Fix and re-run the relevant phase before writing.

1. **Data is fresh.** As-of date matches the operator's stated refresh date.
2. **Coverage matches spec.** All named entities the spec promised are covered, or the gaps are documented in methodology.md.
3. **Calculation matches spec.** The metric definition in the edition matches the metric definition in the spec.
4. **No invented numbers.** Every number in the edition is sourced from the operator's data or referenced public source.
5. **Year-on-year change surfaced (edition 02+).** Where prior editions exist, change vs prior is shown.
6. **Voice rules applied.** No banned words, paragraph length, English variant.
7. **Methodology is honest.** Known limitations are documented, not hidden.
8. **Named entities are correct.** No misspellings, no wrong company names, no out-of-scope entities snuck in.
9. **Distribution formats match channels in the spec.** No invented channels, no skipped channels.
10. **The edition's headline finding is concrete.** "Many UK dental groups miss calls" fails. "60% of UK dental groups with 5+ sites missed more than half of inbound calls between 9am and 11am in <quarter>" passes.

If 3 or more fail, do not write to `/workspace/execution/artefact/<slug>-edition-<NN>/`. Surface and fix.

## Hard rules

- Apply voice rules from `voice.md` throughout.
- Never invent data. Every number sourced from operator-provided data or public source.
- Never auto-publish. Operator reviews and ships.
- Never deviate from the spec without surfacing the deviation. If the spec said quarterly and the operator wants this to be a one-off, note it.
- The methodology section is mandatory and honest. Hide nothing.
- Edition numbering is sequential. No skipping. No re-using numbers (edition 01 is permanent once written).
- Data snapshot is mandatory. Save the parsed data so editions can be audited and reproduced.

## Edition numbering

Sequential, zero-padded to two digits. 01, 02, 03 ... 99. If the operator publishes more than 99 editions of one artefact, congratulations, then move to three digits.

For multi-cadence operators (an artefact published quarterly + an annual companion), use suffix conventions:

- Quarterly: `edition-Q1-2026`, `edition-Q2-2026`, etc.
- Annual: `edition-annual-2026`.
- One-off: `edition-special-<slug>` (with operator approval).

## Hand-off integration

After production completes, the spec's "Quality checklist for ongoing editions" is the operator's runbook for edition <NN+1>. Reading prior editions, the spec, and the methodology together tells the operator (or the meta-agent in Build 3) how to produce the next one.

Build 3 will eventually run this skill on cadence per the spec. For v1, the operator runs it manually.
