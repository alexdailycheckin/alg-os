# Agent Taxonomy

The catalogue of agent categories ALG OS can recommend, organised by capability, with provider options for each. The recommendation engine in Build 3 reads from this file. Capability sync (mode 1) annotates this file's entries with current platform state but does not modify the file at runtime.

Read in conjunction with `foundation.md` section 9.

## How to read this file

Each category has four tiers. The recommendation engine ranks tiers in this order when an operator runs a skill that needs an agent in that category.

| Tier | When to recommend |
|---|---|
| 1 - Native | The work can be done by the operator's primary AI (Claude in v1) without extra tooling. Lowest cost, fastest deploy. |
| 2 - Specialist | The work needs a dedicated tool because native quality is materially below the specialist's. Voice and audio is the canonical example. |
| 3 - Custom orchestration | The work needs multiple capabilities composed in a non-trivial way. Three named build paths: in-house build, freelancer marketplace, AI consultancy. ALG OS does not prefer one shop. |
| 4 - Third-party SaaS | The work is best served by a SaaS product the operator already pays for or should pay for. Named alternatives, no kingmaker. |

## Hard rules

- Vendor neutrality. Three or more named alternatives per tier where alternatives exist. No tier 4 entry has a single vendor unless the category has only one usable provider.
- Quality over completeness. If a category has 50 vendors but only 3 produce usable agents, list the 3. Operators who want exhaustive lists go to G2.
- Capability sync runtime annotations. Mode 1 reads this file and tags entries that have shifted in the last 90 days (e.g. Claude shipped native voice, retire the tier 2 voice provider as the default). Annotations write to `/workspace/research/capability-snapshot.md`, not back into this file.
- Updates to this file ship via tagged framework releases. Operators pick them up via `alg-upgrade`.

## Categories

### 1. Prospecting and account research

Identifies target accounts, surfaces signals (funding, hiring, technographic), enriches contact records.

| Tier | Recommendation |
|---|---|
| 1 - Native | Claude with web research tools (`web_fetch`, `web_search`, MCP-connected sources) handles target-account research and signal capture for low-volume operators. Strongest where the operator has already named the ICP and just needs research depth per account. |
| 2 - Specialist | None today. Native is sufficient unless volume exceeds what conversational research can produce. |
| 3 - Custom orchestration | Composite agents combining web research, social signal monitoring, and CRM enrichment at high volume. Build paths: in-house engineering team, AI freelancer marketplace, AI consultancy. |
| 4 - Third-party SaaS | Apollo, Clay, ZoomInfo, Cognism, Lusha, Ocean.io. Pick by data quality in your geography and ICP overlap. Clay is strongest for pipeline composability, Apollo for raw breadth, ZoomInfo for enterprise depth, Cognism for European compliance. |

### 2. Data enrichment and signal capture

Adds attributes to records (company size, technographic, funding, intent signals) at scale.

| Tier | Recommendation |
|---|---|
| 1 - Native | Claude can enrich a small batch (under 100 records) using web research. Native is not the answer for thousands of records per week. |
| 2 - Specialist | None. Enrichment is a SaaS-led category. |
| 3 - Custom orchestration | Composite enrichment pipelines combining multiple data providers, scoring logic, and CRM write-back. Build paths: in-house engineering team, AI freelancer marketplace, AI consultancy. |
| 4 - Third-party SaaS | Clay (composable enrichment), Apollo (built-in), ZoomInfo, Cognism, LeadIQ, Bombora (intent), G2 (intent), 6sense (intent + scoring). Pick by data accuracy in your ICP. |

### 3. Call analysis and conversation intelligence

Records calls, transcribes, scores, surfaces insights, drafts follow-ups.

| Tier | Recommendation |
|---|---|
| 1 - Native | Claude handles transcription analysis and summarisation if the operator brings the transcript text. Native is strong for ad-hoc analysis, weak for continuous conversation intelligence at scale. |
| 2 - Specialist | None. SaaS dominates this category. |
| 3 - Custom orchestration | Composite agents combining transcript ingestion, scoring frameworks (e.g. MEDDIC, BANT), CRM write-back, and coaching surface. Build paths: in-house, freelancer marketplace, AI consultancy. |
| 4 - Third-party SaaS | Gong, Chorus, Avoma, Fireflies, Clari Copilot, ExecVision. Gong is strongest for revenue intelligence at scale, Chorus for sales coaching, Fireflies for affordable transcription + meeting notes, Avoma for combined meeting + revenue intelligence. |

### 4. Content production (text, image, video)

Drafts written content, generates images, produces video. Spans long-form blog, sales collateral, social, ads.

| Tier | Recommendation |
|---|---|
| 1 - Native | Claude is strongest for long-form text, brand-voice extraction, and structured documents (proposals, briefs, reports). Native handles 80% of B2B content needs once `voice.md` is calibrated. |
| 2 - Specialist | Image: Midjourney, DALL-E, Adobe Firefly, Stable Diffusion. Video: Runway, Synthesia, HeyGen, Descript. Audio narration: ElevenLabs, PlayHT. Pick by output style your brand uses. |
| 3 - Custom orchestration | Multi-format pipelines (e.g. blog plus social plus video) with brand-voice consistency checks. Build paths: in-house, freelancer marketplace, AI consultancy. |
| 4 - Third-party SaaS | Jasper, Copy.ai, Writer, Anyword for text. Canva, Visme for design with AI assistance. Most operators do not need these on top of native Claude unless they require non-Claude voice or design templates at volume. |

### 5. Voice and audio agents

Inbound and outbound voice. Real-time conversation, IVR replacement, after-hours coverage.

| Tier | Recommendation |
|---|---|
| 1 - Native | Native voice from Claude is not yet generally available for production voice agents. Capability sync flags this entry the moment it changes. |
| 2 - Specialist | ElevenLabs, Synthflow, Retell AI, Bland AI, Vapi, PlayHT. ElevenLabs is strongest for voice quality, Synthflow and Retell for end-to-end agent platforms with low latency, Bland for high-volume outbound, Vapi for developer-led builds. |
| 3 - Custom orchestration | Composite voice agents with CRM context, post-call action execution, and handoff to human. Build paths: in-house, freelancer marketplace, AI consultancy. |
| 4 - Third-party SaaS | None at the platform layer that beats specialist providers above. |

### 6. Browser-use and computer-use agents

Executes tasks against legacy SaaS where no API exists. Simulates a human at a keyboard.

| Tier | Recommendation |
|---|---|
| 1 - Native | Claude has computer-use capability for desktop applications and browsers. Strong for ad-hoc workflows, requires careful scope. Capability sync tracks computer-use evolution. |
| 2 - Specialist | None. Computer-use is a relatively new category and quality is consolidating around foundation-model providers. |
| 3 - Custom orchestration | Composite agents combining computer-use, OCR, vision, and rule-based fallback for legacy systems. Build paths: in-house, freelancer marketplace, AI consultancy. |
| 4 - Third-party SaaS | Adept, Bardeen, Multion, Browserbase. Most are early-stage. Buyer beware on production reliability. |

### 7. CRM hygiene and lifecycle automation

Keeps CRM data clean, deduplicates, enriches, runs lifecycle workflows (onboarding, renewal, churn risk).

| Tier | Recommendation |
|---|---|
| 1 - Native | Claude with MCP-connected CRM (HubSpot, Salesforce, Attio) handles ad-hoc hygiene and small-scale lifecycle work. Native is weak for high-volume continuous workflows. |
| 2 - Specialist | None. CRM hygiene is SaaS-led. |
| 3 - Custom orchestration | Composite agents for cross-CRM data quality, duplicate detection, lifecycle stage automation. Build paths: in-house, freelancer marketplace, AI consultancy. |
| 4 - Third-party SaaS | HubSpot Operations Hub, Salesforce Data Cloud, Insycle, Validity DemandTools, RingLead. Pick by primary CRM. |

### 8. Outbound execution (email, LinkedIn, SMS)

Runs sequences across channels. Personalisation, deliverability, cadence management.

| Tier | Recommendation |
|---|---|
| 1 - Native | Claude drafts outbound but does not execute at scale. Native is the right place to write personalised one-to-ones (the right call most of the time post-2025 given convergence). |
| 2 - Specialist | None. SaaS dominates outbound execution. |
| 3 - Custom orchestration | Composite agents combining personalisation logic, multi-channel cadence, and reply handling. Build paths: in-house, freelancer marketplace, AI consultancy. |
| 4 - Third-party SaaS | Outreach, Salesloft, Apollo (built-in), Lemlist, Smartlead, Instantly. Pick by deliverability and team size. Smartlead and Instantly for small teams optimising deliverability, Outreach and Salesloft for enterprise sales, Apollo for combined data + execution. |

### 9. Inbound qualification and routing

Qualifies leads on inbound (chat, form, call). Routes to the right person or workflow.

| Tier | Recommendation |
|---|---|
| 1 - Native | Claude with MCP-connected inbox or chat handles low-volume inbound qualification. Strong for nuanced qualification logic, weak for high-volume real-time chat. |
| 2 - Specialist | None at the qualification layer. Voice tier 2 (section 5) covers inbound voice. |
| 3 - Custom orchestration | Composite agents combining chat, form intake, qualification scoring, and routing logic. Build paths: in-house, freelancer marketplace, AI consultancy. |
| 4 - Third-party SaaS | Drift, Intercom, Qualified, Default, ChiliPiper (routing), Calendly (booking). Pick by primary inbound channel and CRM stack. |

### 10. Attribution and reporting

Tracks pipeline source, multi-touch attribution, conversion rates, content effectiveness.

| Tier | Recommendation |
|---|---|
| 1 - Native | Claude with MCP-connected analytics handles ad-hoc reporting and pipeline analysis. Weak for continuous attribution that requires data warehousing. |
| 2 - Specialist | None. Attribution is data-warehouse-led. |
| 3 - Custom orchestration | Composite agents combining warehouse reads, attribution model logic, and dashboard generation. Build paths: in-house, freelancer marketplace, AI consultancy. |
| 4 - Third-party SaaS | Dreamdata, HockeyStack, Segment, RudderStack (instrumentation), Looker, Tableau, Mode (BI). Pick by data warehouse. Dreamdata and HockeyStack are strongest for B2B revenue attribution out of the box. |

## Categories not covered (yet)

The taxonomy ships with the 10 categories above. Real operator usage will surface gaps. Add new categories via PR. Examples that may land in v1.1 or later:

- Account-based intent and surfacing
- Vertical-specific agents (legal, healthcare, financial)
- Internal knowledge management and team enablement
- Pricing and quote-to-cash agents
- Customer success and renewal agents
- Procurement and vendor management agents

## How skills use this file

Build 2 skills do not consume this file directly. Build 3 (the recommendation engine) is the primary consumer. The recommendation engine reads:

1. The operator's `services.md` (tier 4 mode: product-recursive vs tool-agnostic).
2. This file (the available agent options per category).
3. `/workspace/research/capability-snapshot.md` (the current platform reality).

The recommendation engine outputs, for each agent the operator's GTM motion needs:

- Tier 1 if native is sufficient.
- Tier 4 if the operator already has a SaaS that fits.
- Tier 4 with a recommended addition if not.
- Tier 3 with all three build paths if no SaaS fits.
- Tier 2 if a specialist is genuinely required.

Until Build 3 ships, the agent taxonomy is documentation. Operators can read it manually and pick from it.
