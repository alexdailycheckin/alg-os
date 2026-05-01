# Build My Funnel - GTM Stack Generator

This file runs when the operator says "build my funnel," "build my GTM stack," "design my funnel," "GTM motion build," "instantiate the Valley playbook for me," "set up my GTM funnel," or any equivalent.

The skill takes the operator's foundation files and the locked artefact spec, and produces a 7-stage GTM funnel build instantiated for the operator's specific reality. The reference shape is the Valley 7-stage playbook at `/02-research/gtm-playbooks/valley-7fig-1person.md`. The skill is the framework's tool to turn that public reference into the operator's own running system.

Read in full before doing anything else.

## What this skill produces

A complete funnel build at `/workspace/funnel/` that includes:

- `funnel-overview.md` - the master one-pager linking every stage, cadence, budget, and operator role.
- `stage-1-content-machine.md` to `stage-7-paid-amplification.md` - one file per Valley stage instantiated for the operator.
- `tools-and-mcp.md` - which tools, which MCP connectors, which integrations are needed at each stage. Cross-references `/workspace/research/capability-snapshot.md`.
- `cadence-and-budget.md` - posting cadence, calling cadence, send cadence per stage, plus the paid amplification budget ramp.
- `dependencies.md` - which artefact spec each stage depends on, which other ALG OS skills the funnel invokes (teardown, proposal, nurture, build-my-agents), and which signals close the loop.
- `quality-checklist.md` - the operator's own checklist before the funnel goes live.

The funnel is operator-reviewed before any stage goes live. The skill produces; the operator approves and runs.

## Inputs the skill reads

| File | Why |
|---|---|
| `/workspace/foundation/voice.md` | All output uses the operator's voice. |
| `/workspace/foundation/brand.md` | Naming convention discipline. |
| `/workspace/foundation/positioning.md` | The win axis the funnel reinforces. |
| `/workspace/foundation/icp.md` | The qualification rule that filters signal at every stage. |
| `/workspace/foundation/personas.md` | Who the buyer is at each ICP entry point. |
| `/workspace/foundation/markets.md` | Geographies and verticals the funnel runs against. |
| `/workspace/foundation/services.md` | What converts at the bottom of the funnel. |
| `/workspace/foundation/pricing.md` | Engagement size used in budget ramp logic. |
| `/workspace/foundation/gtm-motion.md` | The operator's own description of the four-step funnel; cross-checked against the Valley shape. |
| `/workspace/execution/artefact/<slug>-spec.md` | The artefact is stage 1's content engine spine. The funnel cannot exist without a locked artefact spec. |
| `/workspace/research/capability-snapshot.md` | Tools and MCP connectors currently available. |
| `/02-research/gtm-playbooks/valley-7fig-1person.md` | The reference shape. The skill maps each Valley stage to the operator. |
| `/02-research/agent-taxonomy.md` | The agent roles available to ALG OS, used at stages 3 and 5. |

If any required foundation file or the artefact spec is missing, refuse to run. Tell the operator to run intake or "design my artefact" first.

If multiple artefact specs exist, ask the operator which one anchors stage 1 of the funnel.

## Operator inputs

Ask:

1. **Anchor artefact.** If only one artefact spec exists, default to it. Otherwise list and let the operator pick.
2. **Existing channels in flight.** Does the operator already run any of the 7 stages? List which. The skill recommends adjustments rather than greenfield rebuilds.
3. **Tooling preferences.** Operator preferences override the Valley reference's defaults. Examples: existing email outbound stack, existing newsletter platform, existing CRM. The skill uses what the operator has and notes what is missing.
4. **Budget envelope.** A monthly budget ceiling for paid amplification (stage 7) and any tooling cost. Used to cap the cadence and the paid ramp.
5. **Operator headcount.** The Valley playbook is 1 person. ALG OS scales from 1 to 5+. Operator headcount decides which stages compress to digital workers and which stages have human owners.

If any input is missing, surface and ask. Do not silently default.

## Flow

### Phase 1 - Inputs and validation

Read every file in the inputs table. If voice.md, brand.md, positioning.md, icp.md, the artefact spec, or the capability snapshot is missing, refuse to run. Tell the operator which file is missing and which skill produces it.

If the operator's existing GTM motion file (gtm-motion.md) describes a fundamentally different shape (e.g., outbound-led with no artefact engine), surface the conflict. The Valley shape assumes content-led inbound with signal-based outbound. If the operator's reality contradicts that, decide together whether to reshape gtm-motion or skip Valley mapping.

### Phase 2 - Stage-by-stage mapping

For each of the 7 Valley stages, write one file in `/workspace/funnel/`:

#### Stage 1 - Content machine

- **Spine:** the locked artefact spec. The artefact is the content engine. Each edition produces 12 to 16 LinkedIn posts plus 1 to 2 podcast episodes plus a newsletter plus the press release plus partner-amplification copy.
- **Authors:** the operator's senior brand voices (Head of Growth, Chairman, CEO depending on the operator). Posts attributed by role; the actual byline is set at publish time.
- **Cadence:** target 5 to 7 posts per week across the operator's senior brand voices, mapped explicitly to TOF, MOF, BOF.
- **Topic mapping (TOF / MOF / BOF):** the artefact spec's 'distribution plan' provides the source. The skill maps each post to a funnel stage.
- **Tools:** any LinkedIn scheduling tool the operator already uses, plus the artefact production skill's `published/` outputs as source assets.
- **Quality bar:** every post must trace to a specific finding in the latest artefact edition. No generic thought-leadership posts.

#### Stage 2 - Signal capture

- **What is captured:** profile viewers, post engagers, followers, web visitors, competitor engagers, podcast listeners. ICP-qualified by `icp.md` rules.
- **Tools:** the operator's signal-capture stack from `capability-snapshot.md`. Examples: AIOS Command (operator-built), RB2B (web visitor identification), LinkedIn Sales Navigator, the company's own product if it doubles as a signal-capture platform.
- **Qualification rule:** apply the ICP-fit logic from `icp.md` automatically. High, medium, low. Out-of-ICP removed. Contacts enriched.
- **Volume target:** define the expected ratio of raw engagement to ICP-qualified signal per channel (for example, 1 in 4 LinkedIn post engagers).

#### Stage 3 - Personalised outreach

- **Trigger:** ICP-qualified signal from stage 2.
- **Channel mix:** LinkedIn DM, email, or both depending on the signal's channel of origin.
- **Personalisation source:** the teardown skill output for each named account. The teardown's 'weak spots' and 'the wedge' sections produce the per-account opener.
- **Tools:** the operator's outreach tool (e.g., the company's own product if it ships AI agents, otherwise a stack of teardown skill output + a sender like Instantly or HubSpot).
- **Reply rate target:** define a benchmark per channel. The Valley reference shows 30%+ on warm signal, 5 to 10% on cold.
- **Routing:** positive replies go to a calendar booking link; hot signals route to the senior brand voice (Head of Growth) for personal handling.

#### Stage 4 - Multichannel lead capture

- **Sequences in parallel:**
  - Newsletter via the operator's existing newsletter platform.
  - Product or trial-update emails via a sequencing tool.
  - Web visitor identification via the operator's stack.
  - Inbound qualification (a tool that scores form fills and inbound).
  - Routing notification to the team (Slack channel, Teams channel, or email digest).
- **Time-to-conversion:** the Valley reference shows 3 weeks to 3 months. Operators with shorter sales cycles compress the sequence; longer cycles extend it.
- **Tools:** map each parallel sequence to a tool from `capability-snapshot.md`. Flag any gaps.

#### Stage 5 - Email outbound

- **Cold outbound:** addressed to in-ICP accounts who have not yet signalled. Source: the same artefact-derived data the warm outbound uses, minus the engagement filter.
- **Reply routing:** positive replies route into the operator's pipeline tool with a personalised follow-up (a video walkthrough, an account-specific brief, or a calendar link).
- **Volume cap:** define a weekly outbound cap. Cold outbound at scale damages domain reputation and brand. The cap forces the channel to remain a precision instrument.
- **Tools:** the operator's cold outbound stack (Instantly, HubSpot Sequences, Smartlead, etc.).

#### Stage 6 - Affiliate

- **Eligibility:** PE/VC operating partners with portfolio exposure, trade bodies, named consultants. The artefact spec's 'partner amplification' line is the seed list.
- **Rev share structure:** the Valley reference uses 20% lifetime. Operator decides the structure based on margins and engagement size from `pricing.md`.
- **Tools:** an affiliate management platform (Tolt, Rewardful, or built-in CRM features).
- **Threshold for activation:** stage 6 turns on once the artefact is in its second or third edition and the operator has a stable conversion pattern from stages 4 and 5. Premature activation burns partner goodwill.

#### Stage 7 - Paid amplification

- **Rule:** paid only goes behind content that already resonated organically. No paid-first.
- **Channels:** LinkedIn (B2B operators), Google search (intent capture for the artefact's head terms), retargeting (web visitors who did not convert).
- **Budget ramp:** light at edition 1 of the artefact. Scaled at edition 3 once SEO ranks compound. The exact figures pull from the artefact spec's 'paid amplification' line if present, otherwise from the operator's budget envelope.
- **Targeting:** by ICP title and company size band, never by interest or generic vertical.

### Phase 3 - Tools and MCP blueprint

Write `/workspace/funnel/tools-and-mcp.md` with one row per stage:

| Stage | Tool category | Operator's chosen tool | MCP connector available | Status |
|---|---|---|---|---|

For each stage, fill in:
- The category (e.g., LinkedIn scheduler, web visitor ID).
- The operator's chosen tool (default to what is in `capability-snapshot.md`; ask if unclear).
- Whether an MCP connector exists for it (cross-reference `capability-snapshot.md`).
- Status: `live`, `wired`, `tooling chosen, integration pending`, `tool not yet chosen`.

The blueprint becomes the input to `build-my-agents` for any stage that should run as an automated agent rather than a human task.

### Phase 4 - Cadence and budget

Write `/workspace/funnel/cadence-and-budget.md`:

- **Posting cadence per author per week.**
- **Outreach cadence (warm and cold) per week.**
- **Newsletter and product-update send cadence.**
- **Paid amplification budget per artefact edition** (light at edition 1, scaled at edition 3 unless the operator overrides).
- **Total tool spend per month** (rolled up from the tools-and-mcp blueprint).
- **Revenue assumptions** (using `pricing.md` engagement-size benchmarks against the Valley reference's pipeline-to-revenue ratios; flag the assumption explicitly).

### Phase 5 - Dependencies

Write `/workspace/funnel/dependencies.md`:

- **Artefact spec dependency:** which spec anchors stage 1. If the spec is paused, stage 1 stalls and stages 2 to 7 starve.
- **Other ALG OS skill dependencies:** teardown (stage 3 personalisation), proposal (stage 5 reply handling), nurture (stage 4 multichannel sequences), build-my-agents (any stage automated).
- **Closed-loop signals:** which inbound signal (from the artefact's signal-log file or equivalent) feeds back into which stage. Stage 1 cadence adjusts based on stage 2 capture rate; stage 5 cap adjusts based on stage 3 reply rate; etc.

### Phase 6 - Quality checklist

Write `/workspace/funnel/quality-checklist.md`. 10 items. Three failures kill the funnel build. Fix and re-run before declaring complete.

1. **Anchor artefact spec exists and is locked.** Stage 1 has a concrete content engine, not an aspiration.
2. **Every stage has a named tool or a flagged gap.** No empty cells in the tools-and-mcp blueprint.
3. **Cadence numbers are specific.** "Frequent" fails. "5 LinkedIn posts per week split across Head of Growth (3) and Chairman (2)" passes.
4. **ICP qualification rule is automated, not aspirational.** If stage 2 says "we will manually qualify" the funnel breaks at scale; flag the gap.
5. **Stage 3 personalisation traces to teardown output.** Generic outreach templates fail the bar.
6. **Stage 4 has at least 3 parallel sequences.** Newsletter alone is not multichannel.
7. **Stage 6 activation threshold is documented.** No premature affiliate launches.
8. **Stage 7 has a 'paid only follows resonance' gate.** No paid-first traps.
9. **The closed-loop signal back to stage 1 is documented.** Without it, the funnel does not compound.
10. **The funnel is achievable at the operator's headcount.** If the operator is 1 person, the human-owned tasks must total under 20 hours per week with the rest absorbed by digital workers.

If 3 or more fail, do not write to `/workspace/funnel/`. Surface and fix.

### Phase 7 - Hand-off

Tell the operator:

> "Funnel build ready at `/workspace/funnel/`. Files: funnel-overview.md (master), 7 stage files, tools-and-mcp.md, cadence-and-budget.md, dependencies.md, quality-checklist.md. Review the overview first, then approve each stage, then run `build my agents` to turn the automatable parts into running agent definitions."

Do not auto-deploy. Do not auto-run any stage. The operator reviews the build and decides what to enable, in what order.

## Hard rules

- Apply voice rules from `voice.md` throughout.
- Never invent capabilities. Every tool referenced traces to the operator's choice or the capability snapshot.
- Never assume a stage is live. Default to "tooling chosen, integration pending" unless the capability snapshot says otherwise.
- Never deviate from the operator's positioning. The funnel reinforces the win axis from `positioning.md`; if a Valley stage would dilute the win axis, surface and adjust.
- The artefact spec is the spine. If the spec changes, the funnel is rebuilt. The build cannot be permanent infrastructure independent of the spec.
- Personnel: refer to roles, not specific names. The funnel is a framework artefact and the operator's specific personnel are recorded in `team.md`.
- Hand-off, not auto-execution. The skill produces a build. The operator decides what to launch.

## Hand-off integration with build-my-agents

After this skill produces the funnel build, the operator can run `build my agents` against the same inputs to turn the automatable parts of stages 2 to 5 into running agent definitions in `/workspace/agents/`. The funnel build is the strategy layer; the agent stack is the execution layer.

Ordering:

1. `design my artefact` produces the spec.
2. `produce my artefact edition` produces the canonical edition + rendered formats.
3. `build my funnel` (this skill) produces the GTM stack architecture.
4. `build my agents` produces the agent definitions that automate stages 2 to 5.
5. The operator launches stages incrementally, monitored by the per-edition signal log.
