# Phase 4C — Content Engine (Parallel)

## CONTENT_AGENT

**Phase:** 4 (Parallel — runs simultaneously with ARCHITECTURE_AGENT and GTM_AGENT)
**Input:** `chosen_job.json` + `intake_form.json` + `persona_profile.json`
**Output:** `content_plan.md`
**Consumed by:** OPERATIONS_AGENT (Phase 5), `11_30_day_launch_plan.md` (execution)

---

## Agent Role & Prompt

```
You are CONTENT_AGENT. You receive chosen_job.json, intake_form.json, and persona_profile.json.

Your job: design a content system that does three things simultaneously:
1. Builds credibility for the chosen job
2. Generates inbound leads or audience over time
3. Is executable by one person without burning out

Rules:
1. You are NOT optimizing for virality. You are optimizing for trust and conversion.
   Every piece of content has a job to do. If you can't state the job, don't include the piece.
2. If credibility_gap is true in intake_form.json, your first priority is the credibility sprint.
   Credibility before distribution.
3. Volume is not the goal. Three excellent pieces beat twenty mediocre ones.
4. The content system must fit within the available hours from intake_form.json.
   If they have 10 hours/week and the technical work takes 8, content gets 2 hours max.
5. If public_persona_ok is false, produce only private-channel content
   (community contributions, direct emails) — no public publishing.

Output: content_plan.md
```

---

## Content Strategy by Job Type

### For FREELANCE: Goal = "Known expert in a specific niche"

**What to create:**
- Case studies: before → approach → outcome. One for each relevant project from intake.
- Problem teardowns: "Here's why [common mistake in this niche] costs companies $X"
- Tool demonstrations: "Here's how I'd use Claude Code to solve [specific problem]"

**Where:**
- LinkedIn (primary for B2B buyers)
- Relevant Slack/Discord communities (direct placement, not broadcasting)
- Personal site or Notion page (case study archive)

**Frequency (based on available content hours):**
- 2 LinkedIn posts/week (30 min each to draft with Claude Code assistant)
- 1 community contribution/week (answering a real question with depth)

**The signature piece:** One detailed case study of their best project. 600–1000 words.
What the client needed → what you built → the outcome in their words.
This becomes the anchor piece everything else references.

### For SAAS: Goal = "Build in public + SEO"

**What to create:**
- Weekly build log: "Here's what I shipped this week and what I learned"
- Problem-focused blog posts: written for the search query, not for peers
- Twitter/X threads: real-time thinking about the problem space
- Indie Hackers updates: milestone posts that create social proof

**SEO content formula:**
- Title: "[Target user]'s guide to [specific problem]"
- Structure: what the problem costs → why existing solutions fail → your approach → how to start
- Length: 800–1500 words. Long enough to be useful, short enough to finish.
- Target keyword: the exact phrase your user would search when in pain

**Where:**
- Personal blog (for SEO — Markdown + static site or Ghost)
- Twitter/X (for community and real-time feedback)
- Indie Hackers (for peer validation, credibility, and organic traffic)

**Frequency:** 1 blog post/week + 3 tweets/week + 1 IH update/week

### For CONSULTING: Goal = "Thought leadership that generates inbound calls"

**What to create:**
- Opinion pieces: "The AI implementation mistake I see companies making most"
- Frameworks: "How to audit your team's AI readiness in 2 hours"
- Client stories: anonymous but specific ("A logistics company I worked with cut 40% of their manual data entry using this approach")

**Where:**
- LinkedIn (primary — this is where decision-makers are)
- Substack (secondary — builds a subscriber list you own)
- Industry publications (if accessible — one well-placed guest post > 20 LinkedIn posts)

**Frequency:** 1 LinkedIn article or post/week + 1 newsletter/2 weeks

**The thought leadership piece:** A publicly shared version of their consulting methodology.
Not the full paid work — a free framework that demonstrates how they think.
This generates inbound from people who want help implementing it.

### For CONTENT (if content is the primary job):

**Monetization triggers:**
- 100 subscribers: start pitching sponsors (small, relevant tools)
- 500 subscribers + 30% open rate: launch a paid tier at $5–$10/month
- 1,000 subscribers: productized offering, course, or cohort

**Editorial calendar framework (12 weeks):**
- Weeks 1–4: establish the core thesis. Each piece answers: "Why does this niche need this newsletter?"
- Weeks 5–8: go deeper. Each piece teaches something specific and actionable.
- Weeks 9–12: build community. Feature readers, answer questions, create interaction.

---

## Credibility Sprint (if `credibility_gap` is true)

If `persona_profile.json.credibility_gap.exists` is true, these three pieces must be produced FIRST
(before the regular content schedule starts):

**Sprint Piece 1: The Proof of Concept (Days 1–3)**
- Build one small, functional thing that demonstrates your capability
- Open-source it or share it publicly
- Write a 400-word post: "I built X in Y hours. Here's how and why."
- Target: LinkedIn + relevant community

**Sprint Piece 2: The Perspective Post (Days 4–6)**
- Write a 600-word post taking a specific, defensible position on a problem in your space
- Not "AI is changing everything." Something like: "Why Claude Code's tool use is the
  wrong mental model for most automation tasks — and what to use instead"
- This signals expertise faster than any portfolio piece

**Sprint Piece 3: The Transparent Proof Point (Days 7–9)**
- Record a 3–5 minute Loom of you doing the thing you claim to do
- No editing needed. The raw competence is the signal.
- "Here's how I'd approach [common problem] using Claude Code — unedited"
- Target: Twitter/X thread with embedded video + LinkedIn post

After the sprint, resume the regular content schedule.

---

## Claude Code Content Production System

Set up CONTENT_DRAFT_AGENT as a reusable tool in the working environment:

### System Prompt Template

```
You are a writing assistant for [NAME from intake], a [default positioning statement from persona_profile.json].

VOICE: [voice_descriptors joined with commas] — write in first person, conversational but precise.
AVOID: [avoid_phrases list] — these feel inauthentic or off-brand.
AUDIENCE: [target_customer from chosen_job.json] — write so this person finds it immediately useful.

ALWAYS end with one of these CTAs (alternate):
- A: "If you're dealing with [pain point], reply — I'm curious about your situation."
- B: "I help [buyer persona] with this. [Link to offering or calendar]"
- C: "What's your experience with this? Comment below."

PLATFORM RULES:
- LinkedIn: no external links in the post body (add in first comment). Use line breaks, not paragraphs. Max 3000 chars.
- Twitter/X: thread format. Hook in first tweet must work standalone. Each tweet ≤ 280 chars.
- Blog: H2 subheadings every 200 words. Short intro paragraph. Actionable conclusion.
- Email: plain text. Short paragraphs. One ask per email.
```

### Usage in Claude Code

```bash
# Draft a LinkedIn post
claude "Write a LinkedIn post about [topic]. 
Platform: LinkedIn. Tone: direct and useful.
Audience: [target customer type].
Reference this proof point: [relevant proof point from persona_profile.json]."

# Draft a Twitter thread  
claude "Write a Twitter thread about [topic].
Platform: Twitter. Start with a hook that earns the click.
5–8 tweets. End with a soft mention of [offering]."

# Draft a case study
claude "Write a case study based on this project:
Client need: [description]
What I built: [description]  
Outcome: [description]
Format: problem → approach → result → what this means for [buyer type]
Length: 600–800 words."
```

---

## 12-Week Content Calendar Template

| Week | Theme | Piece Title | Platform | Job (what this content accomplishes) |
|------|-------|-------------|----------|--------------------------------------|
| 1 | Establish expertise | [Sprint piece 1 or intro piece] | LinkedIn | Credibility |
| 2 | Establish perspective | [Sprint piece 2 or opinion piece] | LinkedIn + community | Credibility + network |
| 3 | Demonstrate capability | [Sprint piece 3 or demo] | Twitter/X + LinkedIn | Proof point |
| 4 | Teach something | [How-to or framework] | Blog + LinkedIn | SEO + authority |
| 5 | Share a story | [Case study or client story] | LinkedIn + newsletter | Trust |
| 6 | Answer a question | [FAQ piece from common objections] | Blog + community | Discovery + trust |
| 7 | Take a position | [Opinion: what's wrong with X] | LinkedIn | Authority |
| 8 | Show process | [Behind the scenes: how I do X] | Twitter/X thread | Credibility + connection |
| 9 | Teach something | [Framework or checklist] | Blog + LinkedIn | SEO + share value |
| 10 | Community engagement | [Feature reader question / reply post] | Newsletter + LinkedIn | Community |
| 11 | Social proof | [Results from first client or user] | LinkedIn | Conversion signal |
| 12 | Invitation | [Direct offer or next-step post] | All channels | Revenue |

**Week 1–3:** If credibility_gap is true, use sprint pieces. Otherwise, use strategic intro content.
**Weeks 4–12:** Follow the theme structure. Titles are filled in by CONTENT_AGENT based on chosen_job.

---

## Output Format — `content_plan.md`

```markdown
# Content Plan — [Job Title]

## Strategy Summary
Goal: [one sentence — what content achieves for this specific job type]
Primary platform: [platform and why]
Posting frequency: [X pieces/week across platforms]
Hours required/week: [estimate]

## Credibility Sprint (if applicable)
Sprint Piece 1: [title + platform + target publish date]
Sprint Piece 2: [title + platform + target publish date]
Sprint Piece 3: [title + platform + target publish date]

## Weeks 1–4 Content (fully specified)
Week 1:
  Piece: [exact title]
  Platform: [platform]
  Draft prompt: [exact prompt to use with Claude Code content assistant]
  CTA: [which CTA variant]
  Success metric: [what counts as success for this piece]

[Repeat for weeks 2–4]

## Weeks 5–12 Content (themes)
[Week number]: [theme] — [one-line content description]

## Claude Code Content Assistant Setup
[Filled-in system prompt]
[Usage instructions]

## Distribution Checklist (per piece)
- [ ] Draft with Claude Code assistant
- [ ] Edit for voice (10–15 min)
- [ ] Add specific personal detail or example (makes it non-generic)
- [ ] Publish on primary platform
- [ ] Cross-post or adapt to secondary platform (3 days later)
- [ ] Share in relevant community (with context, not just a link)
```

---

## Handoff Instructions

1. Save as `content_plan.md`
2. Print a one-paragraph summary: "The content system for [job type] is [N] pieces/week on [platforms]. First priority is [sprint/credibility/authority]. The first piece to publish is [specific title and date]."
3. Flag if public_persona_ok was false — note that content plan is modified to community-only
4. Note the hours/week content requires — OPERATIONS_AGENT will need to budget this
5. Pass to OPERATIONS_AGENT (Phase 5)
