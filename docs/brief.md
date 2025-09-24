# Project Brief: Echo

## Introduction
This Project Brief captures the context, goals, and initial scope for Echo, a frontline-focused capability to detect psychosocial risks early and drive timely, trackable interventions while preserving worker privacy. It serves as the foundation for downstream product documentation and delivery.

## Executive Summary
Echo is a no‑app, 90‑second voice/WhatsApp check‑in system for frontline organizations that detects psychosocial risks early and drives timely, trackable micro‑interventions—while preserving worker privacy. It reliably reaches “deskless” staff, surfaces explainable, ISO 45003‑aligned risk signals, prompts supervisors with simple playbooks and SLAs, and produces board‑ready evidence of due diligence and improvement.

- Problem: Frontline orgs can’t detect/act on psychosocial risks fast enough; legacy surveys are slow, brittle, and ignored. Engagement data from deskless staff is sparse, limiting insight into attrition risk, conflict, or poor management.
- Target market: Shift‑based, distributed, high‑load teams in field services, logistics, healthcare, funerals, mining, and similar frontline‑heavy environments.
- Value proposition: High‑coverage reach with minimal friction; explainable risk flags mapped to ISO 45003; supervisor action lists and SLA tracking; privacy‑by‑design with cohort‑level analytics; exportable evidence packs for execs/boards.
- Unique Capabilities: Echo builds a Perceptual Control Theory aligned psychological goal heirarchy for each worker than enables the system to predict how a given worker is likely to react to changes in context, real or simulated. 

## Problem Statement
Frontline-heavy organizations struggle to reliably surface and act on psychosocial risks before they escalate. Current approaches—annual/quarterly surveys and ad hoc incident reporting—are slow, brittle, and often ignored, especially by “deskless” teams. This results in delayed detection of issues like workload strain, fatigue, exposure to traumatic events, and harassment, with downstream consequences across safety, attrition, and regulatory exposure.

- Current state and pain points
  - Low-friction reach to frontline workers is inconsistent; response windows rarely align with shift patterns.
  - Signals are lagging (e.g complaints), non-explainable, and not actionable at the cohort level managers operate in.
  - Supervisors lack simple, time-bound playbooks and tracking to ensure interventions happen.
  - Privacy concerns and unclear exception handling reduce trust and participation.
- Impact (quantified where possible)
  - Increased risk of safety incidents and burnout; higher attrition costs; potential regulator scrutiny.
  - Missed opportunities to prevent issues early due to lack of explainable, reliable signals.
- Why existing solutions fall short
  - Traditional surveys are slow, non-contextual, and poorly suited to deskless environments.
  - Tools don’t map to ISO 45003 risk domains with explainability, nor do they integrate action SLAs.
  - Many solutions erode trust by overexposing individual content to managers.
- Urgency
  - Regulator pressure and board-level expectations are increasing; incidents move faster than insights.
  - Early pilots can produce board-ready due diligence evidence while improving local outcomes.

## Proposed Solution
Echo delivers a human, privacy‑preserving operating loop—Reach → Understand → Act → Prove—optimized for frontline realities:

- Core concept and approach
  - 90‑second, no‑app voice/WhatsApp check‑ins on a weekly cadence, with opt‑in micro‑pulses in high‑risk weeks.
  - Schedule‑aware outreach windows with SMS fallback to maximize coverage among shift‑based teams.
  - Dynamic dialogue mapped to ISO 45003 domains with per‑signal explainability.
  - Supervisor workflow: weekly cohort heatmaps, prioritized “act now” list, lightweight action logging, and SLA timers.
  - Evidence outputs: weekly KPIs and exportable, board‑ready due diligence pack.
- Key differentiators
  - Cohort‑level analytics by default; individual content remains private, with named‑by‑exception alerts only for pre‑agreed critical risks.
  - Explainable risk flags aligned to ISO 45003 domains with false‑positive controls and robustness subgroup validation during pilots.
  - Time‑to‑intervention focus with simple playbooks, nudges, and closure tracking.
- Why this will succeed
  - Reduces friction for deskless workers; aligns to their schedules and channels.
  - Builds trust through transparent exception policy and privacy‑by‑design defaults.
  - Converts signals into timely action and proof, meeting regulator and board expectations.
- High‑level vision
  - Channels: telephony + WhatsApp (SMS fallback).
  - Engines: orchestration (consent, prompts, language/tone), risk scoring, action/SLA management.
  - Governance: role‑based views, access logging, retention defaults configurable; ISO 45003 evidence pack.

## Target Users

### Primary User Segment: Frontline Workers (Deskless Staff)
- Demographic/firmographic profile: Shift-based, distributed roles in field services, logistics, healthcare, funerals, mining; often mobile with limited desktop access, variable bandwidth and devices.
- Behaviors/workflows: On-the-go, minimal time for surveys or apps; prefer quick, human interactions; rely on mobile voice/WhatsApp; respond best within roster-aware windows.
- Needs and pain points: Want to be heard without friction; distrust lengthy/opaque surveys; need privacy and clarity about exceptions; prefer short, plain-language prompts; desire visible “you said, we did” outcomes.
- Goals: Share real context quickly; see local fixes happen; avoid surveillance; maintain control over participation (reschedule/opt-out).

### Secondary User Segment: Frontline Supervisors & HSE Specialists
- Demographic/firmographic profile: Team/site managers and safety leads responsible for local risk and wellbeing outcomes; operate at cohort level with limited time.
- Behaviors/workflows: Monitor multiple teams; triage tasks; respond to SLAs; need explainable signals and simple playbooks; track actions to closure.
- Needs and pain points: Too much noise, not enough explainable, actionable insight; difficult to prove due diligence; lack of time-bound guidance; fragmented tools.
- Goals: Prioritize the right actions this week; meet SLA and compliance expectations; show improvements with evidence; build trust with staff.

## Goals & Success Metrics

### Business Objectives
- Reduce time-to-detection of psychosocial risk signals in pilot cohorts by 50% within 8 weeks.
- Improve actioning: ≥80% of “act now” items closed within SLA each week.
- Demonstrate due diligence: ship ISO 45003-aligned evidence pack to exec/board by week 4.
- Increase participation: achieve ≥60% weekly active coverage among treatment cohorts.

### User Success Metrics
- Worker trust: ≥70% positive sentiment on usefulness/boundaries in post-call micro-pulse.
- Worker friction: median interaction ≤90 seconds; ≥85% report clarity of exception policy.
- Supervisor confidence: ≥75% rate signals as explainable/actionable; <10% false-positive escalation rate.

### Key Performance Indicators (KPIs)
- Coverage: weekly active %, by cohort and segment; target ≥60%.
- Signal quality: actionable flags per 100 interactions; false-positive rate <X% (to be set per pilot).
- Actioning: median time-to-intervention; % actions closed within SLA.
- Risk movement: directional change on targeted ISO 45003 domains MoM.
- Trust & privacy: sentiment score; exception handling audits passed; access logs reviewed.

## MVP Scope

### Core Features (Must Have)
- Channel reach: 90-second voice + WhatsApp check-ins; SMS fallback.
- Roster-aware scheduling: shift windows, reschedule, opt-out.
- Risk signals: ISO 45003 mapping with explainability attached to each flag.
- Supervisor workflow: cohort heatmaps, weekly “act now” list, simple playbooks.
- Action tracking: assignments, SLA timers, closure logging, “you said, we did” receipts.
- Privacy-by-design: cohort-level analytics by default; named-by-exception policy for critical risks.
- Evidence outputs: weekly KPIs and exportable evidence pack.

### Out of Scope for MVP
- Worker mobile app; browser portals for workers.
- Broad HRIS integrations beyond minimal roster/identifier sync.
- Advanced analytics (predictive modeling beyond explainable flags; long-term trends).
- Multi-language NLU beyond core locales identified for pilots.
- Organization-wide, always-on micro-pulse automation.

### MVP Success Criteria
- ≥60% weekly active coverage in treatment groups for 6 of 8 pilot weeks.
- ≥80% “act now” items closed within SLA for 6 of 8 pilot weeks.
- Evidence pack delivered to exec/board by week 4 and week 8.
- Exception handling SOP tested with zero critical incidents; audits pass.

## Post-MVP Vision

### Phase 2 Features
- Supervisor nudges and coaching informed by action outcomes and patterns.
- Robustness controls: adaptive false-positive tuning; confidence calibration dashboards.
- Light HRIS connectors for richer cohorts and site/roster dynamics.
- Multi-language expansion based on pilot locales and feedback.
- Micro‑pulse library for targeted follow-ups by domain/context.

### Long‑term Vision
- “Wellbeing risk OS” for frontline work: anticipate risk spikes from scheduling, incidents, policy changes.
- Simulation sandbox to test “what if” scenarios (rosters, seasonality) using explainable models.
- Organization‑wide governance: retention profiles, enterprise auditability, policy controls.
- Privacy leadership: standard-setting exception transparency and worker control patterns.

### Expansion Opportunities
- Industry‑specific playbooks and certified evidence templates.
- EAP/critical‑incident partner ecosystem with warm handoffs and tracking.
- Research collaborations on psychosocial risk measurement and false‑positive mitigation.
