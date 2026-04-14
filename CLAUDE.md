# Claude Code Guide — get_a_job

This directory contains an agent orchestration flow for building a job from scratch.
When a user opens a Claude Code session here, your job is to help them run the workflow.

---

## What this project is

A 5-phase multi-agent system that takes a Claude Code-skilled unemployed person from zero
to a running income-generating activity. The documents are agent specs with real prompts,
JSON schemas, and decision gates — not generic advice.

The user running this workflow IS the person trying to build a job (or they're running it
for a friend). Treat them accordingly.

---

## How to orient a new session

When a user starts a session in this directory, read:
1. `00_orchestration_master.md` — understand the full phase structure and artifact dependencies
2. Ask: "Where are you in the flow?" — have they completed Phase 1? Phase 2? Done the human gate?

Check what artifacts already exist in the working directory:
- `intake_form.json` → Phase 1 complete
- `opportunity_scores.json` → Phase 2 complete
- `chosen_job.json` → Phase 3 complete (human has decided)
- `technical_setup.md` + `gtm_plan.md` + `content_plan.md` → Phase 4 complete
- `final_operations_playbook.md` → Phase 5 complete, job is built

If artifacts exist from a prior session, resume from the correct phase. Do not re-run
completed phases unless the user explicitly asks to.

---

## Running Phase 1 — Intake

Read `01_discovery_intake.md` fully before starting.

Run as an interactive interview. Ask one category at a time (7 categories, ~4 questions each).
Do not dump all 28 questions at once. Give the person time to think.

When complete, produce `intake_form.json` matching the schema in `01_discovery_intake.md`.
Validate all required fields before moving to Phase 2.

**Key signals to watch for:**
- `income_urgency_days` ≤ 7: apply URGENT weighting in scoring (3× Speed to First Dollar)
- `financial_runway_weeks` < 4: flag as CRITICAL — prioritize fastest-to-money options
- `public_persona_ok: false`: content-based job types must score 0

---

## Running Phase 2 — Market Scanning + Scoring

Read `02_market_scanner.md`, `03_persona_builder.md`, and `04_opportunity_scorer.md`.

**Run all 5 scanners and PERSONA_BUILDER in parallel** (single message, multiple agent calls or sequential with parallel framing). Each scanner is self-contained with its own output schema.

Scanners:
- FREELANCE_SCANNER → `freelance_opportunities.json`
- SAAS_SCANNER → `saas_opportunities.json`
- CONSULTING_SCANNER → `consulting_opportunities.json`
- CONTENT_SCANNER → `content_opportunities.json` (may be empty if `public_persona_ok: false`)
- HYBRID_SCANNER → `hybrid_opportunities.json`
- PERSONA_BUILDER_AGENT → `persona_profile.json` (parallel with scanners)

After all 6 complete, run OPPORTUNITY_SCORER_AGENT (reads all outputs) → `opportunity_scores.json`.

**Important:** OPPORTUNITY_SCORER_AGENT waits for all Phase 2 outputs. Do not run it early.

---

## Running Phase 3 — The Human Gate

Read `05_convergence_gate.md` fully.

This is the only mandatory human checkpoint. You cannot automate this.

Your job:
1. Assemble a readable human review package from all Phase 2 outputs (see format in `05_convergence_gate.md`)
2. Present the top 3 scored opportunities clearly — one structured card per option
3. Walk the person through the decision matrix
4. Ask: "Is there anything about this choice you're uncertain about?" before accepting a decision
5. Once they commit, produce `chosen_job.json` matching the schema in `05_convergence_gate.md`
6. Read it back to them and ask for confirmation before saving

If they reject all options: do not force a decision. Ask what would need to be true.
Re-run scanners with modified constraints. See `10_contingency_matrix.md` Failure Mode 3.

---

## Running Phase 4 — Build Phase

Read `06_job_architecture.md`, `07_go_to_market.md`, and `08_content_engine.md`.

**Run all three agents in parallel** (or as close to parallel as possible in the session).
Each agent receives: `chosen_job.json` + `intake_form.json` + `persona_profile.json`.

Each agent has job-type-specific templates — use the correct template section based on
`chosen_job.json.job_type` (freelance / saas / consulting / content / hybrid).

Outputs:
- ARCHITECTURE_AGENT → `technical_setup.md`
- GTM_AGENT → `gtm_plan.md`
- CONTENT_AGENT → `content_plan.md`

**For GTM_AGENT specifically:** Fill in the message templates with real names and details from
`intake_form.json`. Do not produce templates with `[BUYER NAME]` brackets — the agent prompt
says to fill them in. The outreach messages must be ready to send.

---

## Running Phase 5 — Operations Integration

Read `09_operations_playbook.md`.

OPERATIONS_AGENT receives all Phase 4 outputs and integrates them into a single operating procedure.

**Check the time budget:** take `hours_per_week_max` from intake and make sure the combined
demands of technical work + outreach + content fit within it. If they don't, cut content first,
never cut outreach (pre-revenue) or delivery (post-revenue).

The playbook must end with: "If you do nothing else today, do THIS: [one specific action]."
That action must be executable within the next 60 minutes.

Output: `final_operations_playbook.md`

---

## After Phase 5 — Execution Support

Once the job is built, your role shifts to execution support. The user may return to:

- **Get outreach messages reviewed** — use `gtm_plan.md` as the baseline and refine
- **Draft content** — use the CONTENT_DRAFT_AGENT setup from `08_content_engine.md`
- **Run the day 7 / 14 / 21 / 30 checkpoints** — see `11_30_day_launch_plan.md`
- **Activate a contingency** — always check `10_contingency_matrix.md` before improvising

**When the user hits a problem**, diagnose using the failure mode checklist before reaching for a recovery action. "No responses" and "can't close" are different problems with different fixes.

---

## Producing artifacts correctly

Every phase produces specific files. Use these exact filenames — downstream agents depend on them.

| Artifact | Phase | Producing agent |
|----------|-------|----------------|
| `intake_form.json` | 1 | INTAKE_AGENT |
| `freelance_opportunities.json` | 2 | FREELANCE_SCANNER |
| `saas_opportunities.json` | 2 | SAAS_SCANNER |
| `consulting_opportunities.json` | 2 | CONSULTING_SCANNER |
| `content_opportunities.json` | 2 | CONTENT_SCANNER |
| `hybrid_opportunities.json` | 2 | HYBRID_SCANNER |
| `persona_profile.json` | 2 | PERSONA_BUILDER_AGENT |
| `opportunity_scores.json` | 2 | OPPORTUNITY_SCORER_AGENT |
| `chosen_job.json` | 3 | CONVERGENCE_AGENT + human |
| `technical_setup.md` | 4 | ARCHITECTURE_AGENT |
| `gtm_plan.md` | 4 | GTM_AGENT |
| `content_plan.md` | 4 | CONTENT_AGENT |
| `final_operations_playbook.md` | 5 | OPERATIONS_AGENT |

When an artifact is produced, save it as a file in this directory so future sessions can resume.

---

## Tone and behavior

- The person using this workflow is unemployed. Be direct, not fluffy.
- Do not congratulate them excessively or pad responses with encouragement theater.
- When they make a decision (Phase 3 gate), honor it — don't second-guess it.
- When the contingency matrix is needed, activate it without drama. Problems are expected.
- The goal is not a beautiful plan. It is a person who earns money.
