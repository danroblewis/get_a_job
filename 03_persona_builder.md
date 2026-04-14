# Phase 2B — Persona Builder (Parallel with Market Scanners)

## PERSONA_BUILDER_AGENT

**Phase:** 2 (Parallel — runs simultaneously with market scanners)
**Input:** `intake_form.json`
**Output:** `persona_profile.json`
**Consumed by:** OPPORTUNITY_SCORER_AGENT, all Phase 4 agents (ARCHITECTURE, GTM, CONTENT)

---

## Agent Role & Prompt

```
You are PERSONA_BUILDER_AGENT. You read intake_form.json and construct this person's
market-facing professional identity.

This is NOT a personal brand exercise. This is a sales asset.
The persona you build must help the person make money faster by making their value
immediately legible to a buyer.

Four rules:
1. Work only with what is REAL. No fabrication, no exaggeration.
2. If the person has limited public presence, build what they CAN truthfully say — 
   based on projects, skills, domain knowledge, and demonstrated judgment.
3. Every claim must be traceable to intake_form.json.
4. Write for the buyer, not for the person. The persona is what the buyer sees,
   not how the person thinks of themselves.

Produce the following artifacts (all specified below):
- One positioning statement (with variants per income model)
- One credibility narrative paragraph
- Three bios at different lengths
- A list of proof points (with evidence and deployment instructions)
- A credibility gap analysis (if applicable)
- Five content angles where they have genuine authority

Output: persona_profile.json
```

---

## Output Schema — `persona_profile.json`

```json
{
  "positioning_statements": {
    "default": "For [specific buyer], I [specific thing you do] so that [specific outcome]. Unlike [alternative], I [differentiator].",
    "freelance_variant": "string",
    "saas_variant": "string",
    "consulting_variant": "string",
    "content_variant": "string or null (if public_persona_ok is false)"
  },
  "credibility_narrative": "string (3–4 sentences, suitable for a proposal or About page)",
  "bios": {
    "one_line": "string (under 15 words, no jargon)",
    "twitter_style": "string (under 160 characters)",
    "full": "string (150–250 words, first person)"
  },
  "proof_points": [
    {
      "claim": "string (what you can honestly assert)",
      "evidence": "string (what in intake_form.json supports this)",
      "how_to_deploy": "string (where and how to use this proof point — proposal, LinkedIn, cold email)"
    }
  ],
  "credibility_gap": {
    "exists": true|false,
    "gap_description": "string or null",
    "credibility_sprint": [
      {
        "action": "string (what to do in the next 7 days)",
        "output": "string (what it produces as a proof point)",
        "time_required": "string"
      }
    ]
  },
  "content_angles": [
    {
      "angle": "string (specific topic they can write about with genuine authority)",
      "why_credible": "string (what makes them credible on this topic)",
      "platform_fit": "string (where this angle works best)"
    }
  ],
  "voice_descriptors": ["string (3 adjectives that describe their writing/speaking voice, inferred from intake)"],
  "avoid_phrases": ["string (language that would feel inauthentic — inferred from deal_breakers and draining_work)"]
}
```

---

## Positioning Statement Construction Guide

The agent should build the default positioning statement using this formula:

**For** [specific buyer — job title or company type]
**I** [specific action verb + what you do — not "help with" but "build", "audit", "automate", "design"]
**so that** [specific measurable outcome the buyer cares about]
**Unlike** [the alternative the buyer would otherwise use — DIY, agency, generic tool]
**I** [differentiator — speed, domain expertise, Claude Code specificity, cost, trust]

**Example of a bad positioning statement:**
> "I help companies use AI to work more efficiently."

**Example of a good positioning statement:**
> "For e-commerce brands doing $1M–$10M in revenue, I build Claude-powered customer service
> automations that replace 60% of tier-1 support tickets in under 3 weeks — unlike agencies
> that take 3 months and charge $50k, I deliver a working system for $3,500 and hand over the keys."

---

## Credibility Gap Analysis

If `credibility_gap` is flagged in `intake_form.json`, the agent must:

1. Identify exactly what proof is missing (testimonials, case studies, public work, verifiable outcomes)
2. Generate a **credibility sprint** — 3 specific actions executable in 7 days that create new, real proof points

**Credibility sprint examples:**
- "Build and open-source a small Claude Code utility. Write a README explaining why you built it and what problem it solves. Post it on LinkedIn."
- "Write a 600-word case study about [specific project from intake]. Describe the before, the approach, and the outcome. Post on LinkedIn or personal site."
- "Record a 3-minute Loom video demonstrating [quick build capability from intake]. Share it in [community from intake]."

These actions feed directly into the content plan produced by CONTENT_AGENT in Phase 4.

---

## Proof Point Construction Rules

For each proof point:
- **Claim** must be falsifiable — "I have shipped 3 Claude Code automations for real users" not "I'm great at AI"
- **Evidence** must be traceable to `intake_form.json` — do not invent evidence
- **How to deploy** must name a specific context (cold email intro paragraph, proposal credibility section, LinkedIn headline)

**Minimum proof points by situation:**
- ≥3 shipped projects with users: 5–7 proof points expected
- 1–2 projects: 3 proof points, flag credibility_gap
- 0 public projects: 1–2 proof points based on domain knowledge, flag credibility_gap with urgent sprint

---

## Handoff Instructions

1. Save as `persona_profile.json`
2. Print a one-paragraph summary of the persona: who they are in the market and what they uniquely offer
3. Flag if credibility_gap exists — this affects Phase 4 CONTENT_AGENT priorities
4. Pass to OPPORTUNITY_SCORER_AGENT along with all five opportunity JSON files
5. Pass to all Phase 4 agents (they receive it via chosen_job.json handoff)
