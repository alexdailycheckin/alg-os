# Nurture Skill - Post-Proposal Email Sequence

This file runs when the operator says "nurture sequence," "post-proposal emails," "follow-up sequence," "reactivate this prospect," or any equivalent.

The skill produces a 5 to 7 email sequence over 30 to 60 days for a prospect who has gone quiet after a proposal. The sequence diagnoses the stall reason and addresses it directly.

Read in full before doing anything else.

## What this skill produces

A complete sequence at `/workspace/execution/nurture/<prospect-slug>-nurture-sequence.md` that includes:

- Stall diagnosis (BUYIN, PROOF, INFRASTRUCTURE, TIMING, or operator-named).
- The full sequence (5 to 7 emails) with subject lines, send dates, and full body copy.
- Send schedule (when to send each, with conditional logic).
- Voice rules applied throughout.

Length per email: 60 to 90 words by default (per typical operator voice rules). Override if the operator's `voice.md` says otherwise.

## Inputs the skill reads

| File | Why |
|---|---|
| `/workspace/foundation/voice.md` | All output uses the operator's voice. Email length budget often lives here. |
| `/workspace/foundation/services.md` | Services and tiers the sequence references. |
| `/workspace/foundation/positioning.md` | The win axis the sequence leans on. |
| `/workspace/foundation/personas.md` | Who is being emailed. Their objections. What unblocks them. |
| `/workspace/foundation/gtm-motion.md` | The funnel context. The proposal sold step 3 or 4; the nurture re-engages around that step. |

If foundation files are missing, refuse to run.

## Operator inputs

Ask:

1. **The prospect.** Company name, named decision-maker, named champion if different.
2. **The proposal context.** A reference to the proposal that was sent (`@path/to/proposal.md`), or a summary of what was proposed and at what price.
3. **When they went quiet.** Date of last contact. The send schedule depends on this.
4. **The stall reason if known.** Operator may already know why the prospect stalled. If so, name it. If not, the skill diagnoses.

## The four stall reasons

Most post-proposal stalls are one of:

| Stall | Description | Typical signal |
|---|---|---|
| **BUYIN** | The decision-maker needs internal alignment. Buying committee resistance. CFO, board, or peer pushed back. | Champion says "I need to get sign-off." Or silence after a discovery call where multiple stakeholders attended. |
| **PROOF** | They want more reference points. Case studies, benchmarks, peer validation. | "Can you share more case studies?" Or silence after the proposal but engagement on follow-up content. |
| **INFRASTRUCTURE** | Internal blocker on legal, IT, security, compliance, procurement. | "Our IT team is reviewing." "We need to run this past legal." |
| **TIMING** | Wrong moment. Budget cycle, leadership change, M&A activity, distraction. | "We are slammed with X right now, can we revisit in Q2?" Or silence with no clear hostility. |

If the operator names the stall, use it. If not, infer from the context they gave.

## Flow

### Phase 1 - Diagnose the stall

If the operator named the stall, confirm. If not, ask 1 to 2 clarifying questions to narrow it down. Do not produce a sequence without a diagnosis. Generic "just checking in" sequences are banned.

### Phase 2 - Map the stall to a sequence shape

Each stall has a sequence pattern. Adjust based on the operator's context.

**BUYIN sequence (5 emails over 30 days):**
- Email 1, day 0: Light, references the conversation. Offers help equipping the champion to sell internally (one-pager, FAQ, ROI calculator).
- Email 2, day 5: A peer-company case study with similar buying-committee dynamics, framed as "this is how <peer> got internal alignment."
- Email 3, day 12: Direct ask. "What is the biggest internal pushback so far. I can answer it directly so you do not have to carry it alone."
- Email 4, day 21: New external truth. A signature artefact edition or a piece of the operator's own data the champion can forward internally.
- Email 5, day 30: Decision close. "Worth a 15-minute call with <decision-maker> to address objections directly?" Or quiet exit if no engagement on emails 1 to 4.

**PROOF sequence (6 emails over 45 days):**
- Email 1, day 0: Light, references the conversation. Promises specific proof points coming.
- Email 2, day 5: First case study, named, with quantified outcome that maps to the prospect's named pain.
- Email 3, day 14: Second case study, different vertical or size, demonstrating breadth.
- Email 4, day 21: A piece of the operator's own data (mystery shop, benchmark, signature artefact edition) with the prospect's segment included.
- Email 5, day 30: Reference call offer. "Want to speak directly with <named customer> who solved <named pain>?"
- Email 6, day 45: Decision close.

**INFRASTRUCTURE sequence (5 emails over 60 days):**
- Email 1, day 0: Acknowledge the review process. Offer documentation proactively (security, GDPR posture, integration overview).
- Email 2, day 14: Direct ask. "What specifically does <IT/legal/procurement> need to clear this. I can answer or provide directly."
- Email 3, day 28: Status check. "Where are we in the review."
- Email 4, day 42: Re-anchor against the original trigger. Remind the decision-maker why this purchase started. The longer reviews go, the easier it is for the original urgency to fade.
- Email 5, day 60: Decision close.

**TIMING sequence (5 emails over 60 to 90 days):**
- Email 1, day 0: Acknowledge the timing. Light. No pressure.
- Email 2, day 14: External truth. A piece of news or data relevant to the prospect's market that suggests waiting has cost.
- Email 3, day 30: A signature artefact edition with the prospect's segment included.
- Email 4, day 45: Direct re-engagement. "Worth a 20-minute call to revisit, or is timing still wrong."
- Email 5, day 60 to 90: Decision close. Or quiet exit if no signal.

### Phase 3 - Write the sequence

Use the template below. Apply voice rules. Each email:

- 60 to 90 words by default (override per `voice.md`).
- One specific point per email. No "checking in" emails.
- Subject line under 40 characters.
- No banned words from the operator's voice.md.
- No "I hope this finds you well." No "just wanted to circle back." No marketing softeners.

### Phase 4 - Quality checklist

Run the checklist below. Fix failures before writing to `/workspace/execution/nurture/`.

## Output template

```
# Nurture Sequence - <Prospect Company Name>

**Prospect:** <Company>
**Decision-maker:** <Name, role>
**Champion:** <Name, role, if different>
**Last contact:** <Date>
**Stall diagnosis:** <BUYIN | PROOF | INFRASTRUCTURE | TIMING | <operator-named>>
**Sequence length:** <X emails over Y days>
**Voice variant:** <British | American per voice.md>

## Stall diagnosis rationale

<2 to 3 sentences. Why this stall. What signals point to it. What this sequence addresses.>

## Send schedule

| Email | Send date | Subject | Purpose |
|---|---|---|---|
| 1 | <Day 0, e.g. <YYYY-MM-DD>> | <Subject> | <One-line purpose> |
| 2 | <Day 5> | <Subject> | <Purpose> |
| ... | ... | ... | ... |

## Email 1 - <Send date>

**Subject:** <Subject line, under 40 chars>

**To:** <Decision-maker or champion, named>

**Body:**

<Email body copy. 60 to 90 words. One specific point. Voice rules applied.>

---

## Email 2 - <Send date>

**Subject:** <Subject>

**To:** <Recipient>

**Body:**

<Email body>

---

<Repeat for each email in the sequence>

## Conditional logic

| If prospect | Then |
|---|---|
| Replies to any email with a clear next step | Stop the sequence. Switch to direct conversation. |
| Replies asking for more time | Pause for the requested duration. Resume one week before. |
| Replies declining | Stop. Send a graceful close. Mark CRM. |
| Engages (open, click, reply) but no clear next step | Continue the sequence as scheduled. |
| Stays silent through the full sequence | Final email is a quiet exit. Mark CRM. Note in operator's `/workspace/feedback/` log for future re-engagement consideration. |

## Notes for the operator

<Any flags. E.g. "The 'Direct ask' email in this sequence is more direct than your default voice; flag if you want to soften." Or "Email 4 references your Q2 signature artefact edition; confirm publication date matches send date.">
```

## Quality checklist

Seven items. Three failures kill the sequence.

1. **Stall diagnosis is named.** Not "general follow-up." One of BUYIN / PROOF / INFRASTRUCTURE / TIMING / operator-named.
2. **Voice rules followed.** No banned words. Word count per email respects the operator's email-length rules.
3. **Each email has one specific point.** No "checking in" emails. Each one moves the conversation by addressing a specific element of the diagnosis.
4. **No marketing softeners.** No "I hope this finds you well." No "just wanted to circle back." No "as we discussed" if it was a single conversation.
5. **Subject lines under 40 characters.** Optimised for inbox preview.
6. **Send schedule is specific dates.** "Day 5" alone is not enough. Map to actual dates based on the operator's "last contact" input.
7. **Final email has a quiet-exit option.** No sequence ends with another "checking in" email if the prospect has not engaged.

If 3 or more fail, do not write to `/workspace/execution/nurture/`. Surface and fix.

## Hard rules

- Apply voice rules from `voice.md` to every email.
- Never invent prospect details. Source from the operator's input.
- Never produce a sequence without a stall diagnosis.
- Never send the sequence directly. The operator reviews and sends. The skill produces the artefact only.
- Quiet exit is mandatory. If a prospect does not engage, the operator stops chasing.

## Hand-off

After writing:

> "Sequence saved to `/workspace/execution/nurture/<slug>-nurture-sequence.md`. Review the email copy and adjust to your voice if needed. The conditional logic table at the bottom tells you when to pause, stop, or continue based on prospect response. If the prospect re-engages and the deal moves forward, run 'write the handoff' once they sign."

Do not auto-run other skills.
