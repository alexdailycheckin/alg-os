# Teardown Skill - Competitor and Positioning Analysis

This file runs when the operator says "run the teardown," "competitor analysis," "tear down a competitor," "teardown <competitor name>," or any equivalent.

The skill produces an actionable teardown of a named competitor. Specific positioning gaps the operator can attack, not a summary of what the competitor does.

Read in full before doing anything else.

## What this skill produces

A complete teardown at `/workspace/execution/teardown/<competitor-slug>-teardown.md` that includes:

- The competitor's stated positioning (lifted from their public surface).
- Their proof points (what is measurable vs what is marketing).
- Their stated and inferred ICP (who they actually serve vs who they claim to serve).
- Their pricing model if public.
- Their weak spots: positioning gaps, segment gaps, proof gaps the operator can attack.
- Strategic recommendations: 3 to 5 specific moves the operator should make.
- The wedge: the one positioning move that beats this competitor on the operator's win axis.

## Inputs the skill reads

Before doing anything else, read:

| File | Why |
|---|---|
| `/workspace/foundation/voice.md` | All output uses the operator's voice. |
| `/workspace/foundation/positioning.md` | The operator's win axis and concession axis frame the teardown. |
| `/workspace/foundation/icp.md` | The teardown is filtered through what matters to the operator's ICP. |
| `/workspace/foundation/services.md` | Mode and tier structure shape the comparison. |
| `/workspace/foundation/brand.md` | The operator's positioning in their own words. |
| `/workspace/foundation/markets.md` | Geographic and vertical scope of the comparison. |

If foundation files are missing, refuse to run. Tell the operator to complete intake first.

## Operator inputs

Ask:

1. **Which competitor.** Name the company. If the operator gives more than one, run the teardown for each in sequence.
2. **Optional URLs.** The competitor's website, LinkedIn page, customer reviews (G2, Trustpilot), recent press, sales collateral if the operator has it. The skill will scrape what is given. If nothing provided, default to scraping the competitor's main domain plus LinkedIn.
3. **Optional context.** Any specific deal where the operator is competing against this competitor right now, or a specific axis the operator wants the teardown to focus on.

## Flow

### Phase 1 - Public surface scrape

Run `web_fetch` and `web_search` against:

- The competitor's main domain (homepage, product pages, pricing if public, case studies, about page).
- The competitor's LinkedIn company page.
- Public reviews (G2, Trustpilot, Glassdoor for service companies, Capterra).
- Recent press in the last 90 days (funding, product launches, executive moves).
- Adjacent press: comparison articles, "<competitor> vs <category>" search results.

Extract:

- Their stated one-liner.
- Their stated ICP.
- Their stated proof points (named customers, named numbers, named outcomes).
- Their pricing if public.
- The language they use that is generic vs specific.

### Phase 2 - Marketing vs measurable

Categorise every claim the competitor makes into one of three buckets:

| Bucket | Examples |
|---|---|
| **Measurable** | "75% reduction in handling time," "100+ enterprise clients," "ISO 27001 certified," "GDPR compliant," named customer logos with case studies. |
| **Defensible** | Specific differentiators that are not quantified but are checkable (team size, integrations count, founding date, named partnerships). |
| **Marketing** | "Best-in-class," "next-generation," "AI-powered," "transform your business," "synergy," any banned word from the operator's voice.md. |

The teardown surfaces the ratio. A competitor whose claims are 80% marketing has a positioning weakness regardless of their actual capability.

### Phase 3 - Stated vs inferred ICP

The competitor states an ICP on their site. The actual ICP often differs (inferred from named customers, pricing tier, sales motion).

Extract:

- **Stated ICP.** What their copy says.
- **Inferred ICP.** Who their named customers actually are (size, vertical, geography). Who their pricing model is built for. Whether their motion is enterprise sales or self-serve.

Note any mismatch. A competitor who claims "we serve growing companies" but whose customer logos are all Fortune 500 has a vulnerability against the operator who actually serves growing companies.

### Phase 4 - Cross-reference against operator's positioning

Read `positioning.md` and produce the head-to-head:

| Axis | Operator | Competitor | Edge |
|---|---|---|---|
| Win axis (from operator's positioning.md) | <operator's measurement> | <competitor's measurement or absence of one> | <operator wins by X> |
| Concession axis (from operator's positioning.md) | <operator concedes> | <competitor wins> | <competitor wins, but at what cost to them> |
| Other relevant axes | ... | ... | ... |

This is the actionable core of the teardown. Surface where the operator's positioning is genuinely stronger and where the competitor wins (and whether the competitor's win is at a cost the operator's ICP would not pay).

### Phase 5 - Weak spots

List the 3 to 5 most exploitable weak spots in this competitor's positioning. Each weak spot must:

- Be specific (not "they have a generic website").
- Be exploitable by the operator (something the operator can credibly attack with their actual offer).
- Map to the operator's ICP and personas (the buying committee can be moved by this argument).

### Phase 6 - Strategic recommendations

Three to five specific moves the operator should make against this competitor.

| Move | Why |
|---|---|
| Specific positioning copy update | What sentence to change on the operator's site or sales collateral |
| Specific outbound angle | The line that frames the operator vs the competitor in the buyer's first conversation |
| Specific artefact angle | A future signature artefact edition or one-off comparison piece that puts numbers on the gap |
| Specific deal-level objection handling | What to say in a deal where the prospect is comparing operator vs this competitor |
| Specific commercial concession (if needed) | If the competitor has a structural advantage (e.g. lower price), where the operator's pricing or packaging needs to flex |

### Phase 7 - The wedge

One sentence. The single positioning move that beats this competitor on the operator's win axis.

Example for a hypothetical operator vs Synthflow: "Implement AI sells managed labour against hiring cost; Synthflow sells per-minute software against per-minute software. The wedge is to never let the buyer compare per-minute, always compare against hiring."

### Phase 8 - Write the teardown

Use the template below. Save to `/workspace/execution/teardown/<competitor-slug>-teardown.md`.

## Output template

```
# Teardown - <Competitor Name>

## One-liner

<One sentence. The competitor's stated positioning, lifted from their public surface.>

## Their proof points

- **Measurable:** <list>
- **Defensible:** <list>
- **Marketing:** <list>

Ratio: <X% measurable / Y% defensible / Z% marketing>

## Their ICP

- **Stated:** <from their copy>
- **Inferred:** <from their customer logos, pricing tier, sales motion>
- **Mismatch:** <any gap between stated and inferred, with implications>

## Their pricing

<If public, summarise. If not public, note this and infer from sales motion.>

## Head-to-head

<Table: axis | operator | competitor | edge>

## Their weak spots

1. **<Weak spot>** - <why it is exploitable, by which operator argument>
2. ...

## Strategic recommendations

1. **<Move>** - <specific change to make, where>
2. ...

## The wedge

<One sentence. The positioning move that beats this competitor on the operator's win axis.>

## Sources

<List the URLs scraped, with date of scrape. Important for revisiting when the competitor updates their site.>
```

## Quality bar

The teardown is defensible when:

1. Every claim about the competitor is sourced (URL referenced).
2. The marketing/measurable/defensible ratio is honest. Most B2B competitors are 60%+ marketing.
3. Weak spots are exploitable, not generic.
4. Strategic recommendations are specific (named copy changes, named artefact angles, named objection handling lines).
5. The wedge is a single sentence and survives the "what does that mean concretely" follow-up.

If the teardown reads like "they are good at X, we are good at Y," the bar fails. Surface specific positioning gaps the operator can attack.

## Hard rules

- Apply voice rules from `voice.md` to all output.
- Apply sparring discipline if the operator describes the competitor in vague terms ("they are not as good"). Force specificity.
- Never produce a teardown without scraping at least the competitor's main domain. Inferred-from-memory teardowns are not allowed.
- Always include the head-to-head table. The visual comparison is the core of the artefact.
- Refuse to run for competitors the operator names but cannot point at a public surface for. If the competitor is stealth or the operator has no URL, ask for context (sales collateral, briefing notes) before proceeding.

## Hand-off

After writing the teardown:

> "Teardown saved to `/workspace/execution/teardown/<slug>-teardown.md`. Ready inputs: the next deal where you are competing against this competitor, or the next outbound campaign. Want me to draft a proposal that uses this teardown's wedge as the framing? Run 'draft a proposal' next."

Do not auto-run other skills. Operator decides next.
