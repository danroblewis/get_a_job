# 30-Day Launch Plan

## How to Read This Document

This is the execution calendar. Everything else in this orchestration has been preparation.
This document is what you actually do.

**Reference documents:**
- `gtm_plan.md` for specific outreach targets and message templates
- `content_plan.md` for specific content pieces to produce
- `technical_setup.md` for setup checklists
- `final_operations_playbook.md` for the daily/weekly rhythm
- `10_contingency_matrix.md` if a checkpoint is missed

---

## Pre-Launch (Days -3 to 0) — Run the Orchestration

| Day | Action | Output |
|-----|--------|--------|
| Day -3 | Run INTAKE_AGENT. Answer all 28 questions honestly. | `intake_form.json` |
| Day -3 | Validate intake output. All fields non-null. | Validated `intake_form.json` |
| Day -2 | Launch all Phase 2 agents simultaneously: 5 scanners + PERSONA_BUILDER | 6 agents running in parallel |
| Day -2 | Review outputs as they complete. Flag anything that seems wrong. | 5 opportunity files + `persona_profile.json` |
| Day -1 | Run OPPORTUNITY_SCORER_AGENT once all Phase 2 outputs exist. | `opportunity_scores.json` |
| Day -1 | Run CONVERGENCE_GATE. Review top 3. Fill out decision matrix. Commit. | `chosen_job.json` |
| Day 0 | Launch Phase 4 agents simultaneously: ARCHITECTURE + GTM + CONTENT | 3 agents running in parallel |
| Day 0 | Review all three outputs. Accept or flag for revision. | `technical_setup.md`, `gtm_plan.md`, `content_plan.md` |
| Day 0 | Run OPERATIONS_AGENT. Review the playbook. | `final_operations_playbook.md` |

**Gate check before Day 1:**
- [ ] `chosen_job.json` exists and you believe it
- [ ] `final_operations_playbook.md` exists and Day 1 is clear
- [ ] You know who the first 3 outreach messages go to and what they say
- [ ] You have at least one tool set up from `technical_setup.md`

---

## Week 1 — Infrastructure and First Outreach (Days 1–7)

**Week goal:** All tools set up. 15 outreach messages sent. First content piece published.

### Day 1 — Go

**Must do:**
- [ ] Complete Day 1 checklist from `technical_setup.md` (account creation, tools, first file)
- [ ] Send first 3 personalized outreach messages from `gtm_plan.md`
  - Target: buyers 1, 2, 3 from the first buyers list
  - Channel: as specified in `gtm_plan.md`
  - Message: use the ready-to-send templates, not improvised versions
- [ ] Publish Sprint Piece 1 (if credibility_gap) OR first content piece from `content_plan.md`

**Log:**
- Outreach sent: ___
- Channel used: ___
- Content published: yes/no

### Day 2 — Follow-up + More Outreach

**Must do:**
- [ ] Send outreach messages to buyers 4 and 5
- [ ] Draft content piece 2 (publish on Day 5)

**Log:**
- Outreach sent: ___
- Total to date: ___

### Day 3 — Outreach + Community

**Must do:**
- [ ] Send outreach messages to buyers 6, 7, and 8
- [ ] Post one genuine answer to a question in a community from intake (no promotion — just help)

**Log:**
- Outreach sent: ___
- Community contribution: yes/no

### Day 4 — Follow-up Day

**Must do:**
- [ ] Follow up any Day 1 messages that haven't responded (48h follow-up is normal)
- [ ] Send outreach messages to buyers 9 and 10

**Log:**
- Follow-ups sent: ___
- Responses received to date: ___

### Day 5 — Ship Content + Reach Out Further

**Must do:**
- [ ] Publish content piece 2 from `content_plan.md`
- [ ] If communities have produced any leads, follow up directly

### Day 6 — Rest or Light Admin

- Optional: catch up on setup tasks from `technical_setup.md` Week 1 list
- Do NOT outreach on this day if it feels forced
- Do NOT produce content under pressure

### Day 7 — Week 1 Review

**Checkpoint:**

| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| Outreach messages sent | 15 | ___ | ✓/✗ |
| Responses received | 1+ | ___ | ✓/✗ |
| Content pieces published | 1–2 | ___ | ✓/✗ |
| Tools set up (Day 1 checklist) | Complete | ___ | ✓/✗ |

**Go/No-Go Decision:**

- **0 responses**: Activate `10_contingency_matrix.md` Failure Mode 1. Run OUTREACH_AUDIT_AGENT before Day 8.
- **1–2 responses**: On track. Continue to Week 2.
- **3+ responses**: Ahead of pace. Prioritize following up and booking calls.

---

## Week 2 — First Conversations and Proposals (Days 8–14)

**Week goal:** At least 1 discovery call. At least 1 proposal sent.

### Day 8 — Continue Outreach + Prep for Calls

**Must do:**
- [ ] Send 3 more outreach messages (next names from the extended target list)
- [ ] If any responses have come in: schedule discovery calls within this week
- [ ] Review `gtm_plan.md` discovery call script — read it out loud once

### Day 9 — Calls (if booked)

- [ ] Run any booked discovery calls using the call script from `gtm_plan.md`
- [ ] Take notes in the exact format: their words → their pain → their budget → next step
- [ ] If call went well: promise a proposal within 48 hours

### Day 10 — Proposals

**Must do:**
- [ ] If a call happened: draft the proposal using the template from `gtm_plan.md`
- [ ] If no call yet: send 3 more outreach messages; continue building the pipeline
- [ ] Publish content piece 3 from `content_plan.md`

### Day 11 — Proposal + Follow-up

- [ ] Send any drafted proposals
- [ ] Follow up on Week 1 outreach that hasn't responded (second touch — shorter, lighter)

### Day 12 — Community + Content Draft

- [ ] 30-min community engagement: give genuine value in one community
- [ ] Draft content piece 4

### Day 13 — Calls + Build Work

- [ ] If second calls are booked: run them
- [ ] Begin any build work that can be done before the first client signs
  (e.g., SaaS: core feature, Freelance: reusable component, Consulting: assessment template)

### Day 14 — Week 2 Review

**Checkpoint:**

| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| Outreach total (cumulative) | 25+ | ___ | ✓/✗ |
| Responses | 2+ | ___ | ✓/✗ |
| Discovery calls completed | 1+ | ___ | ✓/✗ |
| Proposals sent | 1+ | ___ | ✓/✗ |
| Content pieces published | 3–4 | ___ | ✓/✗ |

**Go/No-Go Decision:**

- **No calls and no proposals**: Activate `10_contingency_matrix.md` Failure Mode 1 or 2.
  Run OUTREACH_AUDIT_AGENT immediately.
- **Calls but no proposals**: Review call script. Was there a fit check moment? Did you ask for the next step?
- **Proposals sent**: On track. Focus Week 3 on closing.

---

## Week 3 — First Revenue Sprint (Days 15–21)

**Week goal:** First payment received.

### Day 15 — Follow Up on Proposals

**Must do:**
- [ ] Follow up any proposals sent more than 48 hours ago (if no response)
  Use the objection responses from `gtm_plan.md`
- [ ] Schedule a "check-in call" if the proposal has been out 5+ days without a decision

### Day 16 — Close or Continue Building

- [ ] If a proposal is being negotiated: focus here. Don't let it stall.
- [ ] Continue SaaS development or consulting template work
- [ ] Publish content piece 5

### Day 17 — First Delivery Begins (if closed)

If a deal closes:
- [ ] Send the onboarding message: "Got it — here's what happens next [timeline]"
- [ ] Collect first payment BEFORE starting work (per proposal payment terms)
- [ ] Start work only after payment confirmed

If no deal yet:
- [ ] Send 5 more outreach messages to new targets (expanding beyond initial 10)
- [ ] Consider running a "soft offer" in a community: "I have capacity for one more project this month"

### Day 18 — Delivery or Outreach

- [ ] If client: deep work on delivery
- [ ] If no client: run another round of targeted outreach to adjacent buyer types

### Day 19 — Mid-Week Review

Mini-check:
- Do I have a deal? If yes — deliver excellently.
- Do I have a pipeline conversation in progress? If yes — move it forward today.
- Am I stuck? If yes — run DEAL_AUTOPSY_AGENT from `10_contingency_matrix.md`.

### Day 20 — Invoice or Ship

- [ ] If work is done: send final deliverable + invoice
- [ ] If SaaS: soft-launch to first 10 target users for feedback
- [ ] Publish content piece 6

### Day 21 — Week 3 Review (CRITICAL GATE)

**Checkpoint:**

| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| Revenue received ($) | $1+ | ___ | ✓/✗ |
| Proposals sent (cumulative) | 2+ | ___ | ✓/✗ |
| Active pipeline conversations | 2+ | ___ | ✓/✗ |
| Content pieces published | 5–6 | ___ | ✓/✗ |

**Go/No-Go Decision:**

- **Revenue received**: The job exists. Move to Week 4 to systematize.
- **No revenue but active pipeline**: Close the pipeline. Do nothing else this week.
- **No revenue, no pipeline**: This is a critical signal. Activate `10_contingency_matrix.md`
  — specifically determine which failure mode applies and execute the recovery.

---

## Week 4 — Systematize and Compound (Days 22–30)

**Week goal:** Establish the repeatable loop. Understand what caused the first sale.

### Day 22 — Deliver Excellently

- [ ] If you have a client: deliver better than promised
- [ ] First delivery is the seed of every testimonial and referral that follows

### Day 23 — The Signature Case Study

**Must do:**
- [ ] Write the "Day 23 case study" — what happened in the last 3 weeks:
  - What you offered
  - Who bought it and why (from their perspective)
  - What you delivered
  - The outcome (even if preliminary)
  - What you'd do differently

  This becomes content piece 7 AND a proof point AND a sales tool.

### Day 24 — Re-activate Cold Leads

**Must do:**
- [ ] Send the case study (or a version of it) to the people who didn't respond in Week 1
  Now you have proof. The message is different: "When I reached out three weeks ago,
  I didn't have this to show you. Now I do."

### Day 25 — Pipeline Maintenance

- [ ] Follow up on any open proposals or conversations from earlier weeks
- [ ] Send outreach to 5 new targets
- [ ] Publish content piece 7 (the case study)

### Day 26 — Operations Review

**Must do:**
- [ ] Review `final_operations_playbook.md` with 26 days of real data
- [ ] Update the playbook where reality differed from plan:
  - What took longer than expected?
  - What was easier than expected?
  - What tool did you not use?
  - What channel worked best?

### Day 27 — Pricing Review

- [ ] Did the first sale close at the price you proposed? If you discounted, why?
- [ ] Is there evidence you could charge more? (Did they say yes immediately without negotiation?)
- [ ] Plan the pricing for the second client: same or higher?

### Day 28 — Community Contribution

- [ ] Post a "what I learned" update in one community where you've been active
  (Not a pitch. Genuine learning from the last 28 days.)
- [ ] This is how you become known in the community without promotion.

### Day 29 — Month 2 Plan

**Must do:**
- [ ] Write the Month 2 plan using the template below
- [ ] Identify the 3 changes to make to the operations playbook
- [ ] Identify the 10 new outreach targets for Month 2

### Day 30 — 30-Day Review

**Full review:**

| Metric | Day 7 | Day 14 | Day 21 | Day 30 |
|--------|-------|--------|--------|--------|
| Outreach sent | | | | |
| Responses | | | | |
| Calls | | | | |
| Proposals | | | | |
| Revenue ($) | | | | |
| Content pieces | | | | |

**Questions to answer in writing:**
1. What was the single most effective thing I did in Month 1?
2. What was the biggest waste of time?
3. What do I know now that I wish I'd known on Day 1?
4. What's the plan for Month 2?

---

## Month 2 Plan Template

(Fill in on Day 29 based on real data)

| Area | Month 1 Result | Month 2 Goal | How |
|------|---------------|--------------|-----|
| Revenue | $X | $X | [specific change] |
| Client count | N | N | [acquisition plan] |
| Content | N pieces | N pieces | [platform focus] |
| Outreach | N messages | N messages | [targeting change] |

**The one thing I'm changing in Month 2:**
[One sentence — the highest-leverage change based on what Month 1 taught you]

---

## Checkpoint Summary

| Day | Must-Have | Good-to-Have | Red Flag → Action |
|-----|-----------|--------------|-------------------|
| 7 | 15 outreach sent | 1+ response | 0 responses → FM1 |
| 14 | 1 call completed | 1 proposal sent | 0 calls → FM1/2 |
| 21 | $1+ revenue | $500+ revenue | 0 revenue → FM matrix |
| 30 | Repeatable routine defined | $1,000+ revenue | No Month 2 plan → FM3 |

FM = Failure Mode in `10_contingency_matrix.md`

---

## The Last Thing

The job is built. This document is its operating manual for the first 30 days.

The flow — intake, scanning, scoring, convergence, build, launch — was designed to get here.
Not to produce documents. To produce a person who knows what they're doing and why,
who has the tools and targets they need, and who knows what to do if it goes wrong.

Now close the browser and go send the first message.
