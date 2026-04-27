# Artefact Skill - Signature Artefact Generator

This file runs when the operator says "design my artefact," "run the artefact skill," "what should our signature artefact be," or any equivalent.

The skill is a diagnostic, not a template. It interrogates the operator's business and proposes 3 candidate signature artefacts. The operator picks one. The system specs the data sources, the production cadence, and the distribution channels.

Read in full before doing anything else. The full design lives in `foundation.md` section 8.

## What this skill produces

A complete signature artefact specification at `/workspace/execution/artefact/<artefact-name>-spec.md` that includes:

- The artefact's name and one-line summary.
- The external truth it reveals.
- The data set used to produce it (what data, sourced from where, with what cadence).
- The production cadence (quarterly, monthly, one-off).
- Named entities the artefact scores or measures.
- Distribution channels (where it gets published, who promotes it, how it gets indexed by search).
- Why it compounds (what gets longitudinally stronger over time).
- Quality bar (the test the operator runs before publishing each edition).

## Inputs the skill reads

Before doing anything else, read:

| File | Why |
|---|---|
| `/workspace/foundation/voice.md` | All output uses the operator's voice. |
| `/workspace/foundation/brand.md` | The artefact must align with what the brand actually does. |
| `/workspace/foundation/services.md` | Mode (product-recursive vs tool-agnostic) shapes which artefacts are realistic to produce. |
| `/workspace/foundation/icp.md` | The artefact has to land with the named ICP. |
| `/workspace/foundation/personas.md` | The artefact has to make the buying committee read it. |
| `/workspace/foundation/positioning.md` | The artefact extends positioning, it does not contradict it. |
| `/workspace/foundation/markets.md` | Geographies and verticals constrain what entities can be named. |
| `/workspace/foundation/team.md` | Production capacity. If artefact production has no owner, the cadence changes. |
| `/workspace/foundation/gtm-motion.md` | The artefact is step 1 of the four-step funnel. The other three steps depend on it. |
| `/workspace/research/capability-snapshot.md` | Production tools available right now. |

If any foundation file is missing, refuse to run. Tell the operator to complete intake first. The artefact skill cannot produce a defensible spec without a defensible foundation.

## Flow

### Phase 1 - Fit diagnostic

The artefact skill defaults to looking for the high-ticket, service-heavy, customer-facing pattern from `foundation.md` section 8. Most B2B operators in that pattern can produce a quarterly named-entity benchmark or index. This is the dominant case.

But the skill must be honest when the operator's business does not fit. Run the fit diagnostic before proposing anything.

**Diagnostic questions (ask if not already clear from foundation files):**

1. Are buyers in your ICP making purchase decisions north of £10k or equivalent? (Yes = high-ticket pattern. No = consider alternative artefact types.)
2. Is the buying decision made by a committee or a single buyer? (Committee = artefacts that travel internally have leverage. Single buyer = the artefact is a personal-decision tool.)
3. Does your ICP search for category-specific terms when researching? (Yes = SEO-indexable artefacts compound. No = consider non-search-led distribution.)
4. Do you have access to, or can you produce, a data set that ranks or measures named entities your ICP cares about? (Yes = signature index pattern fits. No = consider state-of-category report or anonymised benchmark.)

Based on the answers, pick the artefact pattern.

| Pattern | When it fits |
|---|---|
| **A. Signature named-entity index** | High-ticket, search-led, named-entity buying committee. Quarterly cadence. The dominant pattern. Examples: Quarterly Customer Experience Index for healthcare chains, Time-to-Value Audit for B2B SaaS, Candidate Experience Report for recruitment, First Call Resolution Benchmark for trades. |
| **B. State-of-category report** | High-ticket but not named-entity oriented (early-stage category, fragmented buyer set). Annual or biannual cadence. Less compounding than A but lower production cost. |
| **C. Anonymised benchmark study** | High-ticket where naming entities is legally or commercially impossible (e.g. patient data, security incidents). Quarterly or biannual. Buyers self-identify their position in the benchmark. |
| **D. Industry diagnostic tool** | Low-ACV B2B SaaS or transactional e-commerce. The "artefact" is an interactive tool a prospect runs against their own data. Compounds via aggregate trend reports across users. |
| **E. Honest "no fit"** | The operator's business genuinely does not fit any of A to D. State this directly and route them to one-to-one signature work (founder-led research-driven outreach) instead. |

If E fires, do not propose a forced fit. Explain the diagnosis and stop.

### Phase 2 - Three candidates

Once the pattern is decided, generate 3 candidate artefacts within that pattern. Each candidate must:

- Use a data set the operator can actually produce or source.
- Reveal an external truth a buying committee in the ICP would care about.
- Name entities the buying committee already pays attention to (competitors, peers, public companies, geographies).
- Be produceable on the operator's stated production capacity (read `team.md`).
- Compound longitudinally.

Format the candidates for the operator to compare. Use a structured side-by-side:

```
Candidate 1: <Name>
- External truth: <one sentence>
- Data set: <what, sourced from where>
- Named entities: <list>
- Production cadence: <quarterly | monthly | etc.>
- Why this compounds: <one sentence>
- Production cost estimate: <hours per edition, or % of one FTE>

Candidate 2: <Name>
[same structure]

Candidate 3: <Name>
[same structure]
```

Do not pre-rank the candidates. Let the operator choose. If the operator picks one without sparring, ask one clarifying question to ensure they understand what they are committing to:

> "You picked Candidate <X>. To produce this on the cadence you said, your team needs to <produce the data set / write the report / distribute to <named channels>>. Confirm your production capacity supports this, or pick another candidate."

### Phase 3 - Spec the chosen artefact

Once a candidate is chosen, produce the full spec. Write to `/workspace/execution/artefact/<slug>-spec.md` using the template at `/03-execution/artefact/templates/spec.md`.

The spec includes everything from the candidate plus:

- Production workflow (step by step, who does what).
- Distribution plan (operator domain, press release strategy, SEO targets, social amplification, partner amplification).
- Compounding mechanism (what gets stronger after edition 2, 3, 4).
- Year-2 and year-3 vision (data subscription? Vertical expansion? Sister index?).
- Quality checklist before publishing each edition.

### Phase 4 - Quality checklist

Before declaring the spec complete, run the checklist in `/03-execution/artefact/quality-checklist.md`. If any item fails, surface it to the operator and fix before writing the spec to `/workspace/execution/artefact/`.

### Phase 5 - Spec hand-off and edition-1 branch

Tell the operator the spec is complete:

> "Spec complete at `/workspace/execution/artefact/<slug>-spec.md`. Two next steps:
>
> 1. **Produce edition 1 now.** If you have the data the spec describes, I can produce the first edition of the artefact in this same session. The output is review-ready (canonical markdown, methodology, distribution-ready formats per the spec's plan). You review and ship.
> 2. **Stop here.** The spec is the deliverable. Run 'produce my artefact edition' later when you have the data ready.
>
> Which do you want?"

If the operator says yes to edition 1, route to `/03-execution/artefact/production.md` and continue. The production skill picks up where this skill ended, reads the spec, asks for the data, and produces the edition.

If the operator says no, hand-off as before:

> "OK. The spec is the input to Build 3 (the meta-agent), which will eventually run production on cadence. For now, run 'produce my artefact edition' whenever you have the data ready."

Do not auto-run other skills. Operator decides next.

## Hard rules

- Never produce an artefact spec for an operator whose foundation does not pass intake validation. Refuse and route them back to intake.
- Never propose all three candidates within the same pattern if the operator's business straddles two patterns. Honestly mix patterns and let the operator see the trade-off.
- Never claim a data set is available that the operator cannot actually produce or source. Production-capacity reality wins over creative ambition.
- Never propose an artefact that contradicts `positioning.md`. The artefact extends positioning, it does not undermine it.
- Apply voice rules from `voice.md` to every operator-facing message.
- Apply the sparring discipline from `/00-intake/sparring-rules.md` if the operator picks a weak candidate or describes the production process in vague terms.
