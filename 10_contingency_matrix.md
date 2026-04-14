# Contingency Matrix — Failure Modes & Recovery

## CONTINGENCY_AGENT

**Mode:** Passive (runs throughout all phases, activates on failure signals)
**Input:** KPI dashboard data + current phase artifacts
**Output:** Recovery plan + modified agent prompts
**Activation:** When KPI triggers are hit (see `09_operations_playbook.md`) or when the human flags a problem

---

## Overview

This document is not pessimism. It is what makes starting possible.

Knowing exactly what to do when something fails removes the paralysis of failure.
The person does not need to improvise when they've already planned for it.

There are five core failure modes. Each has:
- A **detection signal** (how you know it's happening)
- A **root cause checklist** (diagnose before acting)
- A **recovery action** with a modified agent prompt
- A **timeline** (how long to try the recovery before escalating)

---

## Failure Mode 1 — No Response to Outreach

### Detection Signal
20+ outreach messages sent across 14 days with fewer than 3 responses (responses include replies, "not interested," and "wrong time").

### Root Cause Checklist
Before doing anything, diagnose which of these is true:

- [ ] **Wrong audience**: Is the buyer persona too vague? Did you reach out to people who don't actually have this problem?
- [ ] **Wrong message**: Is the offer unclear, jargon-heavy, or talking about features instead of outcomes?
- [ ] **Wrong channel**: Are these people actually active on the platform you're using?
- [ ] **Wrong timing**: Is there a seasonal or market reason (post-layoffs, budget freeze, holidays)?
- [ ] **Wrong offer**: Is the price or scope not matching what this buyer actually buys?
- [ ] **Wrong credibility**: Are you asking for trust you haven't yet established?

### Recovery Action

**Step 1:** Run OUTREACH_AUDIT_AGENT with this prompt:

```
You are OUTREACH_AUDIT_AGENT. The person has sent [N] outreach messages and received [N] responses.
Read the message templates from gtm_plan.md and the 10 first buyers list.

Diagnose the most likely failure reason from this checklist:
[paste root cause checklist above]

Then:
1. Rewrite ONE outreach message for the top 5 remaining targets — hyper-personalized,
   specific to each person, referencing something real about them or their work.
2. Suggest one change to the channel or platform if the current one isn't working.
3. Propose a new "entry offer" that reduces friction: something free or very cheap
   that makes the first yes easier.

Do not produce generic advice. Produce 5 ready-to-send messages.
```

**Step 2:** Also run AUDIENCE_SHIFT_AGENT if root cause is "wrong audience":

```
You are AUDIENCE_SHIFT_AGENT. The outreach has not produced responses.
Read intake_form.json and chosen_job.json.

The current target buyer is: [target_customer from chosen_job.json]
This buyer has not responded. We need to find a different buyer for the same service.

Identify 2–3 adjacent buyer types who have the same underlying problem but are
easier to reach or more likely to respond quickly. For each:
- Who they are (job title, company type)
- Why they have the same problem
- Where to find them specifically
- What one sentence in the outreach message changes to speak to them
```

**Recovery Timeline:** 7 days. If still no responses after revised outreach, escalate to Failure Mode 3.

---

## Failure Mode 2 — Calls Happening But Can't Close

### Detection Signal
3+ discovery calls completed, 2+ proposals sent, 0 signed agreements in 21 days.

### Root Cause Checklist

- [ ] **Price objection**: Is the price higher than the buyer expected or budgeted?
- [ ] **Unclear value**: Did the proposal not clearly connect their pain to your solution?
- [ ] **Wrong decision-maker**: Are you talking to someone who is interested but can't sign?
- [ ] **Trust gap**: Do they like you but not trust you enough to hand over money yet?
- [ ] **Scope mismatch**: Is what you're offering too big/small for what they actually need?
- [ ] **Timing issue**: They want it, but not now?

### Recovery Action

**Step 1:** Run DEAL_AUTPOSY_AGENT after each lost deal:

```
You are DEAL_AUTOPSY_AGENT. A proposal was sent and not accepted.
Context: the proposal is at [describe or paste], the discovery call notes say [describe],
and the buyer's last message was: [paste].

Identify the most likely reason it didn't close.
Then produce:
1. One follow-up message that re-opens the conversation without being pushy.
2. A modified version of the proposal that addresses the likely objection.
3. If price was the issue: a restructured entry offer at 40–60% of the original price
   that still delivers clear value and leads naturally to the full engagement.
```

**Step 2:** Run PRICING_RESET_AGENT if price is the recurring objection:

```
You are PRICING_RESET_AGENT. The person has had [N] calls and [N] proposals but no signed clients.
Read their proposal from gtm_plan.md and their pricing card.

The buyers have not signed. Price friction appears to be a factor.

Design a "starter package" that:
- Costs under $500 (freelance/consulting) or is free for 14 days (SaaS)
- Can be delivered in under 8 hours of work
- Delivers one concrete, demonstrable result
- Contains a natural upsell to the core offering

Write the exact new entry offer, a one-paragraph pitch for it, and a 3-sentence
outreach message specifically for the 5 people who didn't close on the original proposal.
```

**Recovery Timeline:** 7 days. If no close after revised approach, consider Failure Mode 3.

---

## Failure Mode 3 — Wrong Job Type Selected

### Detection Signal
30 days in with no revenue AND the person reports low motivation, avoidance of the plan, or not executing the daily procedure.

Note: this is different from Failure Mode 1 or 2. Those are tactical problems.
This is a strategic problem. The person bet on the wrong option.

### Root Cause Checklist

- [ ] Was there a deal-breaker from intake that wasn't weighted heavily enough?
- [ ] Has something changed since intake (new constraints, new network opportunities)?
- [ ] Is the work itself energy-draining rather than energizing?
- [ ] Did the market reveal a reality that the scanners didn't capture?
- [ ] Was the intake data incomplete or optimistic?

### Recovery Action

**This is not failure. This is the most valuable data the first 30 days can produce.**

**Step 1:** Run RETROSPECTIVE_AGENT:

```
You are RETROSPECTIVE_AGENT. It has been 30 days. No revenue. Low motivation.

Read intake_form.json, chosen_job.json, and the KPI log.

Ask the person:
1. What part of this did you do consistently? What did you avoid?
2. What felt wrong from the beginning that you didn't say out loud?
3. If you had to earn $500 by Friday and could do anything, what would you do?

After hearing their answers, identify:
- The specific misalignment between chosen_job.json and their actual behavior
- What the third-question answer reveals about what they'll actually do

Produce a revised chosen_job.json based on this new information.
Do NOT re-run all phases. Run a compressed Phase 4 sprint: 2 days to produce
revised technical_setup, gtm_plan, and content_plan for the new direction.
```

**Step 2:** Run compressed Phase 4 (2-day sprint):
- Day 1: ARCHITECTURE_AGENT and GTM_AGENT in parallel (2 hours each)
- Day 2: CONTENT_AGENT + OPERATIONS_AGENT (2 hours each)
- Use the insights from retrospective to pre-fill all constraints

**Recovery Timeline:** 5 days to produce new plan, then reset Day 1.

---

## Failure Mode 4 — SaaS Stalls at Zero Paying Users

### Detection Signal
SaaS product is live, has 10+ free/trial users, but 0 paying users after 30 days of availability.

### Root Cause Checklist

- [ ] **Pricing page problem**: Is the value proposition unclear or the price unjustified?
- [ ] **Wrong audience signed up**: Are the free users the target buyer, or are they curious onlookers?
- [ ] **Feature missing**: Is there one thing blocking them from paying?
- [ ] **Upgrade prompt missing**: Do they even know there's a paid tier?
- [ ] **Trust gap**: Do they like the product but not trust the company (one-person SaaS)?
- [ ] **Value not realized**: Are users not getting to the "aha moment" before the trial ends?

### Recovery Action

**Step 1:** Run CONVERSION_AUDIT_AGENT:

```
You are CONVERSION_AUDIT_AGENT. A SaaS product has [N] free users but 0 paid conversions.

Context:
- Product: [description from chosen_job.json]
- Pricing: [pricing from chosen_job.json]
- Target user: [target_customer from chosen_job.json]
- What users do in the product: [describe the core action]

Identify the 3 most likely reasons a user would NOT upgrade, based on the product description
and common SaaS conversion failure patterns.

For each reason, produce:
1. A specific fix (copy change, UX change, or email addition)
2. The exact text/implementation of that fix
3. How to test if the fix worked (what metric changes)

Then produce 5 short personal emails the person can send to free users asking:
"You signed up for [product] but haven't upgraded. What would need to change for you to pay $X/month?"
These emails should feel like they're from a person, not a system.
```

**Step 2:** If no upgrades after 7 more days with fixes applied, consider a "founding user" offer:

```
Run FOUNDING_OFFER_AGENT:
"You are FOUNDING_OFFER_AGENT. Design a time-limited founding user offer for [SaaS name].
The offer: lifetime deal or discounted annual plan for the first 10 paying users.
Produce the offer terms, the announcement post, and personal outreach messages
to the 10 most active free users."
```

**Recovery Timeline:** 14 days. If still 0 after founding offer, escalate to Failure Mode 3.

---

## Failure Mode 5 — Burnout / Execution Breakdown

### Detection Signal
Two or more of:
- Person stops logging KPIs for 5+ days
- Person misses a full week of outreach
- Person reports feeling overwhelmed, paralyzed, or like they want to quit

### Root Cause Checklist

- [ ] **Overwhelm**: too many tasks, unclear priority
- [ ] **Wrong job type**: the work itself is draining (see Failure Mode 3)
- [ ] **Personal circumstances**: external factors making the plan infeasible
- [ ] **Isolation**: working alone without feedback is demoralizing
- [ ] **No progress visible**: KPIs are flat and the person can't see evidence of movement

### Recovery Action

**This is the most human failure mode. Do not treat it mechanically.**

**Step 1:** Scope reduction protocol. Immediately:
- Cut content production to ZERO for 2 weeks
- Cut all "nice to complete" tasks
- Reduce the plan to ONE action per day

**The minimum viable daily action** (choose the one that fits the job type):
- Freelance: "Send one personalized message to one person today."
- SaaS: "Merge one small improvement today."
- Consulting: "Email one person who knows you and ask if they know anyone who needs X."
- Content: Skip entirely for 2 weeks.

**Step 2:** Run SCOPE_REDUCTION_AGENT:

```
You are SCOPE_REDUCTION_AGENT. The person is burned out.
Read final_operations_playbook.md and intake_form.json.

Re-run OPERATIONS_AGENT with hours_per_week_max reduced by 50%.
Produce a "minimum viable operations" version of the playbook:
one must-do action per day, nothing else.
The goal for the next 2 weeks is not revenue — it is staying in the game.
```

**Step 3:** Check community engagement. Is the person connected to even one other person
doing similar work? If not, recommend joining one relevant community for peer support.
Working alone is a risk factor, not just a workflow issue.

**Recovery Timeline:** No deadline. The person needs to rest, not be pressured.
After 2 weeks on minimum viable operations, re-evaluate with full intake re-run if needed.

---

## The Nuclear Option (Day 60, No Revenue)

If after 60 days the person has zero revenue from any source:

1. **Pause the current plan** — do not keep executing something that isn't working
2. **Run EMERGENCY_INTAKE_AGENT:**

```
You are EMERGENCY_INTAKE_AGENT. It has been 60 days and no revenue has been earned.
Read the original intake_form.json and the current KPI log.

Ask the person:
1. What has changed since the original intake? (New constraints, new opportunities, new self-knowledge)
2. What is your financial situation NOW vs. Day 0?
3. What would you do if you had to earn $200 by next Friday — what specifically?

Based on their answers, identify ONE income-generating action with the following properties:
- Executable within 48 hours
- Requires no new infrastructure (no new tools, no new accounts)
- Uses only existing skills and relationships
- Has a realistic path to $200–$500 within 7 days

This is NOT the final job. This is the bridge job. Bridge first, then re-plan.
```

3. **Execute the bridge job** until there is at least one payment
4. **Then** re-run the full orchestration from Phase 3 with the new self-knowledge

The bridge job might be as simple as: "Offer to help one person with one Claude Code task for $200."
That first dollar changes everything.
