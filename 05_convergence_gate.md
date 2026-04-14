# Phase 3 — Convergence Gate (Human Decision)

## Overview

This is the only mandatory human checkpoint in the entire flow.
The machine has done its work. Now the person looks at the top 3 options and commits to one.

This gate exists because no algorithm can measure the person's actual willingness to execute.
A 90-point opportunity the person won't do is worth less than a 65-point opportunity they'll
pursue relentlessly. The human picks the bet.

**This gate cannot be automated.** Do not proceed to Phase 4 without a completed `chosen_job.json`.

---

## Prerequisites Checklist

Before opening this gate, verify all of the following exist:

- [ ] `intake_form.json` — complete, validated
- [ ] `freelance_opportunities.json` — exists (may be empty if no match)
- [ ] `saas_opportunities.json` — exists (may be empty if no match)
- [ ] `consulting_opportunities.json` — exists (may be empty if no match)
- [ ] `content_opportunities.json` — exists (may be empty if no match)
- [ ] `hybrid_opportunities.json` — exists (may be empty if no match)
- [ ] `persona_profile.json` — complete
- [ ] `opportunity_scores.json` — at least 3 scored opportunities

If any are missing, do not open the gate. Fix the missing artifact and return here.

---

## CONVERGENCE_AGENT

### Role & Prompt

```
You are CONVERGENCE_AGENT. Your job is to prepare the human decision package for the
convergence gate and, after the human decides, to encode their decision into chosen_job.json.

Step 1: Assemble the human review package from all Phase 2 outputs.
Step 2: Present it clearly — not a data dump. A readable one-pager.
Step 3: Walk the human through the decision matrix below.
Step 4: Listen to their choice. Ask: "Is there anything about this choice you're uncertain about?"
Step 5: If they're uncertain, explore it — do not pressure. The uncertainty might reveal a
        constraint not captured in intake that changes the recommendation.
Step 6: Once they commit, produce chosen_job.json exactly matching the schema below.
Step 7: Read chosen_job.json back to the human and ask for confirmation before saving.
```

---

## Human Review Package Format

Assemble a single readable summary with these sections:

### Section 1: Your Situation (from `intake_form.json`)
- Income urgency: X days | Financial runway: X weeks | Hours available: X–X/week
- Network: X warm leads | Communities: [list] | Past sales experience: [summary]
- Key constraint: [the most important constraint from intake]

### Section 2: What We Found (from opportunity files + scorer)
**Scoring mode used:** URGENT / STANDARD / GROWTH

**Top 3 Opportunities:**

For each, a structured mini-card:
```
Rank #N — [Opportunity Title]
Type: [freelance|saas|consulting|content|hybrid]
Score: [X/100]

What you'd actually do:
[1 sentence description of the day-to-day work]

Who pays you:
[buyer persona]

How you get paid first:
[first revenue action from scorer output]

Biggest upside:
[one thing that makes this compelling]

Biggest risk:
[honest risk statement]

What Day 1 looks like:
[specific action]
```

### Section 3: Our Recommendation
Agent's pick with 2–3 sentence rationale. Not hedged.

---

## Decision Matrix (Human Fills This Out)

Rate each of the top 3 options 1–5 on these four dimensions. Multiply by weights. Highest total wins.

| Criterion | Weight | Option A | Option B | Option C |
|-----------|--------|----------|----------|----------|
| I believe I will actually do this daily | 30% | | | |
| I believe I can get the first paying customer | 25% | | | |
| I'm excited to still be doing this in 3 months | 25% | | | |
| I don't have a major hidden objection to this | 20% | | | |
| **Weighted Total** | | | | |

> Note: This is not a replacement for the agent's scoring — it's a gut-check overlay.
> If the human's top differs from the agent's top, explore why before deciding.

---

## Possible Outcomes

### Outcome 1: Accept Recommendation
Human picks the #1 scored option.
Action: Populate `chosen_job.json` from opportunity data. Proceed to Phase 4.

### Outcome 2: Select Alternative
Human picks #2 or #3 with written rationale.
Action: Note the override reason in `chosen_job.json.selection_rationale`. Proceed to Phase 4.

### Outcome 3: Hybrid Selection
Human wants to combine elements from multiple options (e.g., "freelance first, SaaS second").
Action: CONVERGENCE_AGENT writes a custom `chosen_job.json` encoding the combined model.
Flag `job_type` as "hybrid" and describe the sequencing in `hybrid_sequencing`.

### Outcome 4: Reject All Options
Human rejects all three. (This should be rare if intake was honest.)
Action: Do NOT force a choice. Ask: "What would have to be true about an option for you to commit to it?"
Record the answer. Re-run market scanners with the new constraint. Return to this gate.
Reference `10_contingency_matrix.md` Failure Mode 3.

---

## `chosen_job.json` Schema

```json
{
  "job_title": "string (what you call this work — the human's own words)",
  "job_type": "freelance|saas|consulting|content|hybrid",
  "one_sentence_description": "string (what you do, for whom, at what price)",
  "target_customer": "string (specific — not 'businesses')",
  "core_deliverable": "string (what the customer receives)",
  "pricing_model": {
    "type": "fixed|hourly|retainer|subscription|hybrid",
    "entry_price": "integer (USD — the low-friction first engagement)",
    "core_price": "integer (USD — the main offering)",
    "premium_price": "integer (USD — the expanded engagement)"
  },
  "primary_acquisition_channel": "string (where first customers come from)",
  "monthly_income_target": {
    "30_days": "integer (USD)",
    "90_days": "integer (USD)"
  },
  "key_dependencies": ["string (things that must be true for this to work)"],
  "first_revenue_action": "string (the single next action — specific, executable TODAY)",
  "selection_rationale": "string (why this was chosen — human's own words)",
  "override_of_recommendation": "boolean",
  "override_reason": "string or null",
  "hybrid_sequencing": [
    {
      "phase": "string",
      "income_type": "string",
      "trigger_to_next": "string"
    }
  ]
}
```

---

## Handoff to Phase 4

Once `chosen_job.json` is complete and confirmed by the human:

1. Save the file
2. Distribute to ALL Phase 4 agents simultaneously:
   - ARCHITECTURE_AGENT (receives `chosen_job.json` + `intake_form.json` + `persona_profile.json`)
   - GTM_AGENT (receives `chosen_job.json` + `intake_form.json` + `persona_profile.json`)
   - CONTENT_AGENT (receives `chosen_job.json` + `intake_form.json` + `persona_profile.json`)
3. All three Phase 4 agents launch in parallel — do not wait for one before starting the others
4. Tell the human: "Phase 4 is running. Three agents are building your technical setup, your go-to-market plan, and your content system simultaneously. This may take a few minutes."
