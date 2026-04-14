# Phase 4B — Go-to-Market (Parallel)

## GTM_AGENT

**Phase:** 4 (Parallel — runs simultaneously with ARCHITECTURE_AGENT and CONTENT_AGENT)
**Input:** `chosen_job.json` + `intake_form.json` + `persona_profile.json`
**Output:** `gtm_plan.md`
**Consumed by:** OPERATIONS_AGENT (Phase 5), `11_30_day_launch_plan.md` (execution)

---

## Agent Role & Prompt

```
You are GTM_AGENT. You receive chosen_job.json, intake_form.json, and persona_profile.json.

Your job: produce a first-revenue plan. "First revenue" means real money received from a
real customer. Not a conversation. Not a proposal sent. Money received.

Rules:
1. Work with what exists. Use the warm leads and communities from intake_form.json first.
   Cold outreach to strangers is a last resort, not a first move.
2. Do not build funnels. Do not optimize. Get the first deal closed.
3. Every template you produce must be ready to send — not a template with [INSERT VALUE PROP].
   Fill in the blanks using persona_profile.json and chosen_job.json.
4. Be honest about price. Do not race to the bottom. Do not propose "do it for free to build
   portfolio" unless financial runway is critically short and there is no alternative.
5. The goal is to close within 14 days, not to build a sustainable sales system.
   The system comes after the first revenue.

Produce ALL sections below. Output: gtm_plan.md
```

---

## Section 1: The 10 First Likely Buyers

Using `intake_form.json.network.warm_leads` and community data, identify the 10 most likely
first buyers. For each, the agent produces:

```markdown
### Buyer 1: [Name or description from intake]
- Relationship: [how they know the person]
- Why they might buy: [specific reason connected to chosen_job.json]
- Outreach channel: [how to reach them — DM, email, call]
- Personalization hook: [what specifically to reference in the message]
- Outreach priority: HIGH / MEDIUM / LOW
```

If warm_leads has fewer than 10 people, fill the remainder with researched targets from
communities listed in intake_form.json — specific usernames or roles, not "people on Reddit."

---

## Section 2: Outreach Message Templates (Ready to Send)

One template per channel. All templates are filled in using persona data — no brackets.

### LinkedIn DM (connection request + follow-up sequence)

**Connection request (300 char max):**
```
Hi [Name] — I saw your post about [relevant topic]. I'm [one-line bio from persona_profile.json].
Connecting because [specific reason related to their work and chosen_job.json offering].
```

**Follow-up DM (3 days after connection):**
```
[Name] — thanks for connecting. I'm currently working with [buyer persona description] on
[core deliverable from chosen_job.json]. Wondering if you're dealing with [specific pain point].

If so, I'd love to hear about your situation — no pitch, just curious. Worth a 15-min call?
```

**If they respond with interest:**
```
Great — here's my calendar: [Calendly link or "what's a good time this week?"]

Before we talk, can you tell me in 2–3 sentences: what's the biggest [relevant pain point]
you're dealing with right now? Helps me make the call more useful for you.
```

### Email (cold or warm)

**Subject options (test these):**
- `Question about [specific thing they're working on]`
- `[Mutual connection or shared context] → quick question`
- `[Company name] + Claude Code automation — 15 min?`

**Body:**
```
Hi [Name],

[Personalization sentence — what specifically prompted this outreach.]

I'm [one-line bio]. I [specific thing from chosen_job.json — what you do and for whom].

I've been talking to [buyer persona type] lately and hearing a lot about [pain point].
I built [related proof point from persona_profile.json] that [specific outcome].

Are you dealing with [pain point]? If yes, I'd love to hear about your situation.
15-minute call this week?

[Name]
[one-line bio]
[portfolio or relevant link if exists]
```

### Discord/Slack/Community DM

```
Hey [Name] — I've seen your posts about [topic] in [community name] and always found them useful.

I'm building [chosen_job.json one-sentence description] and I'm talking to people who deal with
[pain point] to make sure I'm solving the right problem.

Would you be open to a 20-minute conversation? No pitch — just want to understand your workflow.
```

### Twitter/X DM

```
[Name] — your thread on [topic] was great (especially the [specific part]).

Quick question: does [pain point] come up in your work? I'm [one-line bio] and I've been
working on something that might be relevant. Happy to share — no sell, just curious if it lands.
```

---

## Section 3: The Discovery Call Script

**Duration:** 20–30 minutes (keep it short)
**Goal:** Understand their situation and decide if there's a fit worth proposing

```
Open (2 min):
"Thanks for making time. I'll keep this focused — [X] minutes. I want to understand your
situation first. No pitch from me today. If it seems like I can help, I'll suggest a next step.
Sound good?"

Their situation (8 min):
"Tell me what's going on with [pain point area]. What are you doing now, and what's not working?"
→ Listen. Do not interrupt. Write down their exact words.

Pain depth (5 min):
"What does that cost you? Time? Money? Something else?"
"How long has this been a problem?"
"Have you tried to fix it? What happened?"

Fit check (5 min):
"Based on what you've described, I think I can [specific thing]. The way I work is [brief description].
Does that sound like what you need, or am I off base?"

Next step (5 min):
If yes: "I'll send you a proposal by [specific date — 2 business days]. It'll include the scope,
timeline, and price. We can adjust from there. Sound good?"

If no: "That's helpful. What would actually solve this for you?" 
→ Either pivot the offering or end the call professionally.
```

---

## Section 4: The Proposal Structure

Fill this in using `chosen_job.json` and call notes. Send within 48 hours of the call.

```markdown
# Proposal: [Project Name]
**Prepared for:** [Name], [Company]
**Date:** [Date]
**Valid until:** [Date + 7 days]

## What I understand you need
[2–3 sentences using their exact words from the call]

## What I will deliver
[Numbered list of specific deliverables — no vague descriptions]
1. [Deliverable with acceptance criteria]
2. ...

## What is NOT included
[2–3 explicit scope limits — protects both parties]

## Timeline
- Kickoff: [Date]
- First milestone: [Date + description]
- Final delivery: [Date]
- Note: timeline begins on receipt of [required inputs]

## Investment
**[Price]**
Payment: [X]% ($[amount]) due at signing. [X]% ($[amount]) due on final delivery.
Payment via: [Stripe link or bank transfer details]

## Why this will work
[1–2 sentences connecting their specific situation to your relevant experience]

## To proceed
Reply to this email with "I agree" or sign the attached [DocuSign/HelloSign link].
Questions? Let's schedule a 15-min call: [calendar link]
```

---

## Section 5: Pricing Architecture

Based on `chosen_job.json.pricing_model` and opportunity data:

### Entry Offer (low-friction first engagement)
- Purpose: Reduce buyer's risk. Let them experience the value before a bigger commitment.
- Target price: $150–$500 for freelance/consulting; $0 trial or $29 first month for SaaS
- What it includes: [one concrete deliverable, deliverable in ≤8 hours]
- What it leads to: naturally transitions to the core offering if the client sees value

### Core Offering (primary service)
- Price: from `chosen_job.json.pricing_model.core_price`
- What's included: full scope
- Positioning: not the cheapest, not the most expensive — best ROI for this specific buyer

### Premium Tier
- Price: from `chosen_job.json.pricing_model.premium_price`
- What's different: ongoing involvement, faster turnaround, or broader scope
- When to offer: after successful core engagement

### Pricing Conversation Rules
1. State the price confidently. Do not add "but we can negotiate."
2. If they push back on price: ask "What budget were you expecting?" before discounting.
3. If their budget is genuinely lower: offer the entry package, not a discounted core package.
4. Raise prices after 3 successful clients. Do not ask permission.
5. The first client is not worth $0. Even a discounted first engagement should exceed $200.

### Objection Responses

**"This is more than I expected"**
> "I understand. What were you expecting to invest? [Pause] Based on that, let me think about
> whether there's a way to structure this that works for both of us without compromising
> what you actually need."

**"Can you do it cheaper?"**
> "I could reduce the scope — let me tell you what I'd cut and you tell me if it still
> solves your problem."

**"We need to think about it"**
> "Of course. What specifically needs more thought? Sometimes I can answer it now
> and save you the back-and-forth."

**"We're not ready yet"**
> "When do you think you'll be ready? [Note the date] I'll follow up then — or if something
> changes earlier, feel free to reach out."

---

## Section 6: Platform-Specific Strategies

### Upwork / Toptal (if applicable)
- Profile optimization: headline must contain the exact phrase buyers search for
- First 5 proposals: personalized, specific, reference their exact job description
- Proposal structure: 3 sentences max — "I've done X similar to yours, here's proof, want to talk?"
- Starting rate: market rate, not below. Low rates attract bad clients.

### LinkedIn (for all job types)
- Optimize headline: "[What you do] for [specific buyer] | [result you deliver]"
- 3 posts in first week: 1 expertise post, 1 story post, 1 question post
- Connection strategy: connect to 5 targeted people per day with a short personal note
- DM timing: send DM 2–3 days after connection, not immediately

### Community Channels (Discord, Slack, Indie Hackers, Reddit)
- Week 1: give value first. Answer 3 questions where you can genuinely help. No pitch.
- Week 2: soft mention. "I'm building [X] for [Y]. Anyone dealing with [problem]?"
- Week 3: direct offer. "I'm offering [entry offer] to [N] people in this community this month."

---

## Output Format — `gtm_plan.md`

```markdown
# Go-to-Market Plan — [Job Title]

## The 10 First Buyers
[Table or list with name/description, channel, priority, personalization hook]

## Week 1 Outreach Schedule
Day 1: Send to buyers 1, 2, 3 via [channel]
Day 2: Follow up + send to buyers 4, 5
Day 3: Send to buyers 6, 7, 8
Day 4: Follow up Day 1 messages
Day 5: Send to buyers 9, 10

## Ready-to-Send Messages
[All templates filled in — not templates with brackets]

## Proposal Template
[Filled in for the chosen job type]

## Pricing Card
Entry: $[X] — [what's included]
Core: $[X] — [what's included]
Premium: $[X] — [what's included]

## Objection Responses
[All five objections with responses]
```

---

## Handoff Instructions

1. Save as `gtm_plan.md`
2. Print a one-paragraph summary: "You have [N] warm leads, [N] community targets. The first message you should send is to [specific person] via [channel] with this hook: [one sentence]."
3. Flag if warm_leads was empty — in that case, note that the first week is harder and community strategy is primary
4. Pass to OPERATIONS_AGENT (Phase 5)
