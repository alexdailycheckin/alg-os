# Artefact Diagnostic - Picking the Right Pattern

The fit diagnostic the artefact skill runs in Phase 1 to decide which of patterns A to E fits this operator.

## The four diagnostic questions

Each question shapes which artefact pattern fits. The operator may have already answered some implicitly via their foundation files. Check `/workspace/foundation/` first. Only ask the operator if the answer is genuinely unclear from intake.

### Question 1 - Ticket size

**Are buyers in your ICP making purchase decisions north of £10k or equivalent?**

| Answer | Implication |
|---|---|
| Yes | High-ticket pattern. Patterns A, B, C, or E. |
| No | Low-ticket. Pattern D (interactive diagnostic tool) is the better fit. Or pattern B if the operator can subsidise the artefact strategically. |

Inferred from `pricing.md` (the floor and typical mid-tier).

### Question 2 - Buying committee

**Is the buying decision made by a committee or a single buyer?**

| Answer | Implication |
|---|---|
| Committee | Patterns A, B, C all fit. Artefacts travel inside the buyer's organisation when they name peers or quantify a leak the committee already suspected. |
| Single buyer | Pattern D (interactive tool) fits. The artefact is a personal-decision aid, not a committee-circulating document. |

Inferred from `personas.md` (the buying committee shape).

### Question 3 - Search behaviour

**Does your ICP search for category-specific terms when researching options?**

| Answer | Implication |
|---|---|
| Yes | Patterns A, B, C compound via SEO and AEO. Artefact gets indexed, becomes the answer to category searches over time. |
| No | Distribution is harder. Pattern D or pattern E. Or pattern B with paid distribution in lieu of organic search. |

Inferred from `gtm-motion.md` (channel mix) and `markets.md`.

### Question 4 - Data accessibility

**Do you have access to, or can you produce, a data set that ranks or measures named entities your ICP cares about?**

| Answer | Implication |
|---|---|
| Yes | Pattern A (signature named-entity index) is the dominant fit. Strongest compounding. |
| No, but we can produce a vertical-wide aggregate dataset | Pattern B (state-of-category report) fits. |
| No, and naming entities is legally or commercially impossible | Pattern C (anonymised benchmark) fits. |
| No data set possible | Pattern D or pattern E. |

Inferred from `services.md` (mode and delivery model) and `team.md` (artefact production capacity).

## The five patterns

### Pattern A - Signature named-entity index

The dominant pattern. Most B2B operators in high-ticket, service-heavy, customer-facing categories can produce this.

**Examples:**

- A multi-location healthcare or services chain: Quarterly Customer Experience Index based on mystery shopping data.
- A B2B SaaS company: Time-to-Value Audit comparing onboarding speeds across the category.
- A recruitment firm: Candidate Experience Report scoring named hiring brands.
- A plumbing or trades franchise: First Call Resolution Benchmark.
- A law firm: Client Response Time Index in their practice area.
- A financial services brand: Switching Friction Report for current account or pension providers.
- A logistics or 3PL: Delivery Promise vs Reality Index.

**Why it compounds:** Year 2 has longitudinal trends. Year 3 the data subscription itself can become a product line.

**Production cadence:** Quarterly is the gold standard. Monthly is too frequent for most data sets to refresh meaningfully. Annual loses search-engine freshness signals.

### Pattern B - State-of-category report

Fits when the operator is in a high-ticket category but cannot or will not name entities. Often early-stage categories or fragmented buyer sets.

**Examples:**

- "State of the AI Operations Market 2026" with vertical breakdowns and aggregate trends.
- Annual benchmark of an emerging job role (e.g. Heads of RevOps salary and tooling survey).
- Aggregated ROI study across category buyers.

**Why it compounds:** Buyers come back annually for updated data. The first edition is the most expensive; subsequent editions reuse infrastructure.

**Production cadence:** Annual or biannual. Quarterly is rarely possible for state-of-category data.

### Pattern C - Anonymised benchmark study

Fits when naming entities is legally or commercially impossible (patient data, security incident data, financial data behind NDAs). Buyers self-identify their position in the benchmark by entering their own metric.

**Examples:**

- Cyber Security Breach Cost Benchmark (anonymised by sector and size).
- Patient Wait Time Index (anonymised by hospital trust size).
- Pension Fund Performance Benchmark (anonymised by AUM band).

**Why it compounds:** Each edition adds participants. Buyers want to know where they stand relative to peers, which keeps engagement high.

**Production cadence:** Quarterly or biannual.

### Pattern D - Industry diagnostic tool

Fits low-ACV B2B SaaS, transactional e-commerce, and any operator whose buyer is a single decision-maker, not a committee. The "artefact" is an interactive tool the prospect runs against their own data.

**Examples:**

- A SaaS pricing-page audit tool that scores the prospect's pricing transparency.
- A LinkedIn profile diagnostic for recruiters.
- An email deliverability checker for cold-outbound operators.

**Why it compounds:** Each prospect run produces aggregate data the operator can publish as a meta-artefact ("State of pricing pages 2026").

**Production cadence:** The tool is always-on. Aggregate trend reports run quarterly or annually.

### Pattern E - Honest no fit

Fits when the operator's business genuinely does not match any of A to D. Examples:

- Pre-revenue startup with no operational data and no customer reference set.
- Bespoke high-touch consulting where the unit economics do not justify artefact production.
- Operators whose ICP is so niche that named-entity comparison is meaningless.

In these cases, the artefact pattern is not the right motion. Tell the operator directly:

> "Your business does not fit the signature artefact pattern. The four-step funnel still applies, but step 1 is one-to-one founder-led research and outreach, not a published artefact. The artefact skill cannot produce a defensible spec. Skip ahead to the proposal and handoff skills once Build 2 ships."

Do not force a candidate into pattern A through D when E is honest.

## Diagnostic scoring

Internal scoring for the skill (do not show this to the operator unless asked):

| Q1 | Q2 | Q3 | Q4 | Pattern |
|---|---|---|---|---|
| Yes | Committee | Yes | Yes (named entities) | A |
| Yes | Committee | Yes | Yes (aggregate only) | B |
| Yes | Committee | Yes | No naming possible | C |
| Yes | Committee | No | Any | B (with paid distribution) |
| Yes | Single | Any | Any | D |
| No | Any | Any | Any | D |
| No data, no fit | Any | Any | None | E |

Edge cases:

- Operator with mixed ICPs (one high-ticket, one low-ticket): pick the dominant ICP from `icp.md` and run the diagnostic against that. Note the secondary in the candidates section.
- Operator with no foundation file ready: refuse to run the diagnostic until intake is complete.
- Operator who insists on a pattern that does not fit their answers: flag the mismatch, ask once for confirmation, then proceed with the operator's pick (with the mismatch noted in the spec).
