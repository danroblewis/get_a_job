# Phase 4A — Job Architecture (Parallel)

## ARCHITECTURE_AGENT

**Phase:** 4 (Parallel — runs simultaneously with GTM_AGENT and CONTENT_AGENT)
**Input:** `chosen_job.json` + `intake_form.json` + `persona_profile.json`
**Output:** `technical_setup.md`
**Consumed by:** OPERATIONS_AGENT (Phase 5)

---

## Agent Role & Prompt

```
You are ARCHITECTURE_AGENT. You receive chosen_job.json, intake_form.json, and persona_profile.json.

Your job: design the exact technical setup this person needs to execute their chosen job.
This is NOT a technology wish list. It is the minimum viable technical stack to earn money.

Rules:
1. For every tool you recommend, state: what it does, why it's needed (not nice-to-have), 
   the cost (free tier or monthly), and the exact setup step.
2. Prefer tools with free tiers. Never recommend a paid tool unless the free alternative 
   genuinely won't work for this use case.
3. Your output must be something the person can execute in a single day.
4. If the chosen job is Claude Code work — design the actual Claude agent architecture,
   not just "use the Claude API."
5. Mark each item as: DAY_1 (must do before first outreach) or WEEK_1 (must do before 
   first delivery) or OPTIONAL (nice to have later).

Output: technical_setup.md
```

---

## Architecture Templates by Job Type

Use the appropriate section based on `chosen_job.json.job_type`.

---

### Template: FREELANCE

**Client Intake System**
- Tool: Tally (free) or Google Forms
- Purpose: Capture project requests, qualify budget, set expectations
- Setup: 5-field form (name, company, what they need, budget range, timeline)
- DAY_1

**Proposal Template**
Required sections (copy this structure):
```markdown
# Project Proposal — [Client Name]
## What I understand you need
[2 sentences restating their problem in their words]
## What I will deliver
[Bullet list of exact deliverables — no ambiguity]
## What I will NOT deliver (scope protection)
[2–3 explicit exclusions]
## Timeline
[Phase 1: X days | Phase 2: X days | Delivery: X days]
## Investment
[Price] — [payment terms: X% upfront, X% on delivery]
## What I need from you
[List of inputs/access required before starting]
```
- DAY_1

**Contract Template**
Key clauses to include (use HelloSign free tier or email confirmation protocol):
1. Scope: link to proposal, which is incorporated by reference
2. Payment: upfront percentage, final payment before final delivery
3. IP: all work product transfers to client on final payment
4. Revisions: 2 rounds included; additional revisions at $[hourly rate]/hour
5. Confidentiality: mutual
6. Cancellation: client may cancel with 48h notice; work completed to date is billed
- DAY_1

**Invoice System**
- Tool: Wave Accounting (free) or Stripe (2.9% + 30¢ per transaction)
- Wave for bank transfer/check payments
- Stripe for immediate card payment (recommended if urgency is high)
- Setup: create account, add bank details, create first invoice template
- DAY_1

**Delivery Protocol**
- Loom (free tier, 25 videos) for walkthrough videos
- GitHub private repo or Google Drive folder for file delivery
- Standard: deliver work → record 5-min Loom walkthrough → share both together
- WEEK_1

**Communication Protocol**
- Response time: within 24 business hours (set this expectation on Day 1)
- Project updates: every 2–3 days with a one-line status
- Scope change requests: always in writing, always with revised pricing before doing the work
- WEEK_1

---

### Template: SAAS

**Domain and Hosting**
Decision tree:
- Building a simple tool (few pages, API calls): Vercel (free tier, hobby plan)
- Building something with a database and user auth: Railway ($5/month starter) or Supabase (free tier)
- Need persistent background jobs: Fly.io (free allowance covers most MVPs)
- Domain: Namecheap (~$12/year) — don't buy more than 1 year until you have paying users
- DAY_1

**Auth Strategy**
- If user count < 100 expected: Supabase Auth (free, included in Supabase free tier)
- If user experience matters from day 1: Clerk (free up to 10,000 MAU)
- If you want zero auth complexity: magic link via Resend (free 3,000 emails/month)
- Do NOT build auth from scratch
- DAY_1

**Payments**
- US/Canada/Europe: Stripe Checkout (flat 2.9% + 30¢)
- Rest of world or wanting simpler tax compliance: Lemon Squeezy (5% + 50¢, handles VAT)
- Start with one-time payments, add subscriptions only when you have 5+ paying users
- DAY_1 (account creation) / WEEK_1 (integration)

**Claude API Integration**
Architecture pattern for Claude-powered SaaS:

```python
# System prompt stored in environment variable, not hardcoded
SYSTEM_PROMPT = os.environ["CLAUDE_SYSTEM_PROMPT"]

# Context management: keep conversation history in db, not in memory
def call_claude(user_message: str, conversation_id: str) -> str:
    history = db.get_conversation(conversation_id)  # last N turns
    response = anthropic.messages.create(
        model="claude-opus-4-6",  # or claude-haiku-4-5 for cost-sensitive paths
        max_tokens=1024,
        system=SYSTEM_PROMPT,
        messages=history + [{"role": "user", "content": user_message}]
    )
    db.save_turn(conversation_id, user_message, response.content[0].text)
    return response.content[0].text
```

Cost estimation: at claude-haiku-4-5 pricing, 1,000 API calls/month with 500-token average ≈ $0.50/month. Claude Opus 4.6 for same volume ≈ $15/month. Choose model tier based on task complexity, not habit.

- WEEK_1

**Database**
- SQLite (local dev) → PlanetScale (free tier, 1B row reads/month) or Supabase Postgres
- Don't over-engineer. For an MVP with <100 users, SQLite in production is fine.
- WEEK_1

**Monitoring**
- Sentry free tier (5,000 errors/month) for error tracking
- UptimeRobot free tier (50 monitors, 5-min checks) for uptime alerts
- WEEK_1

**MVP Feature Gate**
List what is NOT in v1:
- No admin dashboard (use database directly or Retool free tier)
- No team/multi-user support
- No API access for users
- No mobile app
- No integrations (webhooks, Zapier) until someone asks

---

### Template: CONSULTING

**Discovery Call Structure (60 minutes)**
```
0–5 min:   Introductions. "Tell me about your situation."
5–20 min:  Current state. What are they doing now? What's broken?
20–35 min: Pain inventory. What does the broken thing cost them? (money, time, risk)
35–45 min: Desired future. What would success look like in 90 days?
45–55 min: Fit check. Explain your approach. Ask: "Does this sound like what you need?"
55–60 min: Next step. Either: "Let me send you a proposal" or "This isn't a fit because X."
```
Never pitch during the discovery call. Just diagnose.
- DAY_1 (script in a doc, not memorized)

**AI Readiness Assessment Framework**
Deliverable template for first engagements (90–120 min audit → written report):

```markdown
# AI Readiness Assessment — [Company Name]
## Current State
- Data infrastructure: [accessible/fragmented/nonexistent]
- Existing AI tools in use: [list]
- Team AI literacy: [low/medium/high]
- Decision velocity: [bottlenecks identified]

## Highest-Value Automation Opportunities (top 3)
1. [Process] — [Est. time saved/week] — [Feasibility with Claude Code: high/medium/low]
2. ...

## Quick Wins (can be done in 2 weeks)
[Specific, actionable items]

## 90-Day Roadmap
[Phased plan]

## Investment Required
[Time, tools, external help]
```
- WEEK_1

**CRM Setup (minimal)**
- Notion database with columns: Company, Contact, Status, Last Touch, Next Action, Revenue
- Or HubSpot free CRM (more features, more overhead)
- Log every conversation within 24 hours
- DAY_1

**Retainer Structure**
- Advisory retainer: 4 hours/month, async + 1 video call — $[rate × 4 + 20% availability premium]
- Implementation retainer: 8–16 hours/month, hands-on Claude Code work — [hourly rate × hours]
- Don't offer retainers until you've completed at least one project successfully with the client
- WEEK_1

---

### Template: CONTENT

**Platform Selection Matrix**

| Goal | Platform | Why |
|------|----------|-----|
| Newsletter (B2B audience) | Beehiiv or Substack | Beehiiv has better monetization tools; Substack has built-in discovery |
| Newsletter (consumer/developer) | Substack | Network effects, easy setup |
| Long-form thought leadership | LinkedIn Articles + personal blog | SEO + professional credibility |
| Short-form developer content | Twitter/X + newsletter | Fast feedback, technical community |
| Video (demos, tutorials) | YouTube | Long shelf life, SEO |

Choose ONE primary platform. Distribute to secondary platforms after 4 weeks if primary is working.
- DAY_1

**Content Production Pipeline with Claude Code**

```
CONTENT_DRAFT_AGENT system prompt (save as environment variable):

"You are a writing assistant for [NAME], a [POSITIONING STATEMENT from persona_profile.json].
Given a topic, a target audience, and a platform, produce a first draft.
Voice: [voice_descriptors from persona_profile.json].
Never use: [avoid_phrases from persona_profile.json].
Always end with: a specific CTA that either invites a reply or links to [primary offering].
Format for [platform]: [platform-specific format rules — LinkedIn: no links in post body; 
Twitter: thread format with hook in first tweet; Blog: subheadings every 200 words]."
```

Usage:
```bash
claude --system-prompt "$CONTENT_DRAFT_AGENT" \
  "Write a LinkedIn post about [topic]. Target audience: [audience]. Tone: [tone]."
```
- WEEK_1

---

## Output Format — `technical_setup.md`

Structure the output as follows:

```markdown
# Technical Setup — [Job Title from chosen_job.json]

## Day 1 Checklist (complete before first outreach)
- [ ] [Tool 1]: [setup action] — [link or command]
- [ ] [Tool 2]: [setup action]
...

## Week 1 Checklist (complete before first delivery)
- [ ] [Tool N]: [setup action]
...

## Optional (add when needed, not before)
- [Tool]: [what it adds and when you'd need it]

## Claude Architecture (if applicable)
[System prompt, invocation pattern, cost estimate]

## Stack Summary
| Tool | Purpose | Cost | Tier |
|------|---------|------|------|
| ... | ... | ... | DAY_1/WEEK_1/OPTIONAL |
```

---

## Handoff Instructions

1. Save as `technical_setup.md`
2. Print a one-paragraph summary of the stack and total Day 1 setup time estimate
3. Flag any tool that requires a credit card even for free tier — note this in the summary
4. Pass to OPERATIONS_AGENT (Phase 5)
