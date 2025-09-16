# Echo Context: Why, Who, What, How

## Why (problem, outcomes, guardrails)

* **Problem:** 
    1. Frontline-heavy organizations struggle to detect and act on psychosocial risks early. Traditional surveys are slow, brittle, and ignored; incidents and regulator pressure arrive faster than insights.
    2. Frontline-heavy organizations struggle to obtain meaningful engagement data from "deskless" employees, inhibiting the organisations abiltiy to predict attrition, intrerpersonal conflict or poor management.   
* **Outcome goals:**

  1. Reach frontline staff reliably with minimal friction
  2. Surface early, explainable risk and engagement signals aligned to ISO 45003 domains
  3. Trigger and track timely, micro-intercentions or local actions by supervisors
  4. Produce board-ready evidence of due diligence and improvement
* **Non-goals:** Echo is not therapy, surveillance, productivity tracking, or a disciplinary tool. No manager gets raw recordings; individual content is private except for pre-agreed critical exceptions.

## Who (users, buyers, stakeholders)

* **Primary users:**

  * Frontline workers (voice or WhatsApp check-ins)
  * Frontline supervisors, HSE specialists (cohort heatmaps, short action lists)
  * Risk sub-comittee of the board
* **Secondary stakeholders:** People & Culture, Operations leadership, Exec/Board, EAP/critical-incident partners.
* **Economic buyer/champions:** COO/Head of Operations, CHRO/Head of Safety, Founder/CEO in mid-size orgs.
* **Environments:** Shift-based, distributed, high-load roles (e.g., field services, logistics, healthcare, funerals, mining).

## What (product scope and artifacts)

* **Core capability:** 90-second, no-app check-ins by phone or WhatsApp, weekly cadence by default; optional micro-pulses on high-risk weeks.
* **Risk domains (ISO 45003 aligned):** Workload and job demands, fatigue/sleep, exposure to traumatic events, role clarity/role conflict, support/civility/harassment, remote/after-hours pressures.
* **Supervisor outputs:**

  * Cohort heatmaps and trend lines
  * Weekly “act now” list with simple playbooks
  * Time-to-intervention tracking and closure SLAs
* **Worker experience:** Human, plain-language calls; can reschedule or opt out any time; receives private guidance and “you said, we did” follow-ups.
* **Exceptions policy:** Named-by-exception alerts only for pre-agreed critical risks (e.g., self-harm intent, violence threats, intoxication on duty, critical fatigue). All exception paths are transparent to the worker.
* **Reporting artifacts:**

  * Weekly pilot KPIs (coverage, signals, actions)
  * ISO 45003-aligned evidence pack for execs/boards
  * Audit trail: actions taken, response times, exception handling
* **Privacy-by-design defaults (pilot-ready):** Cohort-level analytics to supervisors; individual content private; minimal data (name, mobile, team/site, manager, roster windows, optional incident/absence feed); encryption in transit/at rest; access logging; default retention 12 months (configurable).

## How (approach, architecture, operating model)

* **Operating loop:** Reach → Understand → Act → Prove.

  * Reach: schedule-aware calling windows; WhatsApp/SMS fallback
  * Understand: short dynamic dialogue mapped to hazards; explainability attached to each flag
  * Act: supervisor playbooks and SLAs; lightweight action logging
  * Prove: weekly KPIs; “you said, we did” receipts; board evidence pack
* **High-level architecture (conceptual):**

  1. **Channels:** Telephony + WhatsApp; SMS fallback
  2. **Orchestration:** Consent, scheduling, prompt selection, language/tone variants
  3. **Risk engine:** Domain scoring, confidence, false-positive controls, exception detection
  4. **Action engine:** Assignments, nudges, SLA timers, receipts
  5. **Privacy & access:** Role-based views, cohort aggregation, exception gates
  6. **Reporting:** Dashboards, weekly KPI notes, exportable evidence pack
* **Pilot trial pattern (typical):** \~30 participants, weekly for 8 weeks, with a control group and an explicit robustness subgroup that “stress-tests” the system by consent to validate false-positive handling and comms clarity.
* **Success metrics (canonical):**

  * Coverage: ≥60% weekly active in treatment
  * Signal quality: actionable flags with controlled false-positive rate
  * Actioning: median time-to-intervention within SLA; % actions closed per week
  * Risk movement: directional improvement on targeted domains
  * Trust: positive worker sentiment on usefulness and boundaries

## Constraints, assumptions, risks

* **Constraints:** No worker app; low bandwidth tolerant; manager time is scarce; safety/legal review required before named-by-exception alerts.
* **Assumptions:** Workers will engage when calls are short, human, and lead to visible fixes; supervisors will act if actions are concrete and tracked.
* **Key risks:** Low pickup, supervisor inaction, exception mishandling; mitigated by timing, playbooks+SLAs, and transparent exception flows.

## Definitions (canonical terms for derivative docs)

* **Cohort-level analytics:** Aggregated signals at team/site level; individual content not visible to managers.
* **Named-by-exception:** Pre-agreed, tightly scoped conditions under which an individual alert is escalated.
* **Micro-pulse:** 1–3 item follow-up used sparingly in high-risk weeks.
* **Evidence pack:** Exportable, ISO 45003-aligned snapshot of participation, risk trends, actions, and exception audits.

## Filing cabinet (standard outputs other docs can reference)

* Pilot Charter, PIA/DPIA (short form), Privacy Profile, Exceptions SOP, Supervisor Playbook, Weekly KPI Template, Evidence Pack Template, Data Schema & Flow, Security Overview.

Use this as the single source of truth for Echo docs, briefs, and PRDs. If a proposed feature conflicts with these boundaries, either update this context first or reject the feature.
