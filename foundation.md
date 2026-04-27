# ALG OS - Foundation Document

**Agent-Led Growth Operating System**
**Author:** Alexandru Muresan
**Status:** v0.4 - Pre-build foundation (QA-resolved)
**Date:** April 2026

---

## 1. Purpose of This Document

This is the source-of-truth foundation document for ALG OS, a personal project owned by Alexandru Muresan. It captures the rationale, the strategic thesis, the architecture decisions, the constraints, and the 90-day plan to build and validate it.

Claude Code should treat this document as the canonical brief. Every directory, file, skill, and agent in the resulting repo should trace back to a section in here. If something in the build doesn't have a justification in this document, it should be questioned before being added.

ALG OS is brand-neutral, tool-agnostic in its public form, and built to work for any business in any vertical. It is independent of any specific company including Implement AI. Implement AI may use ALG OS internally, the same way any other operator can, but Implement AI is not the parent brand and gets no preferential treatment in the recommendation engine.

---

## 2. Origin and Background

### 2.1 The Operator Context

ALG OS originates from a personal library of Claude skills, markdown knowledge bases, and MCP integrations built by Alexandru while running commercial functions at AI companies. The library compresses days of strategic work into minutes for the specific company it was built for. ALG OS is the abstraction of that library into a universal framework any operator can fork and run on their own business.

### 2.2 The Problem That Triggered ALG

Cold outbound is converging. Apollo, Clay, GPT, the same playbook. Reply rates have collapsed because buyers' defences (AI summarisers, banner warnings, sender-pattern deletion) have evolved faster than the offence. Personalisation at scale produced false intimacy that buyers can now detect at distance.

Doing the same thing better is a losing trade. The market needs a different category of motion, not a refinement of the existing one. ALG OS is an attempt to define and operationalise that category.

### 2.3 The Inspiration Layer

Three influences shaped the architecture.

Kieran Flanagan's four-layer GTM stack (foundation, research, execution, feedback) was the spine. It separates context, intelligence, output, and learning into distinct, composable layers.

Steve Jobs' product discipline (kill 90% of the line, make the remaining 10% inevitable) drove the decision to limit ALG to five surgical skills, with operators able to extend using their own learnings.

Elon Musk's first-principles approach (rebuild from physics, not market convention) drove the central question: what is the marginal cost of producing one piece of attention-grade intelligence about a buyer, distributed to that buyer, in a way that creates inbound demand. ALG OS does not impose a cost target. Cost varies by operator and artefact type and is the operator's call.

---

## 3. The Diagnosis

The honest assessment of the state most growth teams are in.

Most operators have a content production system, not an outreach machine. A content system makes things faster. An outreach machine converts strangers into qualified buyers at decreasing cost per buyer over time.

Content systems don't decrease cost per buyer because nothing compounds. Each artefact dies after it's sent. The data doesn't build a moat. The brand doesn't accrue equity in any vertical. Tools get added but customers don't get cheaper to acquire.

ALG OS exists to close this gap. The output is not faster content. The output is a GTM motion where the unit economics improve quarter on quarter because the artefacts compound and the data compounds.

---

## 4. The Strategic Thesis

### 4.1 The Core Idea

The product produces the marketing. The marketing demonstrates the product. They are the same thing.

For product companies, this means the agents executing the GTM motion are powered, where possible, by the company's own product. Lemlist's prospecting agent is built on Lemlist. Clay's enrichment agent is built on Clay. Gong's call-analysis agent is built on Gong. Every demo of the GTM motion is a demo of the product.

For service companies and operators without a recursive product, this means the agents produce signature intelligence (industry indices, audits, benchmarks) that becomes the inbound mechanism. The artefact is the marketing.

### 4.2 The Signature Artefact

The unit of compounding is the signature artefact. Quarterly. Free to claim by named entities in the data set. Published on the operator's domain. Press-released. Indexed by Google.

Examples of what the diagnostic might propose for different operators:

A multi-location healthcare or services chain: a Quarterly Customer Experience Index based on mystery shopping data.

A B2B SaaS company: a Time-to-Value Audit comparing onboarding speeds across the category.

A recruitment firm: a Candidate Experience Report scoring named hiring brands.

A plumbing or trades franchise: a First Call Resolution Benchmark.

A law firm: a Client Response Time Index in their practice area.

A financial services brand: a Switching Friction Report for current account or pension providers.

A logistics or 3PL: a Delivery Promise vs Reality Index.

The artefact is the outreach. The email that delivers it is confirmation, not initiation. Buyers today are search-led, not inbox-led. The artefact puts the operator permanently inside the consideration set when a prospect searches for the category.

The data moat compounds quarter by quarter. Year 2 has longitudinal trends that competitors cannot reproduce without 12 months of catch-up. Year 3 the data subscription itself becomes a product line.

### 4.3 The Funnel Pattern

Every ALG-designed motion follows a consistent shape, instantiated differently by vertical and product type.

The artefact reveals an external truth (a leak, a gap, a benchmark).

The buyer asks the natural next question (what does this look like inside my own business).

The operator's product, or a recommended tool, answers that question with a low-commitment first step.

The full deployment closes the gaps the first step surfaced.

ALG's job is to design the right four-step shape for the operator running it. The shape is universal. The components are specific to the business.

---

## 5. The Four-Layer System

Adopted from Kieran Flanagan, refined for ALG OS.

### 5.1 Layer 1 - Foundation

Context layer. Brand, ICPs, services, markets, positioning, team, stakeholders, budgets, pricing, personas, banned words, voice rules. All in markdown. All loadable on demand.

ALG OS templates this layer so any operator can fork the repo, run an intake, and generate their own foundation self-serve. The intake gates progression on quality, not on time (see section 10.3).

### 5.2 Layer 2 - Research and Reach

Real-time market and audience intelligence, plus deal and customer context, fed via MCPs only when tasks need it. Balancing act: load too much, clog the context; load too little, generic output.

ALG OS Layer 2 is MCP-config-driven. The repo specifies the data sources required per artefact type. The execution is whatever MCPs the operator has connected (Fireflies, Slack, Microsoft 365, monday.com, Gmail, Calendar, Drive, Airtable, plus whatever the operator brings).

This layer also houses the agent taxonomy (see section 9).

### 5.3 Layer 3 - Execution

The four canonical skills, shipped with the repo.

The Artefact (signature artefact generator).
The Teardown (competitor and positioning analysis).
The Proposal (post-discovery client document).
The Nurture (post-proposal email sequence).

Every skill reads Layer 1, optionally pulls from Layer 2, produces output that matches voice and format. Every skill enforces a quality checklist before completion.

Operators extend this layer with their own skills. The intake asks what additional skills the operator wants based on their motion type (e.g. a PLG-led SaaS operator may need an Onboarding skill, an operator with a delivery team may need a Handoff skill). The four canonical skills are the floor, not the ceiling.

An earlier draft listed five canonical skills including a Handoff (internal solutions team brief). Operator testing surfaced that handoff is situational, not universal. Solo operators and motion types without a delivery team get no value from it. Handoff was demoted to an operator-extension example. Operators with delivery teams write their own handoff skill in `/workspace/execution/handoff/`.

### 5.4 Layer 4 - Feedback and Iteration

Ships as a minimal-viable structure: a feedback log per artefact, a quarterly review cadence, and a foundation-history log inside `/workspace/feedback/` that records why the operator's foundation files changed over time (distinct from the repo-root `CHANGELOG.md`, which tracks framework releases). GitHub Issues serve as the capture mechanism for framework-level feedback in v1. Automation comes later.

---

## 6. ALG OS as a Product

### 6.1 Positioning

ALG = Agent-Led Growth. Distinct from Product-Led Growth. PLG works because users self-serve into value. ALG works because agents don't just power the growth motion, they ARE the growth motion. The agent prospects. The agent produces the artefact. The agent runs the audit. The agent does discovery. The agent demos itself.

The naming is intentional and brand-neutral. Workforce-Led Growth was considered but ties the framework to specific commercial tooling. ALG stays open.

### 6.2 The Two Modes

ALG operates in one of two modes per operator, selected by the intake diagnostic.

**Product-recursive mode.** For product companies. ALG ingests the company's product capabilities and maps them to the agents the GTM motion needs. The agents executing outreach are powered by the company's own product. Lemlist's prospecting agent runs on Lemlist. Gong's call-analysis agent runs on Gong. HubSpot's lifecycle agent runs on HubSpot.

**Tool-agnostic mode.** For service companies, agencies, consultancies, and any operator without a recursive product. ALG recommends best-in-class tools per agent. Three tiers in the recommendation: tools the operator already has, tools they should add (with rationale), composite alternatives if relevant.

### 6.3 Honesty Constraints

ALG has to be honest when an operator's product can't power a given agent. If a tool needs a "post-call summary agent" and the operator's product doesn't do call recording, ALG says so and offers options: use a third-party tool, build custom, or skip the agent. No pretending the product can do something it can't.

ALG never recommends any single AI consultancy or custom-agent shop by default. The recommendation engine treats this category as fully open. Operators who need custom agents see multiple options (consultancies, freelancer marketplaces, in-house build paths) and pick. ALG isn't the kingmaker.

### 6.4 Open Mode

ALG works for everyone who runs it, including direct competitors of any company Alexandru is associated with. The framework's value comes from becoming the category standard. Excluding competitors makes ALG a marketing tool for one company and destroys the neutrality that makes it interesting. The trade is acceptable.

---

## 7. The Sparring Layer

The intake diagnostic is the moat. Most "AI for GTM" tools accept whatever the user types and generate from it. Garbage in, polished garbage out.

ALG refuses weak inputs. Examples of the sparring behaviour:

User says "our ICP is mid-market companies." ALG responds: that's a TAM, not an ICP. Pick a vertical, a revenue band, a trigger event, and one named pain. Try again.

User says "we differentiate on quality." ALG responds: every competitor says that. Name a measurable proof point or pick a different angle.

User says "our signature artefact is industry insights." ALG responds: what insights, whose data, why would the buying committee actually read it. Three sentences.

User says "we sell to enterprises." ALG responds: name three. What was the trigger event for each. What did the buying committee look like. Three sentences.

The system iterates until inputs clear a quality bar. Then and only then does it generate the foundation files.

The intake also asks the operator at the start: British or American English for all output. This sets the voice override that all skills read.

This is Toyoda's five whys applied to GTM intake. It is the unsexy bit most operators will hate for ten minutes and love for a year. The ones who hate it for a year aren't the target users.

The sparring layer is the bit that travels across verticals. It is the first build priority. Without it, every downstream skill is back-fitted to assumptions the intake never validated.

---

## 8. The Artefact Skill (Signature Artefact Generator)

The skill that takes an operator's business and helps them design THEIR signature artefact. Not a template. A diagnostic.

The pattern the Artefact skill looks for: high-ticket, service-heavy, customer-facing businesses where the buying committee already suspects there's a leak but can't measure it. The artefact must be something the operator can produce repeatedly with their own digital workforce or stack, at marginal cost low enough to give away.

The skill interrogates the business and proposes 3 candidate artefacts. The operator picks one. The system specs the data sources, the production cadence, the distribution channels.

Where the operator's business doesn't fit the high-ticket pattern (e.g. low-ACV B2B SaaS, transactional e-commerce), the skill proposes alternative artefact types: state-of-category reports, anonymised benchmark studies, industry-wide diagnostic tools. The diagnostic is honest about which model fits.

This is the bit that doesn't exist yet anywhere. It will need to be built from scratch.

---

## 9. Agent Taxonomy

A living document at `/02-research/agent-taxonomy.md`. Lists the agent categories ALG can recommend, organised by capability, with provider options for each.

Starting categories (extensible):

Prospecting and account research.
Data enrichment and signal capture.
Call analysis and conversation intelligence.
Content production (text, image, video).
Voice and audio agents.
Browser-use and computer-use agents.
CRM hygiene and lifecycle automation.
Outbound execution (email, LinkedIn, SMS).
Inbound qualification and routing.
Attribution and reporting.

For each category, the taxonomy lists:

What Claude can do natively.
What needs a specialist tool to do well (with named alternatives, e.g. voice/audio agents typically need a dedicated voice provider).
What needs custom orchestration (composite agents that combine multiple capabilities, with neutral build paths: in-house build, freelancer marketplaces, AI consultancies). Multiple options per category, no single shop preferred.
What needs a third-party SaaS tool (with named alternatives).

This taxonomy is the catalogue the recommendation engine reads from. New agent categories are added to the framework taxonomy as the market evolves, and ship to operators via tagged releases. Capability sync (section 10.2) calibrates each operator's working recommendation state at first run and surfaces relevant deltas on demand.

The taxonomy is opinionated about quality. If a category has 50 vendors but only 3 produce usable agents, the taxonomy lists the 3. Operators who want exhaustive lists go to G2.

---

## 10. Architecture Decisions

### 10.1 Claude-First

ALG OS is built on Claude. This is a constraint, not a hedge. "Built on Claude" is a position. It cuts scope, sharpens output quality, and aligns with the existing skills library that seeded ALG.

The operator interface is Claude Desktop. The operator forks the repo locally, opens Claude Desktop, points a project at the cloned repo, and runs the intake conversationally. Framework files (skills, templates, prompts) live in the repo as markdown under their respective directories. Operator content (foundation files, generated outputs, research, feedback) saves to `/workspace/` per section 10.6. v1 ships with this single interface. CLI for power users and hosted multi-tenant SaaS are v2 and v3 questions.

Other models may be used by individual operators inside their own ALG deployments if they wire it up themselves. The shipped framework, the skills, the agents, the documentation all assume Claude.

### 10.2 Capability Sync

Capability sync's job is to make ALG OS time-resilient. Whether an operator forks the repo today or 6 months from now, the recommendation engine, agent taxonomy, and skill defaults must reflect current platform reality, not a snapshot of what was available when ALG OS last shipped.

It pulls from three sources.

Anthropic's docs and changelog (web fetch on docs.claude.com and the model release notes).

The MCP registry to see what connectors exist.

The repo's own CHANGELOG.md for skills added or upgraded.

Capability sync runs in two modes.

**Mode 1: first-run calibration.** At intake, the framework reads current state and uses it to set the operator's agent taxonomy, recommendation engine entries, and skill defaults correctly for the moment they fork. This runs invisibly. The operator does not see a release log on day 1. They see a framework that is calibrated to what is actually available.

**Mode 2: on-demand re-sync.** The operator runs it manually when they want to know what has changed since their last calibration. Output is filtered hard against their config and only surfaces material changes against three relevance gates: a new Claude capability that affects an agent currently routed to a third-party tool, a new MCP that connects to a data source already in the research plan, or a canonical skill upgrade that affects work the operator has already shipped. If none of those fire, output is "nothing material since last run." That is the right answer most of the time.

No session-level trigger. No scheduled background runs in v1. Both modes are operator-initiated and run through the operator's Claude Desktop subscription, no API credits required. Implementation starts with manual `web_fetch` calls inside the sync routine. Scheduled background pulls are a v2 question.

### 10.3 The Quality Bar

The intake takes whatever time is needed to produce a foundation strong enough to drive a defensible next step. There is no clock. The gate is output quality.

The discipline still cuts hard, but it cuts on the output surface, not on intake speed. Five canonical skills, not fifty. One signature artefact, not a content calendar. Every feature defends its place by improving the output, not by fitting a time budget.

The version that wins is the one that produces foundation files an operator trusts enough to run skills against without rework. If that takes a focused afternoon, fine. If it takes a week of intermittent work spread across calendar time, also fine. What is not fine is shipping a foundation that produces generic output downstream because the intake let weak inputs through.

The only constraint on intake time is the no-consulting rule. The operator must be able to complete the intake without synchronous 1:1 support. Self-serve, paced by the operator, gated by quality.

### 10.4 Data Ingestion

Three channels, run in sequence. Each has a defined job. The sparring layer's quality bar applies to content from all three, regardless of source.

**1. File upload (runs first).** Operator drops in product spec sheets, sales decks, customer lists, brand guidelines, existing content, transcripts. The framework ingests and parses into Layer 1. Existing artefacts are more authoritative than operator recall, so they go in first. Accepted formats: PDF, .docx, .pptx, plain markdown, .txt, .csv. Raw spreadsheet exports beyond simple lists are flagged for cleanup before ingestion rather than parsed blindly.

**2. Online research (runs second).** The framework runs `web_fetch` and `web_search` against the operator's website, LinkedIn company page, public reviews, competitor sites, industry press, and any URL the operator points it at. Driven by an intake-generated research plan. Catches signal the operator would not think to mention.

**3. Interactive intake (runs third, carries the quality bar).** Operates in two modes against the populated state from steps 1 and 2.

*Free-form extraction.* Operator volunteers context as long-form text, voice notes converted to text, message threads, brain dumps. The framework parses, extracts structured signal, and reflects back what it understood for verification. Most non-technical operators communicate this way by default. The framework meets them where they are rather than forcing form-fill discipline.

*Targeted sparring.* Framework asks pointed questions to fill gaps and pressure-tests inferred content from any source. If a brand doc says "we target mid-market companies," the sparring layer still flags that as a TAM, not an ICP, and forces refinement. Origin of the weak content does not matter. The quality bar is the same.

Iteration continues until Layer 1 is coherent and defensible. The order is fixed (uploads, then research, then interactive) but the interactive layer is non-linear: extraction and sparring interleave as the operator provides more context.

### 10.5 Data and Multi-Tenancy

Every operator's company data lives somewhere. ALG architects multi-tenancy and data isolation from day one. v1 ships with a simple "one repo per operator" pattern (each user forks). Hosted multi-tenant SaaS is a v3 question.

### 10.6 Versioning and Upgrades

ALG OS is a living framework. Skills improve, the agent taxonomy expands, the intake gets sharper. Operators who forked at v1.0 must be able to pick up v1.2 without losing their data and without doing a manual git merge.

This requires architectural discipline from day 1.

**Framework vs workspace split.** Every directory in the repo contains framework files only. All operator-generated content lives in a dedicated root-level `/workspace/` directory that mirrors the framework structure underneath. Framework files are overwritable on upgrade. Workspace files are never touched.

**Upgrade command.** A simple operator-facing command (`alg upgrade`, runnable as a shell script or as a Claude skill) pulls the latest canonical release, overwrites framework files, leaves `/workspace/` untouched. Non-technical operators run one command. No git knowledge required.

**Versioning discipline.** Tagged semver releases. Minor versions for skill improvements and taxonomy additions (the common case). Major versions only when foundation file shape changes, which should be rare. CHANGELOG.md per release lists framework changes, capability taxonomy changes, and any required operator actions (the last category should usually be empty).

**Capability sync integration.** Mode 2 of capability sync (section 10.2) surfaces version deltas alongside platform deltas. "Your fork is at v1.0, latest is v1.2. Two changes matter for your config: here's what they unlock, run `alg upgrade` to pick them up."

The cost of this discipline is real. Every skill, template, and config in the repo has to honour the split. There is no mixing of framework and workspace files inside the same directory. The first-run intake bootstraps `/workspace/` from framework templates. Skills read from both (`/03-execution/<skill>` for logic, `/workspace/foundation/` for operator content) and write outputs to `/workspace/execution/`.

The cost of not doing it is bigger: a framework that locks every operator to the version they forked, with capability sync surfacing improvements they cannot use.

---

## 11. Repo Structure

The repo splits cleanly into framework and workspace. Framework directories ship with the canonical repo and are overwritten on upgrade. The workspace directory is created on first run and is never touched by upgrades.

```
/alg-os
  README.md                  what ALG is, how to run it
  CHANGELOG.md               versioned record of changes
  alg-upgrade                upgrade command (script or Claude skill)

  framework (overwritten on upgrade)
  /00-intake                 structured questionnaire and sparring prompts
  /01-foundation             brand, ICP, positioning, personas templates
                             includes voice.md template (English variant defaults + voice rules)
  /02-research               MCP config, data source schemas, intel templates
                             agent-taxonomy.md (the catalogue the recommender reads from)
  /03-execution              the four canonical skills
    /artefact                signature artefact generator
    /teardown                competitor and positioning analysis
    /proposal                post-discovery client document
    /nurture                 post-proposal email sequence
  /04-feedback               metrics, cadence, review templates
  /capability-sync           Anthropic, MCP, internal changelog reader
  /templates                 shared assets (PPT, email, doc templates)

  workspace (operator data, never overwritten)
  /workspace
    /foundation              operator's actual brand, ICP, positioning, voice.md
    /research                operator's research outputs, scraped content, MCP intel
    /execution               operator's generated artefacts, proposals, handoffs, nurture sequences
    /feedback                operator's feedback logs and review outputs
    /case-studies            operator's own proof points
```

GitHub workflow:

`main` is canonical. Edits go via branch + PR. Reviewer approves before merge. Issues capture "this skill produced weak output on X." Tagged semver releases. CHANGELOG.md is updated manually on each merge.

GitHub Actions automation (CI runs that execute Claude on PRs to validate skills, check banned words, diff outputs) is v2. Requires API credits at ~£20 to £50 per month. Skipped in v1. Manual review and Issues do enough for the first 90 days.

Each operator who runs ALG forks the repo. The first-run intake bootstraps `/workspace/` from framework templates. Subsequent upgrades pull canonical framework changes via `alg-upgrade`, leaving the operator's workspace untouched. The canonical repo never holds operator data.

---

## 12. The 90-Day MVP

Three builds, sequenced. Each has a 5-point validation rubric. All 5 must pass before moving to the next build.

### 12.1 Build 1 (Days 1 to 30) - The Sparring Layer

Build the `/00-intake` directory first. The diagnostic. The questionnaire. The refusal prompts. The quality bar logic.

This is the hardest part of the whole system and the one piece that travels universally across verticals. Building it first is counter-intuitive (the instinct is to start with a concrete skill) but correct. Skills built before the sparring layer end up back-fitted to assumptions the intake hasn't validated.

**Build 1 validation rubric:**

1. Intake completes self-serve. No synchronous 1:1 support required at any point.
2. Foundation files produced are vertical-specific (no generic template language).
3. Sparring layer rejects weak inputs (proves it is actively gate-keeping, not rubber-stamping).
4. Foundation files are internally coherent (no contradictions between persona, ICP, positioning, voice).
5. Operator can articulate their GTM motion shape in one paragraph after intake completes, and the foundation is defensible enough to run Build 2 skills against without Layer 1 rework.

If 5 of 5 pass, Build 2 begins. If fewer, see section 14.

### 12.2 Build 2 (Days 31 to 60) - The Five Execution Skills

Build the four canonical skills as universal templates. Artefact, Teardown, Proposal, Nurture.

Each skill reads from Layer 1 (the foundation produced by Build 1). Each skill is vertical-agnostic in its template, vertical-specific in its output.

The Artefact skill is the most demanding. It must produce a defensible artefact spec for any business that survives the intake.

**Build 2 validation rubric:**

1. Artefact skill produces a defensible signature artefact spec for any business that clears Build 1 (specific data sources, named target entities, production cadence, distribution plan).
2. Teardown produces actionable competitor analysis (specific positioning gaps, not summary).
3. Outputs require less than 30% editing to be usable in production.
4. Each skill enforces voice rules (English variant, banned words, paragraph length) without operator manual checking.
5. Skills produce vertical-specific output, not template language with the company name swapped in.

### 12.3 Build 3 (Days 61 to 90) - Build My Agents (the meta-agent)

**Note: this section was reframed during Build 2 v0.2 testing. Earlier draft scoped Build 3 as "tool-agnostic mode selector + recommendation engine + self-serve readiness." That scope is now subsumed inside the meta-agent below. The reframed scope is described here; the detailed implementation spec lands in a separate Build 3 spec doc when Build 3 work begins.**

Build a meta-agent that constructs the operator's running agent stack. The operator gives ALG OS three things (foundation, signature artefact spec, capability snapshot) and the meta-agent produces working agent definitions, MCP connections, and scheduled triggers so the operator's motion runs autonomously rather than requiring manual skill invocation.

The meta-agent reads:

1. The operator's foundation files in `/workspace/foundation/`.
2. The signature artefact spec in `/workspace/execution/artefact/<slug>-spec.md`.
3. The capability snapshot in `/workspace/research/capability-snapshot.md`.
4. The agent taxonomy in `/02-research/agent-taxonomy.md`.

The meta-agent produces:

- Working agent definitions in `/workspace/agents/` that execute the four canonical skills on triggers (proposal sent and no reply, mystery shop quarter rolling over, new prospect added to pipeline, etc.).
- MCP connection blueprints the operator approves and connects.
- Scheduled triggers (cron-like) for production cycles (artefact edition production, capability sync mode 2, etc.).
- A handoff to the operator: "your motion now runs. Review outputs in /workspace/execution/ before sending."

Mode selection (product-recursive vs tool-agnostic) and tool recommendations are now first-pass decisions inside the meta-agent's planning step rather than separate skills.

**Build 3 validation rubric (placeholder pending the dedicated spec):**

1. Meta-agent ingests the three input sources and produces a working agent stack definition.
2. Mode selection (product-recursive vs tool-agnostic) is decided and documented inside the agent stack.
3. The agent stack is self-serve end to end: an operator can run it without synchronous human support.
4. Documentation covers the full operator path (fork to running motion).
5. No critical bugs in the canonical flow (intake to running motion) when run against a fresh fork.

Capability sync evolution beyond v1 (scheduled background pulls, automated taxonomy updates), GitHub Actions automation, multi-tenancy SaaS, and public marketing release all stay out of scope until after day 90.

---

## 13. Validation and Metrics

ALG OS is validated by adoption and output quality, not by any one operator's pipeline result.

The metrics that matter for ALG OS as a product:

Foundation quality on first pass (does the operator run Build 2 skills against Layer 1 without needing to rewrite it).

Self-serve completion rate (do operators finish the intake without any synchronous human support from the framework maintainers).

Output quality across verticals (do the skills produce usable artefacts for businesses ALG was never specifically designed for).

Operator retention (do operators who run ALG come back and run it again 30, 60, 90 days later).

Number of operators running ALG (top of funnel for the framework itself).

Quality of artefacts produced (do the artefacts the operators ship actually drive inbound, and is this attributable).

Individual operators running ALG will measure their own GTM outcomes inside their own systems. ALG OS doesn't aggregate that data. It's not a SaaS analytics product. It's a framework.

**Failure logic.** When a build phase fails its validation rubric, diagnose the cause first.

Scope failure: the build attempted too much surface area at once. Refactor scope, cut what isn't load-bearing, retry.

Use case failure: the framework is producing weak output regardless of scope. The thesis is wrong for that operator's business type. Goodbye to that operator, retry with a different one.

Don't conflate the two. Scope failures look like "the intake required synchronous support to complete." Use case failures look like "the intake produced incoherent foundation files even when given good inputs." Different problems, different responses.

---

## 14. The 12-Month Sequence

Months 1 to 3: 90-day MVP as specified in section 12. The sparring layer, the five skills, and the tool-agnostic layer all work and clear their validation rubrics.

Months 4 to 6: usage in the wild. Watch how operators actually use the framework. Document failure modes. Iterate the intake aggressively. How operators are sourced (network, public release, paid pilots) is a go-to-market question outside the scope of this document.

Months 7 to 9: productise. Self-serve tier (the repo, the intake, the sparring layer, the templated skills) goes public. Documentation, examples, getting-started guide.

Months 10 to 12: depending on adoption, decide whether to build a hosted multi-tenant version (v3 question) or stay as an open-source framework with paid done-with-you support.

---

## 15. Open Questions and Decisions to Revisit

### 15.1 Done-With-You Revenue

Operators will ask "can you just run this for me." That's a £25k to £50k done-with-you offer. Taking it turns ALG into a service business by stealth. Refusing it leaves money on the table.

Decision required by month 6, before public release. Worth having a view on whether ALG is monetised as a framework, a service, or both.

### 15.2 GitHub Actions Automation

v2 feature. Adds CI runs on PRs that execute Claude to validate skills, check banned words, diff outputs against expected. Requires API credits at ~£20 to £50 per month at expected volume. Revisit at month 4 when the manual review burden has been felt for 90 days.

### 15.3 Multi-Tenant Architecture

v1 ships with "one repo per operator, fork it" pattern. Hosted multi-tenant SaaS is a v3 question. Revisit at month 9 based on adoption.

### 15.4 Open Source vs Commercial

ALG OS could be MIT-licensed and freely forkable, or it could be a paid framework with a commercial licence. Decision required by month 6. The trade-off is reach (open source wins) vs revenue (commercial wins).

---

## 16. Known Traps

The temptation to ship more than four canonical skills. Operators extend with their own, but the canonical floor stays at four. Every additional canonical skill defends its place against the cut-90% discipline.

The temptation to over-engineer the sparring layer. The intake refuses weak inputs but every question must be load-bearing. A 200-question intake is fine if every question moves the foundation. A 30-question intake is bad if half of them are bureaucratic. Quality bar, not gate-keeping for its own sake.

The temptation to skip building the universal version and just ship one operator's instance. The whole point of ALG OS is to work across operators. If it only works for the operator who built it, it's a personal toolkit, not a product.

The temptation to let the framework grow more complex than the outreach machines it produces. The sparring intake, the four canonical skills, the agent taxonomy, and the meta-agent (Build 3) are the whole product surface for v1. Anything else justifies itself or gets cut.

The temptation to recommend specific vendors (including any company Alexandru is associated with) inside the public ALG. Recommendations are tier-based and show multiple options. ALG isn't a kingmaker.

The temptation to confuse scope failure with use case failure when a build phase doesn't validate. Different diagnoses, different responses. Section 13 covers this.

---

## 17. What Claude Code Should Do First

1. Read this document end to end before writing any code or creating any file.

2. Set up the repo structure in section 11. Honour the framework vs workspace split from day 1: framework directories at the root, all operator-generated content paths under `/workspace/`. Create empty placeholder files where templates will go. The `/workspace/` directory is created at first-run intake, not in the canonical repo. Commit.

3. Write the README.md from sections 1, 2, 4, 6, and 12 of this document.

4. Write the initial CHANGELOG.md entry: "v0.3 - Foundation document established."

5. Build the `/00-intake` directory first. The sparring layer is the moat. It's the hardest part. Build it before the skills, not after.

6. Build the `/02-research/agent-taxonomy.md` second. This is what the recommendation engine reads from in Build 3, and getting the structure right early saves rework.

7. Build the `/03-execution/artefact` skill third (the Signature Artefact Generator). This is the most demanding skill and the one that proves the framework works across verticals.

8. The remaining three canonical skills (Teardown, Proposal, Nurture) come after the Artefact skill in Build 2.

9. Stop and check in with Alexandru after each of the three Build phases (day 30, day 60, day 90). Don't ship Build 2 features before Build 1 is validated against the rubric in section 12.1.

10. Treat every section of this document as a constraint, not a suggestion. If a build decision conflicts with this document, raise it before proceeding.

---

## 18. Brand and Voice Standards for ALG OS Outputs

Default voice: British English. No em dashes. No other dashes besides "-". Three sentences per paragraph maximum. Digits not words for numbers. Operator tone, not marketing tone. State things directly. No "that's not X, that's Y" reframing.

The intake asks the operator at the start: British or American English. The operator's selection is written to `/01-foundation/voice.md`. All skills read this file before generating output.

Operators can override other voice rules in `voice.md` if their brand calls for a different style. The defaults are the defaults because they tend to produce sharper output across most B2B contexts, not because they're sacred.

These rules apply to all ALG OS framework documentation (this document, READMEs, CHANGELOGs). They apply to skill output by default unless the operator's `voice.md` overrides them.

---

**End of foundation document.**
