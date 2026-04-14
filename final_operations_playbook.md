# Operations Playbook
**AI Ops Consultant + Meeting Tool Subscription**
*Last updated: April 13, 2026 — open this at 6am, know exactly what to do*

---

## 1. The Job

You build Claude Code automations for B2B SaaS ops teams — the workflows sitting in someone's backlog labeled "we should automate this" that never get done because engineering has other priorities. Buyers are operations managers, chiefs of staff, and CS leads at 15–100 person companies. Projects run 2–3 weeks at fixed price: $500 entry, $2,700 core (most common), $5,400 premium. Alongside consulting, you sell a meeting transcript summarizer for $29–$49/month to the same audience. The business matters because the problem is real: manual ops work costs 5–20 hours per week at companies that can't afford to hire for it, and Claude Code can eliminate most of it in under three weeks.

---

## 2. Who You Serve

**Primary consulting buyer:** Operations manager or chief of staff at a Series A–B SaaS company (20–80 people), 6–18 months into the role, still inheriting process debt, not yet fully staffed. They have Notion, Slack, Airtable, or Gmail problems that are clearly automatable but never get prioritized. A $500–$2,700 project is a personal budget call, not a procurement process.

**Tool subscriber:** Same audience. Currently doing meeting note cleanup manually or skipping it entirely. Not a developer. Pays $29/month because it saves more than an hour a week.

**Not your buyer:** Large enterprise (long procurement cycles), non-SaaS, or anyone whose primary problem is data infrastructure rather than workflow ops.

---

## 3. How You Find Them

**Outreach (primary, weeks 1–4):**
- 10 named targets, 5 warm leads — all messages already written in gtm_plan.md
- 5 outreach messages/week minimum: 2 warm (text or LinkedIn DM), 3 cold (LinkedIn DM, researched)
- Expected path: 5 messages → 1–2 responses → 1 discovery call → 0.5 proposals → 0.25 closes
- Calendly link in every message; calls capped at 2:30pm for school pickup buffer

**Content (secondary, supporting trust):**
- LinkedIn 2x/week: Tuesday + Thursday, 9–11am
- 2.5–3 hrs/week total including drafting with Claude Code content assistant
- Credibility sprint first (days 1–7): meeting summarizer post, position post, GitHub README
- Content does not replace outreach — it makes outreach responses more likely to convert

**Conversion path:** Warm message → discovery call → proposal within 48 hours → deposit invoice → work begins within 7 days of payment.

---

## 4. What You Deliver

**Consulting — every project:**
- Working Claude Code automation deployed in the client's tools (Notion, Slack, Airtable, Gmail)
- Tested on minimum 5 real client data samples before handoff
- 30–60 minute live handoff session (screen share, recorded, sent to client)
- README written for a non-technical user
- 14 days async email support for bugs (not scope changes); response within 24 hours weekdays
- Payment: 50% deposit before work, 50% on delivery via Stripe

**Tool subscription — every subscriber:**
- Zip file + Google Doc setup guide sent by email within 24 hours of payment
- Stripe customer portal link for self-service cancellation
- Tracked in Notion table: name, email, Stripe ID, status, access sent
- Support: setup issues only; email, 24-hour response weekdays; 3+ emails/month = refer to consulting

**Architecture standard:** Every automation follows the same four-layer pattern: Trigger → Context Loader → Claude Call → Output Handler. One GitHub template repo, copied per client. Haiku for extraction/classification; Opus for judgment-heavy tasks.

---

## 5. Weekly Time Budget

**Total available: 30 hours/week. Hard stop: 2:30pm most days.**

| Category | Hours/Week | What Goes Here |
|---|---|---|
| Delivery work | 12 hrs | Client build, testing on real data, writing README, handoff prep, bug fixes within 14-day support window |
| Business development | 8 hrs | Outreach messages (5/week), discovery calls (up to 3), proposal writing (1–2 days of lead time), follow-ups |
| Content | 3 hrs | 2 LinkedIn posts (draft with Claude assistant, edit, publish, respond to comments within 24 hrs) |
| Admin | 2 hrs | Stripe invoices, user management table updates, Calendly review, email triage |
| Buffer / overflow | 5 hrs | Scope changes, unexpected bugs, calls that run long, life with kids |

**Practical constraints:**
- School pickup at 3pm: book discovery calls 9am–2pm only; set Calendly availability to end at 2:30pm
- No weekends, no evenings: state this in kickoff emails, enforce it from day one
- If delivery work hits 15+ hrs in a given week, pause new outreach that week

---

## 6. This Week's Schedule (Week of April 13)

### Monday, April 14
**If you do nothing else:** Send Message 1 (text to Ex-Colleague A — subscription conversion + project ask)
**Must complete:** Send Message 1. Set up Stripe account and connect bank. Create $29/mo subscription product + payment link.
**Nice to complete:** Save proposal template and contract template locally. Create Notion user management table.

### Tuesday, April 15
**If you do nothing else:** Send Message 2 (LinkedIn DM to Ex-Colleague B — subscription + project)
**Must complete:** Send Message 2. Set up Calendly with intake questions, availability capped at 2:30pm. Post LinkedIn credibility sprint piece #1 (meeting summarizer post — draft is in content_plan.md).
**Nice to complete:** Create GitHub repo with standard template structure.

### Wednesday, April 16
**If you do nothing else:** Send Message 3 (LinkedIn DM to former manager — referral + 20-min call ask)
**Must complete:** Send Message 3. Package meeting summarizer for delivery (zip + Google Doc setup guide). Test delivery workflow on yourself — send the welcome email to your own inbox.
**Nice to complete:** Write and push GitHub README for the meeting summarizer (credibility sprint piece #3).

### Thursday, April 17
**If you do nothing else:** Post LinkedIn credibility sprint piece #2 (position post — "most companies aren't ready for AI automation")
**Must complete:** LinkedIn post live by 10am. Send Message 4 (cold DM to VP of Ops at Series B target). Follow up with Ex-Colleague A if no response to Monday's text.
**Nice to complete:** Send 1–2 additional cold DMs to targets #7 and #9 from the first buyers list.

### Friday, April 18
**If you do nothing else:** Review the week: did you send 5 messages? Book any calls? Log it.
**Must complete:** Send Message 5 (soft launch LinkedIn post to all connections — draft in gtm_plan.md Section 2). Respond to any messages or comments from the week.
**Nice to complete:** Run the GitHub README test — can you follow your own setup instructions cold? Fix anything that breaks.

---

## 7. KPI Dashboard

Track every Sunday. Takes 10 minutes.

| Metric | Week 1 Target | Week 2 Target | Week 3 Target | Week 4 Target |
|---|---|---|---|---|
| Outreach messages sent | 5 | 8 | 10 | 10 |
| Responses received | 2 | 3 | 4 | 5 |
| Discovery calls held | 1 | 2 | 2 | 3 |
| Proposals sent | 0–1 | 1 | 2 | 2 |
| Revenue (consulting) | $0 | $0–$1,350 | $1,350–$2,700 | $2,700+ |
| Tool subscribers (paid) | 1–2 | 2–3 | 3–5 | 5+ |
| LinkedIn posts published | 3 (sprint) | 2 | 2 | 2 |
| Hours worked | 20–25 | 25–30 | 25–30 | 25–30 |

**30-day minimum to stay on track:** 1 paid consulting deposit ($1,350 or $500) + 2 paying tool subscribers = ~$1,408. This is survivable. Target: $1,500+.

---

## 8. The Minimum Viable Week

*Everything went sideways. You have 5 hours. Do exactly these three things:*

1. **Send 3 outreach messages** (1 hr): Ex-Colleague A text, Ex-Colleague B DM, former manager DM. These are already written. Copy, personalize the bracket fields, send.

2. **Publish 1 LinkedIn post** (1.5 hrs): Use the Claude Code content assistant. Paste the Week 1 Post 1 prompt from content_plan.md. Edit. Publish Tuesday or Thursday before 11am. Respond to any comments.

3. **Do 1 discovery call if booked, or follow up if not** (1.5 hrs): If a call is on the calendar, show up and run the discovery script. If nothing is booked, spend the time following up with anyone who responded but went quiet. One follow-up message takes 10 minutes.

Remaining 1 hour: admin. Check Stripe, update the user table if someone paid, send any overdue responses.

*Nothing else. No new tools. No setup tasks. No content planning. Just those three.*

---

## 9. Review Triggers

These thresholds activate the contingency matrix. When you hit one, open **10_contingency_matrix.md** before doing anything else.

| Trigger | Threshold | What It Signals |
|---|---|---|
| Outreach response rate | Fewer than 3 responses after 20+ messages sent over 14 days | Wrong message, wrong audience, or wrong channel — run the outreach audit |
| Discovery calls not converting | 3+ calls held, 0 proposals requested | Discovery script isn't uncovering real pain — revisit fit check section |
| Proposals not closing | 2+ proposals sent with no deposit received | Price, scope, or trust problem — check objection responses in gtm_plan.md |
| Revenue at Day 21 | $0 consulting revenue, 0 paid subscribers | Full contingency review — consider $500 entry project as lower barrier, or free trial for 1 subscriber to generate a testimonial |
| Hours creeping up | Consistently over 30 hrs/week | Delivery scope is expanding or business development is inefficient — audit where the time is going |
| Content producing nothing | 8 posts published, 0 inbound DMs from prospects | Reassess content strategy; shift toward more direct outreach until inbound develops |

---

## 10. If You Do Nothing Else Today

**Send this text message right now — takes 5 minutes:**

To Ex-Colleague A (the one already using your meeting summarizer):

> "Hey — glad you've been getting use out of the meeting summarizer. I'm formalizing it as a paid tool at $29/mo. Would that work for you? I can send a Stripe link and keep your setup exactly as is. Also, while I have you — I'm taking on a few paid automation projects this month. Is there anything in your stack right now where your team is doing something manually that drives you crazy? Happy to take a look and tell you honestly if it's something I can fix quickly."

This is Message 1 from gtm_plan.md, verbatim. It covers both the subscription conversion and the project opening. It takes 5 minutes to send. It is the highest-probability action available to you right now.

Send it before you do anything else today.

---

*Review this document every Sunday. Update the KPI table. If a trigger fires, open 10_contingency_matrix.md.*
