# Content Plan: AI Ops Consultant + Meeting Tool Subscription

**Generated:** 2026-04-13  
**Horizon:** 12 weeks  
**Status:** Ready to execute

---

## Section 1: Strategy Summary

**Goal:** Build external credibility for an AI ops consultant who has real tools and real users but no public proof — and convert that visibility into paying consulting clients and tool subscribers.

**Primary platform:** LinkedIn (300 existing connections, target audience is already there)  
**Secondary platform:** Public GitHub repo (technical proof) + Notion page (case study hub)

**Posting frequency:** 2 posts per week on LinkedIn (Tuesday and Thursday work well for B2B SaaS audiences)

**Hours required per week:** 2.5–3 hours total
- Drafting with Claude Code assistant: 1–1.5 hrs
- Editing + final polish: 45 min
- Publishing + distribution steps: 15–30 min

**What this content does:** Every piece either (a) demonstrates technical ability to a stranger evaluating a proposal, (b) attracts ops managers and chiefs of staff who are the exact consulting buyer, or (c) creates a linkable artifact that lives in proposals forever.

---

## Section 2: Credibility Sprint (Days 1–7, before regular schedule)

Run these three pieces before the regular cadence starts. They exist to give a stranger something to look at. Once they are live, every future piece links back to them.

---

### Piece 1: LinkedIn Post — The Meeting Summarizer

**Title:** Not needed for LinkedIn posts. Lead with the hook.  
**Platform:** LinkedIn  
**Time required:** 2–3 hours (drafting, editing, formatting)  
**Proof point created:** Public social proof that the tool exists, real people use it, and you built it. Becomes the primary link in every proposal and outreach message.

**The draft (paste this, edit for your voice, publish):**

---

*I built a meeting notes summarizer with Claude. Two colleagues I used to work with still use it every week. Here is what I learned.*

A few months ago, after my layoff, I started building tools for my own workflow. One of them was a script that takes a raw meeting transcript — the messy, timestamped wall of text you get from Zoom or Otter — and turns it into a clean summary with action items and owners.

I sent it to two former teammates. Neither of them asked for it. I just thought it might be useful.

They are both still using it.

That is the part that changed how I think about AI tools. It is not whether the demo is impressive. It is whether someone pulls it up on their own on a Tuesday morning, six weeks later, because it actually saves them time.

Here is what the tool does:
- Takes raw transcript as input (paste or file)
- Identifies decisions made, not just topics discussed
- Extracts action items with the person who said they'd do the thing
- Produces a summary short enough that you will actually read it

Here is what it does not do:
- It does not attend the meeting for you
- It does not catch things people implied but did not say
- It will occasionally misattribute an action item if two people are talking fast

I am formalizing it as a paid subscription tool at $29/month. If you run meetings at a B2B SaaS company and you are currently doing this cleanup by hand or skipping it entirely, that is who it is built for.

If you want early access or want to see how it works, message me or drop a comment.

The reason I am posting this publicly: I spent a long time building things that lived in private repos and Slack messages. That was a mistake. If the tool is useful, it should be findable.

---

**Formatting note before publishing:**
- Use line breaks exactly as shown above — short paragraphs, no bullet walls
- Add one image: a screenshot of a real (sanitized) output. Blur any names. This is the single highest-engagement addition you can make.
- Do not add hashtags in the post body. Put them as the first comment if you want them.

---

### Piece 2: Perspective Post — Taking a Position

**Platform:** LinkedIn  
**Time required:** 1.5–2 hours  
**Proof point created:** Establishes a point of view. Ops managers and founders who agree will follow. Those who disagree will engage. Both outcomes are good.

**Headline (the first line of the post):**

*Most companies are not ready for AI automation. They think the bottleneck is the tools. It is not.*

**Opening paragraph (draft):**

I have looked at a lot of ops stacks in the last year. The pattern is consistent: the company has Notion, Slack, Zapier, maybe Airtable, and a growing list of AI tools the team signed up for after someone saw a demo. But the manual work has not gone down. In some cases it has gone up, because now there is a new tool that also needs to be maintained.

The problem is not the tools. The problem is that the underlying process was never documented clearly enough to automate. You cannot automate a handoff that is currently held together by tribal knowledge and three Slack threads that nobody can find. Before the automation question, there is a prior question: does anyone actually know, in writing, what is supposed to happen?

**Complete the post with:**
- The three signs a process is not ready to automate (bad documentation, owner ambiguity, exception rate over 30%)
- What to do first (map it, not fix it)
- CTA: "If your team is trying to figure out where AI actually fits in your workflow, that's the kind of problem I work on. Message me."

---

### Piece 3: GitHub README for the Meeting Summarizer

**Platform:** GitHub (public repo)  
**Time required:** 3–4 hours (clean the code, write the README, push)  
**Proof point created:** Externally verifiable technical proof. A stranger can read the code, understand the problem it solves, and evaluate whether you know what you are doing. This link goes in every proposal.

**README structure — write it in this order:**

```markdown
# Meeting Notes Summarizer

A Claude-powered script that turns raw meeting transcripts into structured summaries with action items.

## The problem it solves

[2-3 sentences: what manual meeting notes cleanup costs in time, what gets missed, 
what happens to action items that live only in the transcript]

## What it produces

Given a raw transcript, the tool outputs:
- A 3-5 sentence summary of what was decided (not discussed — decided)
- Action items with the name of the person who committed to each one
- Open questions that were raised but not resolved

## Who uses it

Two operations professionals at B2B SaaS companies use this weekly. 
Neither is a developer.

## Setup

[Actual setup instructions: dependencies, API key, how to run it]

## Usage

[Exact command or usage example with a sanitized sample transcript]

## Limitations

[Be honest: what it gets wrong, when not to use it, what it requires from the input]

## License

MIT
```

**Key instruction:** The Limitations section is what makes this credible. Anyone who has worked with LLMs will trust you more for including it than for leaving it out.

---

## Section 3: Weeks 1–4 Content (Fully Specified)

Two posts per week. Each post is fully specified with a Claude Code draft prompt you paste directly into the content assistant.

---

### Week 1, Post 1

**Title:** "The manual handoff is not a people problem. Here is what it actually is."  
**Platform:** LinkedIn  
**CTA:** "What does your most-broken handoff look like? Drop it in the comments — I read every one."  
**Success metric:** 10+ comments from ops/founder titles within 48 hours

**Claude Code content assistant prompt:**
```
Write a LinkedIn post in my voice (direct, grounded, practical — no buzzwords, 
no enthusiasm performance) about the real cause of manual handoff failures in 
B2B SaaS ops. 

My angle: it is not a people problem or a communication problem. It is a 
documentation problem — specifically, no one has ever written down the 
decision rules that govern when something moves from one team to another. 
So every handoff requires a human to carry context that should be in a system.

Structure:
- Open with a specific, concrete observation (not a question, not a stat)
- Explain the actual mechanism of why handoffs fail
- Give one example of a fix that does not require new software
- Close with a question that invites ops managers to share their own situation

Length: 250-350 words. No bullet lists. Short paragraphs. 
Do not use: "passionate about," "thought leader," "leverage," "transformational," 
"excited to announce," "at the intersection of."
End with the CTA: "What does your most-broken handoff look like? Drop it in the 
comments — I read every one."
```

---

### Week 1, Post 2

**Title:** "Three questions I ask before writing a single line of automation code"  
**Platform:** LinkedIn  
**CTA:** "What workflow are you considering automating right now? I'll tell you which question to start with."  
**Success metric:** 15+ saves/reposts (this is a framework post — saves matter more than comments)

**Claude Code content assistant prompt:**
```
Write a LinkedIn post in my voice (direct, grounded, practical) presenting a 
three-question framework I use to decide whether a workflow should be automated.

The three questions are:
1. Can you write down exactly what happens in every case, including exceptions? 
   (If not, you do not have a process — you have a habit.)
2. How often does a human have to make a judgment call that cannot be documented? 
   (If more than 20% of cases, automation will fail at exactly the wrong moment.)
3. What is the actual cost if the automation is wrong once? 
   (Low stakes = automate. High stakes = human in the loop.)

Tone: skeptical of automation, not evangelical about it. I believe most ops 
teams should automate less than they think, not more. The value is in choosing 
the right 20%.

Format: brief intro, then the three questions each with 2-3 sentences of 
explanation. Close with the CTA.

Length: 300-400 words.
Do not write an intro that starts with "I" or uses a rhetorical question.
CTA: "What workflow are you considering automating right now? I'll tell you 
which question to start with."
```

---

### Week 2, Post 1

**Title:** "What I actually learned building an AI email triage agent"  
**Platform:** LinkedIn  
**CTA:** "If you're trying to figure out where AI fits in your own workflow, that's a specific kind of problem I help ops teams work through. Message me."  
**Success metric:** 3+ inbound DMs or connection requests from ops/founder titles

**Claude Code content assistant prompt:**
```
Write a LinkedIn post in my voice about what I learned building an AI email 
triage agent for my own inbox during a job search. First person, practitioner 
perspective.

Key honest insights to include:
- Where it worked: categorizing high-volume, pattern-based email (recruiters, 
  invoices, newsletters) with very high accuracy
- Where it failed: anything requiring judgment about relationship context, 
  urgency signals that depend on who sent it, or emails with implicit subtext
- The real lesson: LLMs are good at classification and extraction. They are bad 
  at reading between the lines. Design for that reality.
- One specific thing I would do differently: start with a much narrower scope 
  (just categorize, do not try to draft responses until the categorization is 
  reliable)

Tone: builder who actually ran this, not a reviewer of someone else's product. 
The credibility comes from specific failure, not generic success.

Length: 280-380 words. Short paragraphs. 
No bullet lists.
End with the CTA.
```

---

### Week 2, Post 2

**Title:** "Notion is not your ops problem. Here is what is."  
**Platform:** LinkedIn  
**CTA:** "What does your Notion actually look like right now? I am curious whether this pattern holds."  
**Success metric:** High engagement from Notion users; potential to be shared in Notion communities

**Claude Code content assistant prompt:**
```
Write a LinkedIn post in my voice about what ops teams actually get wrong with 
Notion and Airtable — not a criticism of the tools, but a diagnosis of how 
they are misused.

Core argument: The tools are not the problem. The problem is that ops teams 
use them to store information without designing for how information gets 
retrieved and acted on. Notion becomes a graveyard of pages nobody updates. 
Airtable becomes a spreadsheet with extra steps. Both problems have the same 
root: the database was built around how data is entered, not how decisions 
get made.

Include:
- One concrete pattern of Notion misuse (e.g., every project has a page but 
  there is no single view of all open action items across projects)
- One concrete pattern of Airtable misuse (e.g., fields added over time to 
  track edge cases until the base no longer reflects any real process)
- One thing that actually fixes it (design around the query you need most, 
  not the data you have)

Tone: opinionated but not condescending. Written as a peer to an ops manager, 
not as a consultant talking down.
Length: 280-350 words.
End with the CTA.
```

---

### Week 3, Post 1

**Title:** "How to explain AI automation to a non-technical boss without losing them in the first 30 seconds"  
**Platform:** LinkedIn  
**CTA:** "Forward this to whoever you have been trying to convince. Or send me a message if you are the one doing the convincing — I have done this enough to know which framings actually work."  
**Success metric:** High share rate (this is a utility post that solves a real immediate problem)

**Claude Code content assistant prompt:**
```
Write a LinkedIn post in my voice about how to translate AI automation 
capabilities to a non-technical manager or executive.

This is written for mid-level ops people trying to get buy-in, not for the 
executive themselves.

Core insight: Most pitches fail because they lead with the technology 
("we could use an LLM to...") instead of the cost of inaction 
("right now, someone is spending X hours per week doing Y by hand"). 
Non-technical stakeholders do not care about the tool. They care about the 
business problem.

Three framings that work:
1. Time translation: convert automation benefit into hours per week saved, 
   then multiply by headcount cost
2. Error rate argument: manual processes have a failure rate; automation 
   can make that failure rate visible and consistent rather than random
3. The "what breaks when someone is out" test: if the process stops working 
   when one person is on vacation, it is not a process — it is a dependency

What does not work:
- Starting with a demo
- Explaining how the AI works
- Comparing to a competitor who is "already doing this"

Length: 300-400 words. Short paragraphs.
End with the CTA.
```

---

### Week 3, Post 2

**Title:** "A short case study: what broke in a SaaS onboarding handoff and what fixed it"  
**Platform:** LinkedIn (with full version linked to Notion case study page)  
**CTA:** "Full write-up is linked in the first comment. If this pattern looks familiar, I'd be happy to talk through whether there's a version that applies to your team."  
**Success metric:** Clicks to the Notion case study; this post becomes the first anchor for external proof beyond the meeting summarizer

**Claude Code content assistant prompt:**
```
Write a LinkedIn post in my voice presenting a brief case study from a past 
SaaS ops role. No company name. Describe the problem and fix in enough 
operational detail that an ops manager will recognize it immediately.

The scenario: a customer onboarding process where the handoff from sales to 
CS was failing silently. Deals closed, then sat in a queue with incomplete 
information because the data collected by sales did not match what CS needed 
to start onboarding. Nobody knew a deal was stuck until the customer emailed 
asking why nothing had happened.

The fix: not a new tool. A shared intake document with required fields, a 
Slack notification triggered when a deal moved to "closed-won" in the CRM 
that auto-populated key fields into a CS checklist, and a weekly review 
of anything that had been in "onboarding pending" for more than 3 days.

What this taught me:
- The failure was not in the handoff moment — it was in the 2 weeks before 
  it where bad data was being collected
- Automation of a broken process just makes the breakage happen faster
- The fix had to start with the data, not the notification

Tone: practitioner retelling a real situation, not a polished consultant case study. 
Length: 300-380 words.
End with the CTA. Note that the full version is in the first comment.
```

---

### Week 4, Post 1

**Title:** "What six years in SaaS ops taught me that I did not expect"  
**Platform:** LinkedIn  
**CTA:** "If you are an ops manager or chief of staff trying to figure out where AI actually fits — not theoretically, practically — that is the specific problem I work on. Message me."  
**Success metric:** Profile visits and connection requests; this is a credibility and trust post

**Claude Code content assistant prompt:**
```
Write a LinkedIn post in my voice about unexpected lessons from six years 
in B2B SaaS operations. Personal and specific — not generic career advice.

Three real lessons (write with specific texture, not abstractions):
1. The most important ops work is the work nobody asks for — the undocumented 
   process that runs fine until the one person who carries it in their head 
   leaves. Finding and documenting that before it breaks is the highest-value 
   thing an ops person can do.
2. Non-technical stakeholders do not resist technology — they resist 
   uncertainty. If you can show them exactly what will change and what will 
   not, adoption is much easier than most technical people expect.
3. The ROI of ops work is usually invisible until it fails. That makes it 
   politically difficult to fund and easy to cut. The ops people who survive 
   long-term learn to make their wins visible without being annoying about it.

Tone: reflective but not sentimental. No "looking back on my journey." 
Just honest observations from someone who did the work.
Length: 300-380 words.
End with the CTA.
```

---

### Week 4, Post 2

**Title:** "Six months of building AI tools for my own workflow: what works, what does not, what I will keep"  
**Platform:** LinkedIn  
**CTA:** "The meeting summarizer is the one tool I would actually charge money for. If you run B2B SaaS ops and you want to try it, message me — I am offering the first month free to five people this month."  
**Success metric:** Direct tool trial signups; this is a conversion post

**Claude Code content assistant prompt:**
```
Write a LinkedIn post in my voice doing an honest audit of six months of 
building AI tools for personal and professional use.

Tools I built:
- Email triage agent (3 months of personal use)
- Meeting notes summarizer (actively used by 2 colleagues, now paying product)
- Job description screener (built for job search, used heavily)
- Household budget categorizer (still using it)

What actually worked:
- Any tool doing classification or extraction on structured-ish text
- Tools where I control the input format (transcripts, emails with predictable structure)
- Tools where being wrong 5% of the time is acceptable

What did not work:
- Anything requiring judgment about relationships or context outside the text
- Tools where I needed confidence, not probability
- Any use case where I could not review the output before it mattered

What I will keep building:
- Small, focused tools that do one thing reliably
- Tools for non-technical users who do not want to prompt-engineer

The meeting summarizer is the one I am most proud of — not because it is 
technically impressive, but because the two people using it would notice 
immediately if it stopped working. That is the bar worth hitting.

Tone: honest audit, not a success story. Credibility comes from admitting 
what did not work.
Length: 300-400 words.
End with the CTA (first month free offer).
```

---

## Section 4: Weeks 5–12 Content (Themes)

Continue 2 posts/week. These are themes — use the Claude Code content assistant to draft each specific piece.

| Week | Theme | One-line description |
|------|-------|----------------------|
| 5 | The documentation problem | Why ops teams are not actually bad at execution — they are bad at writing down what they do, and why that matters for automation |
| 6 | Real tool stack review | Honest take on what tools are worth paying for in a 15-50 person SaaS ops stack (Notion, Airtable, Linear, Slack, Zapier) |
| 7 | Client story #1 | First paid project deliverable — what the client needed, what was built, what it took, what changed (with permission) |
| 8 | AI hype correction | Specific AI claims that do not hold up in practice — with the more accurate version of each claim |
| 9 | The build vs. buy decision | How to evaluate whether your ops problem needs custom code or a SaaS tool — the actual decision tree |
| 10 | Process debt | What process debt looks like, how it compounds, and how to identify the highest-leverage place to start reducing it |
| 11 | Subscriber milestone + tool update | When the meeting summarizer hits 5 paying subscribers, post about what you learned getting there — honest, not triumphant |
| 12 | 90-day retrospective | What worked, what did not, what is next — genuine reflection post that doubles as social proof of traction |

---

## Section 5: Claude Code Content Assistant Setup

Save this as your content assistant context. The simplest implementation: create a file at `~/content_assistant_prompt.txt` and paste it into a new Claude conversation before each drafting session. Or add it as a Project context in Claude.ai if you use that interface.

---

**The exact system prompt — copy and paste the block below:**

```
You are a content drafting assistant for a B2B SaaS ops consultant and 
automation builder. You write LinkedIn posts and short-form content.

VOICE AND TONE:
- Direct, grounded, practical
- Writes like a practitioner, not a consultant
- No enthusiasm performance — does not announce excitement, does not use 
  words like "thrilled," "excited to share," "honored"
- Skeptical of hype, including AI hype
- Specific over general — concrete examples beat abstractions every time
- Short paragraphs (2-4 sentences max)
- No bullet lists unless the piece is explicitly a list post
- Does not start sentences with "I" in the opening line

BANNED PHRASES — never use these:
- "I am passionate about"
- "leverage" (when used as a verb for anything other than physical levers)
- "thought leader"
- "transformational"
- "disrupting the space"
- "at the intersection of"
- "excited to announce"
- "results-driven"
- "I wear many hats"
- "I help businesses unlock their potential"
- "full-stack problem solver"
- "dynamic professional"

AUDIENCE:
Primary: Ops managers, chiefs of staff, and heads of CS at B2B SaaS companies 
with 15–100 employees. They are smart, time-pressed, and skeptical of vendor 
pitches. They respond to specificity and honesty. They ignore jargon.

CREDIBILITY RULES:
- All claims must be grounded in direct experience (6 years B2B SaaS ops, 
  or tools actually built and in use)
- Never claim outcomes that have not happened
- Admitting limitations builds more credibility than overselling
- The meeting summarizer has two active users. The email triage agent was 
  used personally for 3 months. These are the primary proof points.

FORMAT FOR LINKEDIN:
- Hook in the first line (observation, counterintuitive claim, or specific 
  detail — not a rhetorical question)
- 250–400 words for standard posts
- End with one CTA (comment, message, or follow — not all three)
- Do not add hashtags in the post body (they go in a reply comment)

When given a drafting prompt, produce the post. Then on a new line after 
the post, write "EDIT NOTE:" followed by one sentence identifying the 
weakest line in the draft and why.
```

---

**To use:** Open a new Claude conversation (or start a new Project session), paste the system prompt above as the first message, confirm with "understood," then paste the drafting prompt for that week's post.

---

## Section 6: Distribution Checklist (Per Piece)

Run this checklist for every piece, from draft to live.

---

### Step 1: Draft (30–45 min)
- [ ] Paste the Claude Code content assistant system prompt into a new session
- [ ] Paste the specific drafting prompt for this piece
- [ ] Review the draft. Check: does the opening line make you want to keep reading? Is there at least one specific, concrete detail?
- [ ] Read the EDIT NOTE. Fix the weak line.
- [ ] Do one pass for banned phrases (Ctrl+F: "passionate," "leverage," "excited," "transformational")
- [ ] Cut any sentence that does not add information — most drafts have 2-3 of these

### Step 2: Polish (15 min)
- [ ] Read aloud once. Anything that sounds like a press release gets cut.
- [ ] Check paragraph breaks — no paragraph longer than 4 sentences
- [ ] Write the CTA last. Make sure it asks for exactly one thing.
- [ ] If the piece references the meeting summarizer or GitHub repo, confirm those links are live before publishing

### Step 3: Publish (10 min)
- [ ] Post to LinkedIn during business hours Tuesday–Thursday (9am–11am local time gets the most reach for B2B audiences)
- [ ] Add the image if the piece calls for one (screenshot of tool output, or no image — do not use stock photos)
- [ ] Post is live — add the hashtag comment immediately: reply to your own post with `#SaaSops #AItools #Operations` (these go in the comment, not the post body)

### Step 4: Distribution (15 min, same day as publish)
- [ ] Text or DM the two existing tool users with: "Posted something that might resonate with your ops work — [link]. If it sounds right, a share or comment would mean a lot right now."
- [ ] Forward the link to your former manager with one sentence of context: "Writing about ops stuff publicly now — this one is about [topic]. Sharing in case it's useful to pass along."
- [ ] Check back at 4 hours and 24 hours — respond to every comment within 24 hours (LinkedIn algorithm rewards comment responses with more reach)

### Step 5: Recycle and Build (10 min, day after publish)
- [ ] Note the engagement number (likes + comments + shares) in a simple tracking note
- [ ] If a post gets >15 comments, note the topic — that is a theme to return to
- [ ] If a post generates a DM asking about your work, that is a lead — respond within 4 hours
- [ ] Every 4th week, check whether the Notion case study page or GitHub repo needs updating based on what content has driven traffic

---

### Distribution Checklist for Credibility Sprint Pieces (Days 1–7 only)

For the three sprint pieces, add these steps:

**After the LinkedIn meeting summarizer post:**
- [ ] Message both tool users within 1 hour of publishing: "Just posted about the summarizer publicly for the first time. Would mean a lot if you'd leave a comment saying what you use it for — one sentence is plenty."
- [ ] Message former manager: "Starting to put my ops and automation work out publicly. Posted about a tool I built that two of our former colleagues still use — [link]. Would love a share if it feels right."

**After the GitHub README is live:**
- [ ] Edit the LinkedIn meeting summarizer post's first comment to add the GitHub link: "The code is here if you want to see how it works: [link]"
- [ ] Add the GitHub link to your LinkedIn profile under "Featured"

**After the perspective post:**
- [ ] Share in r/ClaudeAI if the post is relevant to AI tool building (it probably is) — use the "self-post" format, paste the content directly rather than just posting a LinkedIn link

---

*Total estimated time for this plan: 2.5–3 hours/week during regular cadence. Credibility sprint (Days 1–7) requires 8–12 hours one-time investment. After that, the sprint artifacts pay dividends indefinitely — every proposal links to the LinkedIn post and the GitHub repo.*
