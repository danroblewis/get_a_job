# Phase 5 — Operations Playbook

## OPERATIONS_AGENT

**Phase:** 5 (Serial — runs after all Phase 4 agents complete)
**Input:** `chosen_job.json` + `intake_form.json` + `technical_setup.md` + `gtm_plan.md` + `content_plan.md`
**Output:** `final_operations_playbook.md`
**Gate condition:** Playbook exists and Day 1 task is specific and executable right now

---

## Agent Role & Prompt

```
You are OPERATIONS_AGENT. You receive the full suite of Phase 4 outputs:
technical_setup.md, gtm_plan.md, content_plan.md, chosen_job.json, and intake_form.json.

Your job: synthesize these into a single weekly operating procedure the person can actually
follow. A procedure they could hand to their past self on Day 1 and have them succeed.

Rules:
1. Account for available hours. Take hours_per_week_max from intake_form.json.
   Subtract hours for delivery/build work. What's left is for everything else.
   If there's not enough time, CUT something — do not pretend it all fits.
2. Create zero ambiguity about what to do each day. Not "do outreach" but
   "send 3 LinkedIn DMs from the gtm_plan.md list, starting with [Name]."
3. Eliminate contradictions. If gtm_plan says 10 outreach messages/day but 
   content_plan says 2 hours/day of content, and total available hours don't support both,
   make a clear recommendation about which to prioritize and why.
4. The playbook is for the first 60 days, then re-evaluated. Not a permanent system.
5. The playbook must end with: "If you do nothing else today, do THIS: [one specific action]."

Output: final_operations_playbook.md
```

---

## Weekly Time Budget Design

The agent calculates the weekly time budget from `intake_form.json.capacity.hours_per_week_max`
and allocates it across work categories:

### Time Allocation by Job Type

**Freelance:**
| Category | Allocation | Description |
|----------|-----------|-------------|
| Client delivery | 40–60% | Actual project work once clients exist; 0% in Week 1 |
| Business development | 25–35% | Outreach, calls, proposals |
| Content | 15–20% | LinkedIn posts, community engagement |
| Admin | 5–10% | Invoicing, email management, tools |

**SaaS:**
| Category | Allocation | Description |
|----------|-----------|-------------|
| Product development | 50–60% | Building, fixing, improving |
| User acquisition | 20–30% | Outreach, content, community |
| User success | 10–15% | Onboarding, support, feedback interviews |
| Admin | 5% | Payments, infrastructure |

**Consulting:**
| Category | Allocation | Description |
|----------|-----------|-------------|
| Client work | 40–50% | Assessment, report writing, calls |
| Business development | 30–40% | Outreach, networking, thought leadership |
| Content | 15–20% | LinkedIn, newsletter |
| Admin | 5% | Proposals, invoicing |

**Content:**
| Category | Allocation | Description |
|----------|-----------|-------------|
| Content creation | 50–60% | Writing, recording, editing |
| Distribution | 15–20% | Posting, cross-posting, community |
| Audience building | 15–20% | Engagement, outreach to collaborators |
| Monetization | 10% | Sponsor outreach, product development |

---

## Daily Operating Procedure

The agent produces a specific daily schedule for the chosen job type. Example structure:

### Monday — Plan + Reach Out
- **Must complete:**
  - [ ] 15-min weekly review: review KPI dashboard, identify this week's #1 priority
  - [ ] Send 3 outreach messages from `gtm_plan.md` target list
  - [ ] Respond to any messages/emails from previous week
- **Nice to complete:**
  - [ ] Draft one content piece for the week
  - [ ] Update CRM/Notion with any new contacts
- **If I do nothing else:** Send the 3 outreach messages

### Tuesday — Deep Work
- **Must complete:**
  - [ ] 3–4 hours uninterrupted delivery or build work
- **Nice to complete:**
  - [ ] Finish content draft from Monday
- **If I do nothing else:** Do the delivery/build work

### Wednesday — Follow-ups + Proposals
- **Must complete:**
  - [ ] Follow up on any unanswered Monday outreach (if 48h have passed)
  - [ ] If a proposal is pending: finalize and send it
  - [ ] 1 hour community engagement (answer questions, give value)
- **Nice to complete:**
  - [ ] Schedule a discovery call if any leads responded
- **If I do nothing else:** Send the follow-ups

### Thursday — Deep Work
- **Must complete:**
  - [ ] 3–4 hours delivery or build work
- **If I do nothing else:** Do the work

### Friday — Ship + Wrap
- **Must complete:**
  - [ ] Publish one content piece (drafted earlier in the week)
  - [ ] Log KPIs in dashboard
  - [ ] 10-min prep for next week: write down Monday's 3 outreach targets
- **Nice to complete:**
  - [ ] Send 2 more outreach messages
  - [ ] Read one relevant piece of content in the target industry
- **If I do nothing else:** Log the KPIs and write Monday's list

---

## KPI Dashboard

Track these metrics weekly. Keep them in a simple table (Notion, Markdown file, or spreadsheet).

| Metric | Week 1 Target | Week 2 Target | Week 3 Target | Week 4 Target |
|--------|--------------|--------------|--------------|--------------|
| Outreach sent | 15 | 15 | 10 | 10 |
| Responses received | — | 2+ | 2+ | 2+ |
| Discovery calls | 0 | 1+ | 2+ | 2+ |
| Proposals sent | 0 | 1+ | 2+ | 1 |
| Revenue closed ($) | 0 | 0 | 1+ deal | — |
| Content published | 1 | 2 | 2 | 2 |
| Hours worked | X | X | X | X |

**Trigger reviews:**
- If revenue = 0 at Day 30: activate `10_contingency_matrix.md` Failure Mode 1 or 2
- If revenue exists but no growth at Day 60: activate Failure Mode 3 review
- If hours > hours_per_week_max for 2 consecutive weeks: activate scope reduction protocol

---

## Scope Reduction Protocol

If the person is doing too much, this is the priority order for what to cut first:

1. Cut content volume (halve the posting frequency)
2. Cut community engagement time (reduce to 30 min/week)
3. Cut admin to bare minimum (batch once a week)
4. Never cut: outreach (if pre-revenue) or delivery (if post-revenue)

The core loop must always survive: **talk to potential customers → close one → deliver → repeat.**
Everything else is supportive.

---

## The "First Dollar" Checklist

When the first payment arrives:

1. **Acknowledge receipt** (within 4 hours): "Got the payment — thank you. Starting [X] on [date]."
2. **Start delivery** per the proposal/agreement
3. **Log it:**
   - Amount
   - Source (which outreach message led to this)
   - Job type
   - Days from first outreach to payment
4. **Screenshot the transaction** — this is Proof Point #1
5. **Write one sentence** in your notes: "What specifically caused this sale to happen?"
   This is the seed of the GTM insight that will drive the next 10 sales.
6. **Tell someone** (partner, friend, community) — making it real helps make it repeatable

---

## Output Format — `final_operations_playbook.md`

```markdown
# Operations Playbook — [Job Title]

## The Job (one paragraph)
[What you do, for whom, at what price, why it matters]

## Who You Serve
[Customer profile — specific, not generic]

## How You Find Them
[Acquisition summary: primary channel, weekly outreach volume, weekly content output]

## What You Deliver
[Delivery summary: what the customer receives, how long it takes, what excellent looks like]

## This Week's Schedule
[Day-by-day, with must-complete and if-I-do-nothing-else for each day]

## Weekly Time Budget
| Category | Hours/Week | Activities |
|----------|-----------|-----------|
| ... | ... | ... |

## KPI Dashboard
[Table with weekly targets]

## The Minimum Viable Week
[What to do if everything goes sideways and you only have 5 hours this week]

## Review Triggers
[When to activate contingency, when to re-evaluate]

## If You Do Nothing Else Today:
[One specific action — named, detailed, executable in the next 60 minutes]
```

---

## Handoff Instructions

1. Save as `final_operations_playbook.md`
2. Print a closing statement to the human:
   > "Your job is built. Here's what you need to know:
   > 
   > **What you're doing:** [one sentence]
   > **First action today:** [specific action from Day 1 of gtm_plan.md]
   > **How you'll know it's working by Day 14:** [specific leading indicator]
   > **If something isn't working by Day 21:** [reference to contingency]
   >
   > Go."
3. Pass `final_operations_playbook.md` to `11_30_day_launch_plan.md` as execution reference
4. The flow is complete. The job is built. Now the person runs it.
