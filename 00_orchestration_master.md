# Job Construction Orchestration — Master Document

> **Mission:** Transform a Claude Code-skilled unemployed person into a self-employed income generator within 30 days. Every agent must produce a concrete artifact. The flow is done when the person has earned at least $1 from a repeatable activity they own.

---

## Agent Topology

```
┌─────────────────────────────────────────────────────────────────┐
│  PHASE 1 — SERIAL                                               │
│                                                                 │
│  INTAKE_AGENT ──────────────────────────────► intake_form.json │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│  PHASE 2 — PARALLEL (all agents launch simultaneously)          │
│                                                                 │
│  FREELANCE_SCANNER    ──────────► freelance_opportunities.json  │
│  SAAS_SCANNER         ──────────► saas_opportunities.json       │
│  CONSULTING_SCANNER   ──────────► consulting_opportunities.json │
│  CONTENT_SCANNER      ──────────► content_opportunities.json    │
│  HYBRID_SCANNER       ──────────► hybrid_opportunities.json     │
│                                                                 │
│  PERSONA_BUILDER_AGENT ─────────► persona_profile.json          │
│                                                                 │
│  (waits for all scanners)                                       │
│  OPPORTUNITY_SCORER_AGENT ──────► opportunity_scores.json       │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│  PHASE 3 — HUMAN GATE                                           │
│                                                                 │
│  Human reviews top 3 opportunities                             │
│  Human selects one + signs off                                  │
│  CONVERGENCE_AGENT ─────────────► chosen_job.json              │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│  PHASE 4 — PARALLEL (all three agents launch simultaneously)    │
│                                                                 │
│  ARCHITECTURE_AGENT ────────────► technical_setup.md            │
│  GTM_AGENT          ────────────► gtm_plan.md                   │
│  CONTENT_AGENT      ────────────► content_plan.md               │
└──────────────────────────┬──────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│  PHASE 5 — SERIAL                                               │
│                                                                 │
│  OPERATIONS_AGENT ──────────────► final_operations_playbook.md  │
└─────────────────────────────────────────────────────────────────┘

  CONTINGENCY_AGENT (passive, monitors KPIs, activates on failure signals)
```

---

## Global Artifacts

### Inputs (produced during the flow, consumed by later agents)
| Artifact | Produced By | Consumed By |
|----------|-------------|-------------|
| `intake_form.json` | INTAKE_AGENT | All Phase 2+ agents |
| `freelance_opportunities.json` | FREELANCE_SCANNER | OPPORTUNITY_SCORER_AGENT |
| `saas_opportunities.json` | SAAS_SCANNER | OPPORTUNITY_SCORER_AGENT |
| `consulting_opportunities.json` | CONSULTING_SCANNER | OPPORTUNITY_SCORER_AGENT |
| `content_opportunities.json` | CONTENT_SCANNER | OPPORTUNITY_SCORER_AGENT |
| `hybrid_opportunities.json` | HYBRID_SCANNER | OPPORTUNITY_SCORER_AGENT |
| `persona_profile.json` | PERSONA_BUILDER_AGENT | OPPORTUNITY_SCORER_AGENT, all Phase 4 agents |
| `opportunity_scores.json` | OPPORTUNITY_SCORER_AGENT | CONVERGENCE_GATE (human + agent) |
| `chosen_job.json` | CONVERGENCE_AGENT | All Phase 4 agents |
| `technical_setup.md` | ARCHITECTURE_AGENT | OPERATIONS_AGENT |
| `gtm_plan.md` | GTM_AGENT | OPERATIONS_AGENT, 30-day calendar |
| `content_plan.md` | CONTENT_AGENT | OPERATIONS_AGENT, 30-day calendar |

### Final Outputs (what "job built" looks like)
| Artifact | Description |
|----------|-------------|
| `final_operations_playbook.md` | The daily/weekly operating procedure the person runs |
| `job_definition.md` | One-page description of the job — what it is, who it serves, what it delivers |
| `launch_checklist.md` | 30-day artifact checklist with completion status |

---

## Phase Gate Conditions

Each gate must be cleared before the next phase begins. A gate failing does not mean failure — see `10_contingency_matrix.md`.

| Gate | Condition | Failure Action |
|------|-----------|----------------|
| **After Phase 1** | `intake_form.json` exists and all required fields are non-null | Re-run INTAKE_AGENT with gap-filling prompt |
| **After Phase 2 scanners** | At least 4 of 5 opportunity files exist and each contains ≥ 1 opportunity | Re-run missing scanner with relaxed constraints |
| **After OPPORTUNITY_SCORER** | At least 3 scored opportunities, top score ≥ 55/100 | Expand scanner scope, re-run scorer |
| **After Phase 3 (human gate)** | `chosen_job.json` exists and all required fields populated | Human must complete — no automated fallback |
| **After Phase 4** | All three artifact files exist (technical_setup.md, gtm_plan.md, content_plan.md) | Re-run missing agent |
| **After Phase 5** | `final_operations_playbook.md` exists and Day 1 task is specific and executable | Re-run OPERATIONS_AGENT with specificity prompt |

---

## Agent Invocation Format

All agents in this flow are Claude Code agents. Invoke them using this pattern:

```bash
claude --agent-type general-purpose \
  --context intake_form.json \
  --context persona_profile.json \
  --prompt-file 06_job_architecture.md \
  --output technical_setup.md
```

Or in Claude Code interactively, paste the agent role and prompt from the relevant document, attach the listed context files, and request the output artifact by name.

**Context files to pass at each phase:**

Phase 1: none (INTAKE_AGENT interviews the human directly)
Phase 2 scanners: `intake_form.json`
Phase 2 persona: `intake_form.json`
Phase 2 scorer: `intake_form.json` + all 5 opportunity files + `persona_profile.json`
Phase 3: all Phase 2 outputs
Phase 4: `chosen_job.json` + `intake_form.json` + `persona_profile.json`
Phase 5: `chosen_job.json` + `intake_form.json` + `technical_setup.md` + `gtm_plan.md` + `content_plan.md`

---

## Failure Handling

- If any gate fails, reference `10_contingency_matrix.md` for the relevant failure mode
- Retry policy: 2 retries with modified prompts before human escalation
- No automated retry for Phase 3 — the human must make a decision
- CONTINGENCY_AGENT is not a phase — it is a reference document that gets invoked when KPIs signal a problem

---

## Document Index

| Document | Phase | Agent(s) |
|----------|-------|---------|
| `01_discovery_intake.md` | 1 | INTAKE_AGENT |
| `02_market_scanner.md` | 2 | FREELANCE_SCANNER, SAAS_SCANNER, CONSULTING_SCANNER, CONTENT_SCANNER, HYBRID_SCANNER |
| `03_persona_builder.md` | 2 | PERSONA_BUILDER_AGENT |
| `04_opportunity_scorer.md` | 2 | OPPORTUNITY_SCORER_AGENT |
| `05_convergence_gate.md` | 3 | CONVERGENCE_AGENT + human |
| `06_job_architecture.md` | 4 | ARCHITECTURE_AGENT |
| `07_go_to_market.md` | 4 | GTM_AGENT |
| `08_content_engine.md` | 4 | CONTENT_AGENT |
| `09_operations_playbook.md` | 5 | OPERATIONS_AGENT |
| `10_contingency_matrix.md` | passive | CONTINGENCY_AGENT |
| `11_30_day_launch_plan.md` | execution | human (with agent support) |

---

## Definition of Done

The job is **built** when all of the following are true:

1. `chosen_job.json` exists and the person has committed to it
2. `final_operations_playbook.md` exists and the person has read it
3. The person has sent at least 5 personalized outreach messages
4. At least one person has responded with interest
5. The person knows exactly what to do tomorrow morning

The job is **running** when: at least $1 of real money has been received from a real person for the chosen activity.
