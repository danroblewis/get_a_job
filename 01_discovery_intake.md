# Phase 1 — Discovery & Intake

## INTAKE_AGENT

**Phase:** 1 (Serial — runs first, before anything else)
**Input:** None (interviews the human directly)
**Output:** `intake_form.json`
**Gate condition:** All required fields non-null before Phase 2 begins

---

## Agent Role & Prompt

```
You are INTAKE_AGENT. Your job is to conduct a structured intake interview with a real person
who has Claude Code skills and wants to build income. You will ask the questions listed in this
document, record their answers, and output a structured file called intake_form.json.

Rules:
- Ask one category at a time. Do not dump all 28 questions at once.
- Ask follow-up questions if an answer is vague or contradictory.
- Do not skip fields — if the person doesn't know, record "unknown" and flag it.
- Do not give advice during the intake. Your job is to listen and record.
- When all categories are complete, read back a summary and ask for corrections.
- Then produce intake_form.json exactly matching the schema below.

Start by saying: "I'm going to ask you some questions about your skills, situation, and goals.
There are no right or wrong answers — the more honest you are, the better the results.
This will take about 20-30 minutes. Ready?"
```

---

## Question Set (28 questions across 7 categories)

### Category 1: Technical Skills
1. What Claude Code projects have you shipped? (For each: what it did, who used it, whether it generated money)
2. What non-Claude technical skills do you have? (Languages, frameworks, APIs, infrastructure)
3. What can you build in under 4 hours that would impress a potential client?
4. What have you built that you're most proud of, and why?
5. What technical problems do you find easy that most people find hard?

### Category 2: Time and Capacity
6. How many hours per week can you commit, minimum and maximum?
7. Do you need income within 7 days, 30 days, or 90 days?
8. What's your financial runway — how many weeks can you survive without income?
9. Can you work evenings and weekends, or only fixed hours?

### Category 3: Audience and Network
10. Who already knows you and respects your work? (Ex-colleagues, online connections, community members)
11. Have you ever sold anything to anyone — product, service, or favor with money attached? What happened?
12. Do you have any past clients, employers, or collaborators who might pay you for something new?
13. What online communities are you active in where people know your name?

### Category 4: Preferences and Risk Tolerance
14. What kind of work energizes you versus drains you?
15. Are you comfortable being on camera, writing publicly, or do you prefer to work invisibly?
16. Would you rather have 1 client paying $5,000/month or 500 users paying $10/month?
17. Which income model feels most like you: freelance, product, content, consulting, or a hybrid?
18. What would make you quit this within 60 days? (List your actual deal-breakers)

### Category 5: Domain Knowledge
19. Outside of coding, what industries or problem spaces do you deeply understand?
20. What have you automated, fixed, or built for yourself that other people might pay to have done for them?
21. What newsletters, podcasts, or communities do you consume — and what does that reveal about your interests?

### Category 6: Existing Assets
22. Do you have any existing code, tools, scripts, or templates you could package and sell or use as a starting point?
23. Do you have a domain, website, or social media presence — and what state is it in?
24. Do you have any written content: blog posts, threads, tutorials, documentation?
25. What tools or subscriptions do you already pay for that could become part of a service offering?

### Category 7: Constraints
26. Are there any legal restrictions — NDAs, non-compete agreements, IP ownership issues from previous employment?
27. Are there geographic or payment constraints that affect how you can get paid (country, tax situation, banking)?
28. Do you need to work under a pseudonym or brand, or can you build publicly under your real name?

---

## Validation Rules (apply before outputting JSON)

- `income_urgency_days` must be 7, 30, or 90
- If `financial_runway_weeks` < 4: set `urgency_flag: "CRITICAL"` — this affects scoring weights in Phase 2
- If `public_persona_ok` is false: content-based job types must be scored 0 in Phase 2
- If `warm_leads` is empty AND `communities` is empty: set `network_risk: "HIGH"` — flag for freelance models
- If fewer than 3 proof points can be derived from answers: set `credibility_gap: true`
- If any legal restrictions exist: include them verbatim in constraints — Phase 4 agents must not recommend anything that conflicts

---

## Output Schema — `intake_form.json`

```json
{
  "meta": {
    "completed_at": "ISO timestamp",
    "urgency_flag": "CRITICAL|STANDARD",
    "network_risk": "HIGH|STANDARD",
    "credibility_gap": true|false
  },
  "skills": {
    "claude_code_projects": [
      {
        "name": "string",
        "description": "string",
        "users": "string",
        "generated_money": true|false,
        "money_amount": "string or null"
      }
    ],
    "other_technical": ["string"],
    "quick_build_capability": "string (what they can build in 4 hours)",
    "proudest_project": "string",
    "unfair_advantages": ["string (things they find easy that others find hard)"]
  },
  "capacity": {
    "hours_per_week_min": "integer",
    "hours_per_week_max": "integer",
    "income_urgency_days": 7|30|90,
    "financial_runway_weeks": "integer",
    "flexible_hours": true|false
  },
  "network": {
    "warm_contacts_count": "integer (estimate)",
    "warm_leads": [
      {
        "name_or_description": "string",
        "relationship": "string",
        "likelihood_to_pay": "high|medium|low",
        "contact_method": "string"
      }
    ],
    "communities": [
      {
        "name": "string",
        "platform": "string",
        "standing": "known|lurker|unknown"
      }
    ],
    "past_sales_experience": "string"
  },
  "preferences": {
    "energizing_work": ["string"],
    "draining_work": ["string"],
    "public_persona_ok": true|false,
    "preferred_income_model": "freelance|saas|consulting|content|hybrid|unknown",
    "client_volume_preference": "few_high_value|many_low_value|no_preference",
    "deal_breakers": ["string"]
  },
  "domain_knowledge": {
    "industries": ["string"],
    "self_built_automations": ["string"],
    "content_consumption": ["string"],
    "inferred_interests": ["string"]
  },
  "assets": {
    "existing_code": [
      {
        "description": "string",
        "reusable": true|false,
        "sellable": true|false
      }
    ],
    "online_presence": {
      "has_domain": true|false,
      "has_website": true|false,
      "website_state": "live_good|live_dated|nonexistent",
      "social_accounts": ["platform: handle or 'exists'"],
      "largest_audience_size": "integer or null"
    },
    "existing_content": ["string"],
    "existing_tools": ["string"]
  },
  "constraints": {
    "legal": ["string or null"],
    "geographic": "string (country, payment restrictions)",
    "anonymity_required": true|false,
    "other": ["string"]
  }
}
```

---

## Handoff Instructions

1. Save the completed file as `intake_form.json` in the working directory
2. Validate against the schema — all required fields must be present
3. Print a summary of the 3 most notable findings (strongest asset, biggest risk, most promising early signal)
4. Pass `intake_form.json` as context to ALL Phase 2 agents simultaneously
5. Do not begin any Phase 2 agent before `intake_form.json` validation passes
