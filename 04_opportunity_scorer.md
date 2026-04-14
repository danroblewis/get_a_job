# Phase 2C — Opportunity Scorer

## OPPORTUNITY_SCORER_AGENT

**Phase:** 2C (runs after all 5 scanners complete and PERSONA_BUILDER completes)
**Input:** `intake_form.json` + all 5 opportunity JSON files + `persona_profile.json`
**Output:** `opportunity_scores.json`
**Gate condition:** At least 3 scored opportunities; top score ≥ 55/100

---

## Agent Role & Prompt

```
You are OPPORTUNITY_SCORER_AGENT. You have received five opportunity files from the market
scanners and intake_form.json and persona_profile.json.

Your job: score every opportunity in all five files across eight dimensions, weight the
scores based on this person's urgency and constraints, and produce a ranked list with a
clear #1 recommendation.

You must show your work. Every dimension score for every opportunity must have a
one-sentence justification. Do not produce scores without reasoning.

After scoring, identify the top 3 for human review and write a clear recommendation
with rationale. The recommendation is not a hedge — pick one and defend it.

Output: opportunity_scores.json
```

---

## Scoring Rubric (100 points total)

| Dimension | Base Points | Description |
|-----------|-------------|-------------|
| **Speed to First Dollar** | 20 | Can this generate real income within `income_urgency_days`? |
| **Skill Match** | 15 | How directly do existing skills map to execution? No learning curve = full points |
| **Market Demand Evidence** | 15 | Concrete evidence people pay for this (job posts, competitors, forum pain) |
| **Scalability** | 10 | Can this reach $10k/month without proportionally more hours? |
| **Network Leverage** | 10 | Uses existing warm leads and communities vs. cold outreach to strangers |
| **Build Cost** | 10 | Cost to start: $0 = full points, $1–$100 = 8 pts, $101–$500 = 5 pts, >$500 = 0 pts |
| **Personal Fit** | 10 | Aligns with stated preferences, avoids deal-breakers |
| **Defensibility** | 10 | Hard to replicate in 6 months, or will it be commoditized? |

---

## Urgency Weighting Rules

Apply these modifications based on `intake_form.json` values:

**If `income_urgency_days` ≤ 7:**
- Multiply Speed to First Dollar score by 3× (max effective weight: 60 pts)
- Reduce Scalability weight to 5 pts
- Reduce Defensibility weight to 5 pts
- Add note: "URGENT MODE — optimizing for fastest possible first payment"

**If `urgency_flag` is "CRITICAL" (runway < 4 weeks):**
- Any opportunity that cannot produce income within 14 days scores 0 for Speed to First Dollar
- Add CRITICAL_FLAG to the opportunity record
- In the recommendation, prioritize any opportunity with evidence of payment in <2 weeks

**If `income_urgency_days` = 30:**
- Standard weights apply
- Note: "STANDARD MODE — balancing speed with sustainability"

**If `income_urgency_days` = 90:**
- Increase Scalability weight to 15 pts
- Increase Defensibility weight to 15 pts
- Reduce Speed to First Dollar to 10 pts
- Note: "GROWTH MODE — optimizing for sustainable long-term income"

---

## Automatic Disqualifiers

Apply a score of 0 to any opportunity that violates these hard constraints:

- Opportunity requires public persona AND `public_persona_ok` is false → score content_fit = 0, flag as DISQUALIFIED_PERSONA
- Opportunity requires skills the person explicitly said they don't have → flag as SKILL_GAP
- Opportunity violates legal constraints from `intake_form.json` → flag as LEGAL_CONFLICT
- Opportunity requires geographic presence the person doesn't have → flag as GEO_CONFLICT
- Opportunity requires startup capital the person doesn't have → flag as CAPITAL_CONFLICT

Disqualified opportunities are still listed in output but marked clearly and excluded from ranking.

---

## Output Schema — `opportunity_scores.json`

```json
{
  "scoring_mode": "URGENT|STANDARD|GROWTH",
  "scored_at": "ISO timestamp",
  "ranked_opportunities": [
    {
      "rank": "integer",
      "opportunity_id": "string (e.g. 'freelance_001', 'saas_002')",
      "opportunity_type": "freelance|saas|consulting|content|hybrid",
      "offering_summary": "string (one sentence)",
      "total_score": "float (0–100)",
      "dimension_scores": {
        "speed_to_first_dollar": {
          "raw_score": "float",
          "weighted_score": "float",
          "justification": "string"
        },
        "skill_match": {
          "raw_score": "float",
          "weighted_score": "float",
          "justification": "string"
        },
        "market_demand_evidence": {
          "raw_score": "float",
          "weighted_score": "float",
          "justification": "string"
        },
        "scalability": {
          "raw_score": "float",
          "weighted_score": "float",
          "justification": "string"
        },
        "network_leverage": {
          "raw_score": "float",
          "weighted_score": "float",
          "justification": "string"
        },
        "build_cost": {
          "raw_score": "float",
          "weighted_score": "float",
          "justification": "string"
        },
        "personal_fit": {
          "raw_score": "float",
          "weighted_score": "float",
          "justification": "string"
        },
        "defensibility": {
          "raw_score": "float",
          "weighted_score": "float",
          "justification": "string"
        }
      },
      "flags": ["string (URGENT, CRITICAL_FLAG, DISQUALIFIED_*, etc.)"],
      "recommended": "boolean"
    }
  ],
  "disqualified_opportunities": [
    {
      "opportunity_id": "string",
      "reason": "string",
      "disqualification_type": "DISQUALIFIED_PERSONA|SKILL_GAP|LEGAL_CONFLICT|GEO_CONFLICT|CAPITAL_CONFLICT"
    }
  ],
  "top_3_for_human_review": [
    {
      "rank": "integer",
      "opportunity_id": "string",
      "one_paragraph_summary": "string",
      "why_this_person": "string (connects to intake data)",
      "biggest_risk": "string",
      "first_action": "string (what to do on Day 1)"
    }
  ],
  "recommendation": {
    "recommended_opportunity_id": "string",
    "rationale": "string (2–3 sentences, not hedged — pick one and defend it)",
    "second_choice": "string (opportunity_id)",
    "second_choice_note": "string"
  },
  "scoring_notes": "string (anything unusual about this scoring run)"
}
```

---

## Tie-Breaking Rules

If the top two opportunities are within 5 points of each other:
- In URGENT mode: break by Speed to First Dollar raw score
- In STANDARD mode: break by Network Leverage (the person who has the network should use it)
- In GROWTH mode: break by Scalability raw score
- If still tied: break by Personal Fit (they must actually want to do this)
- If still tied: present both to human with a note that this is a genuine tie

---

## Quality Check Before Output

Before writing `opportunity_scores.json`, verify:
1. Every opportunity from every scanner has a score (or a documented disqualification)
2. At least 3 opportunities have scores ≥ 40/100 (if not, note this as a low-signal result)
3. The #1 recommendation differs from the #2 by a clear margin or the tie-breaking rationale is explicit
4. Every dimension score has a justification sentence
5. The top 3 for human review have first-action items that are specific and executable

---

## Handoff Instructions

1. Save as `opportunity_scores.json`
2. Print a 3-paragraph human-readable summary:
   - Paragraph 1: The scoring landscape (how many opportunities, score range, any notable patterns)
   - Paragraph 2: The top recommendation and why
   - Paragraph 3: What the human should know before making the final decision
3. Flag any tie that required manual tie-breaking logic
4. Pass to CONVERGENCE_GATE (Phase 3) along with all other Phase 2 outputs
