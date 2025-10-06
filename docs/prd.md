# Echo Pilot MVP — Product Requirements Document (PRD)

**Doc owner:** Fletcher (Echo)
**Version:** v0.1 (draft)
**Pilot size:** 20 participants
**Pilot duration:** up to 12 weeks (1st evidence pack produced within 90 days)
**Environments:** Production‑like pilot only (single tenant)

---

## 1) Purpose & Outcomes

**Pilot purpose**

Stand up a small, ethical pilot to test whether Echo can:

1. Engage in meaningful voice conversations with frontline workers
2. Measurably surface psychosocial risk signals
3. Provide near real‑time engagement signals
4. Produce an ISO‑45003‑ready evidence pack in 90 days

**Pilot outcome**

A working, end‑to‑end system across three loops:

- **Capture loop:** ~90‑second voice check‑ins captured reliably with consent.
- **Triage loop:**  Explainable tagging + simple risk scoring and next‑best actions for a supervisor.
- **Evidence loop:** Crew‑level dashboards and a board‑ready ISO‑45003 evidence pack.

---

## 2) Success Criteria (Pilot KPIs)

- **Participation:** ≥60% weekly participation among active participants.
- **Signal quality:** ≥80% agreement between human review and automated tags on a 20‑call gold set.
- **Time‑to‑acknowledgement:** Median ≤48h from risk creation to first supervisor acknowledgement for medium/high items.
- **Evidence completeness:** Quarterly pack contains participation trend, risk trend, top hazards, actions taken, and audit trail with no PII leaks.
- **Trust:** Zero unresolved privacy incidents; ≥80% pilot satisfaction (workers and supervisors) in exit survey.

---

## 3) In‑Scope / Out‑of‑Scope

**In scope (v0.1):**

- First‑time consent and brief check‑ins by phone (Bland.ai). supporting interactions via WhatsApp (2Chat) or SMS (ClickSend)
    - Schedule & reschedule via Calendly and Google calendar
- Deterministic tagger (rule‑based) and 0–3 risk score
    - LLM based summary and interp.
- Summary dashboard: Aggregated call metrics, risk score, trend, tags
    - Acknowledgement Queue for supervisors (web UI) with timestamped notes (action or resolution)
    - Weekly metrics and ISO‑45003 evidence pack export (HTML/PDF)
- Per‑tenant config, pseudonymous IDs, named‑by‑exception red‑flag handling

**Out of scope (v0.1):**

- Therapy or clinical advice; Echo only signposts and transfers on red flags
- Heavy integrations (HRIS/SSO); CSV in and HTML/PDF/CSV out only
- Multilingual; English only
- Advanced ML personalization; rules first

---

## 4) Users & Roles

- **Worker (participant):** Receives calls/WhatsApp/SMS, provides consent, answers 1–2 questions, can opt out.
- **Supervisor:** Sees Action Queue (pseudonymous by default), performs and records actions.
- **Pilot Admin (Echo):** Manages onboarding, config, dashboards, exports, data quality.

**Permissions**

- Workers: none beyond their own communications
- Supervisors: Action Queue, cohort metrics; no raw transcripts by default
- Admin: full pilot data access; exports; privacy/audit controls

---

## 5) Assumptions & Constraints

- Cohort fixed at ~20 participants; Region: Australia (three time zones)
- Phone numbers and WhatsApp opt‑in available; workers can receive calls during agreed windows
- Domain echo‑control.com hosted via Squarespace; app front‑end (dashboard, config) hosted on Vercel
- Orchestration via **Zapier Pro**; storage in **Supabase** (RLS on), limited **Zapier Tables** for light lookups
- **Bland.ai** Pathways for call flows; **2Chat** for WhatsApp; **OpenAI** for tagging; **ElevenLabs** optional voice selection

---

## 6) Functional Requirements

### 6.1 Onboarding & Consent

- **FR‑ONB‑1**: Tally form captures participant details, consent preference, preferred call window, language notes, site, crew, role.
    - Alternatively, BARE provides site, crew, role.
    - User could provide via phone call if preferred. initial SMS/Whatsapp link to Form / call.
- **FR‑ONB‑2**: Zap creates participant in Supabase and Zapier Tables with pseudonymous `worker_id`, stores consent record (source, timestamp, text snapshot).
- **FR‑ONB‑3**: Welcome WhatsApp via 2Chat with plain‑English privacy summary and opt‑out instructions.

### 6.2 Scheduling

**Scope**

- In-scope: booking, rescheduling, cancelling via Calendly; webhooks to Zapier; downstream reminders and calls; audit and idempotency.
- Out-of-scope: drag-to-move edits in Google/Outlook; arbitrary ICS edits; multi-host routing; custom workflow engine.

**Core Principles**

- Calendly is the only mutable schedule.
- All time changes flow from Calendly webhooks.
- Idempotent runs.
- Human-visible rescheduling = Calendly link in every message.

**Actors**

- End user (invitee).
- Admin/agent (optional).
- Calendly (API + webhooks).
- Zapier (flows).
- WhatsApp provider (2chat).
- Bland.ai (outbound call).
- Internal Store (DB/Sheets).

**Weekly**

- **FR‑SCH‑1**: Weekly call schedule per participant within chosen window; one retry if no answer.

### **6.2.1 Booking**

- FR-B1: System creates a Calendly invite for a user via API or shares a host link.
- FR-B2: On booking, Calendly sends `invitee.created` webhook with start time, timezone, invitee identifiers, and event UUID.
- FR-B3: Zapier receives webhook and:
    - Stores or updates a `Job` record (`job_id`, `calendly_event_uuid`, `start_at`, `tz`, `user_id`, `status=scheduled`).
    - Schedules reminder messages (relative offsets).
    - Writes an audit entry.
- **FR‑SCH‑2**: If 2 failed attempts, send WhatsApp fallback mini‑check‑in; record non‑response.

### **6.2.2 Reschedule**

- FR-R1: User reschedules only via Calendly’s reschedule UX or link.
- FR-R2: On reschedule, Calendly emits `invitee.rescheduled` with new time and same `event_uuid` (or new invitee UUID plus old reference, per Calendly semantics).
- FR-R3: Zapier updates `Job.start_at`, clears prior reminders, re-schedules new ones, updates audit.

### **6.2.3 Cancel**

- FR-C1: User cancels via Calendly cancel flow.
- FR-C2: Calendly emits `invitee.canceled`.
- FR-C3: Zapier sets `Job.status=canceled`, cancels reminders and the call, and sends a confirmation WhatsApp.

### **6.2.4 Reminders and Messaging**

- FR-M1: System supports N reminder offsets per job (e.g., T-24h, T-1h, T-10m).
- FR-M2: Each outbound message includes:
    - Calendly reschedule link
    - STOP/PAUSE commands
- FR-M3: STOP sets `Job.status=paused`. PAUSE accepts durations (e.g., `PAUSE 14d`) and clears timers.

### **6.2.5 Call Flow Execution**

- FR-X1: At `start_at` minus configured lead (e.g., 0–2 min), Zapier triggers Bland.ai with `user_id`, script id, and metadata.
- FR-X2: If call fails, retry policy applies (e.g., 3 attempts with backoff).
- FR-X3: On success/failure, write an execution log with idempotency key.

**Data Model (minimum)**

- **Job**: `job_id`, `user_id`, `calendly_event_uuid`, `calendly_invitee_uuid`, `start_at` (RFC3339), `tz` (IANA), `status` (scheduled|rescheduled|canceled|paused|completed), `version`, `created_at`, `updated_at`.
- **Execution**: `exec_id`, `job_id`, `scheduled_for`, `status`, `attempts`, `error`, `idempotency_key`, `created_at`.
- **Audit**: `audit_id`, `job_id`, `source` (webhook|admin|user_cmd), `action` (create|reschedule|cancel|pause|resume), `payload_snapshot`, `at`.

**Idempotency and Ordering**

- FR-I1: Derive `idempotency_key` from `(calendly_event_uuid, webhook_occurred_at)` or Calendly’s delivery id.
- FR-I2: Ignore duplicate webhooks.
- FR-I3: If out-of-order webhooks arrive, last-writer-wins using Calendly `updated_at`.

**Time Zones and DST**

- FR-T1: Persist user’s IANA time zone from Calendly; do not convert to floating local time.
- FR-T2: All reminders compute off `start_at` in that TZ.
- FR-T3: Daylight changes are Calendly’s problem; we mirror what Calendly sends.

**Permissions and Links**

- FR-P1: All user-facing messages include the Calendly reschedule URL.
- FR-P2: Admin can send a one-time booking link.
- FR-P3: No editable Google/Outlook events from us. Calendly handles invites.

 **Admin Ops**

- FR-A1: Bulk pause/resume by cohort.
- FR-A2: Search by `user_id`, `event_uuid`, phone.
- FR-A3: Manual fire: trigger next reminder or call once, idempotent.

**Observability**

- NFR-O1: Metrics: webhooks received, deduped, jobs scheduled, calls started/succeeded/failed, reminder send rate, error classes.
- NFR-O2: Tracing: correlation id from webhook through Zap run into provider calls.
- NFR-O3: Dashboards + alerts for failure spikes and schedule drift.

### 6.2.6 External Interfaces

 **Calendly**

- Webhooks: `invitee.created`, `invitee.rescheduled`, `invitee.canceled`.
- API: read event, get reschedule link, fetch invitee and event metadata.
- Required fields to persist: `event_uuid`, `invitee_uuid`, `start_time`, `end_time`, `timezone`, `reschedule_url`, `cancellation_url`, `tracking fields`.

**Zapier**

- Trigger: Catch Hook (Calendly → Zapier).
- Steps:
    1. Deduplicate by `event_uuid` + webhook id.
    2. Upsert Job.
    3. Schedule reminders (Zapier Delay/Queues or external queue).
    4. Send WhatsApp via 2chat.
    5. Trigger Bland.ai at execution time.
    6. Write logs.

**Messaging and Voice**

- 2chat: templated WhatsApp with variables `{user_name}`, `{when_local}`, `{reschedule_url}`.
- Bland.ai: call job with script id, phone, `job_id`, idempotency key.

### **6.2.7 UX Rules**

- Every message includes: time in user’s local TZ, reschedule link, STOP/PAUSE help.
- If user replies with `RESCHEDULE`, return Calendly link. Do not accept free-text times.
- If user tries to move an event in their calendar app, the source of truth remains Calendly; message instructs them to use the link.

### **6.2.8 Error Handling**

- Calendly outage: queue webhooks; retry with backoff.
- Zap run failure: push to DLQ; alert; do not duplicate calls on replay.
- Bland.ai failure: retry policy, then notify user with link to reschedule or request a new slot.
- Late webhook (> scheduled time): if within grace window (e.g., 5 min), proceed; else skip and notify with reschedule link.

### **6.2.9 Acceptance Criteria**

- AC-1: Booking via Calendly triggers creation of `Job` and schedules reminders.
- AC-2: Reschedule in Calendly updates `start_at` and re-schedules reminders within ≤ 10 s.
- AC-3: Cancel in Calendly stops reminders and calls within ≤ 10 s.
- AC-4: Outbound messages contain correct local time and a working reschedule link.
- AC-5: Idempotent handling of duplicate webhooks verified by test suite.
- AC-6: p95 end-to-end delay (webhook→WhatsApp send) ≤ 2 s in steady state.

### **6.2.10 Test Cases (sampling)**

- T1: Create booking → verify Job upsert, reminders set, WhatsApp preview correct.
- T2: Reschedule twice in 60 s → only latest time remains, one reminder schedule active.
- T3: Cancel after reminders started → future reminders and call suppressed.
- T4: Duplicate webhook delivery → no duplicate Job entries or messages.
- T5: Bland.ai 500 error → 3 retries with backoff, then user notified.
- T6: Time zone with DST boundary → correct local rendering before and after shift.

### **6.2.11 Admin and Bulk Ops**

- Pause/resume by tag or cohort.
- Rebuild schedules for a cohort (e.g., change reminder offsets).
- Export audit and execution logs by date range.

### **6.2.12 Notes and Constraints**

- Calendly dictates the contract: if users want drag-to-move inside their calendar, this architecture will not reflect it. They must use the Calendly reschedule UX.
- For Apple-only users without OAuth, Calendly still works via email + ICS.

If you want, I can supply Zapier step definitions and the exact Calendly payload mappings next.

### 6.3 Call Execution (Bland Pathways)

- **FR‑CALL‑1**: First‑time script: identity + privacy + consent; abort if declined.
- **FR‑CALL‑2**: Two questions + follow up or end: micro‑pulse and one hazard probe parameterized by role/shift.
- **FR‑CALL‑3**: Red‑flag detection keywords route to transfer step (EAP/hotline) and stop recording after transfer.
- **FR‑CALL‑4**: Store audio URL, transcript, call metrics (duration, attempts).

### 6.4 WhatsApp Mini‑Check‑in (2Chat)

- **FR‑WSP‑1**: Short template with 1–2 quick‑reply buttons; capture responses; store as a call equivalent.

### 6.5 Triage & Tagging

- **FR‑TAG‑1**: Deterministic phrase/regex mapper to 10 hazard tags: workload, fatigue, sleep, role_clarity, interpersonal, respect, change, remote_isolation, equipment, environment.
- **FR‑TAG‑2**: Risk score 0–3 with simple weights for co‑occurring tags and repeat negatives in 14 days.
- **FR‑TAG‑3**: Next‑best action suggestion: none, supervisor_nudge, playbook_step, escalate.

### 6.6 Acknowledge  Queue

- **FR‑ACT‑1**: Supervisor sees queued items with tag chips, risk, suggested action, and “Mark done” or “Send nudge.”
- **FR‑ACT‑2**: When done, record action, timestamp, optional note.
- **FR‑ACT‑3**: Track time‑to‑first‑action for every medium/high item.

### 6.7 Evidence & Reporting

- **FR‑EV‑1**: Dashboard tiles: Participation by week, Risk trend, Top hazards, Median time‑to‑action.
- **FR‑EV‑2**: Export evidence pack (HTML/PDF) with methodology, cohort heatmap, trends, actions, audit.
- **FR‑EV‑3**: Weekly summary email to pilot stakeholders.

### 6.8 Privacy & Opt‑out

- **FR‑PRV‑1**: “Named by exception” only on red‑flag pathways; default cohort‑level aggregation otherwise.
- **FR‑PRV‑2**: STOP/opt‑out via WhatsApp or verbal decline; cease scheduling; log audit.

---

## 7) Non‑Functional Requirements

- **Reliability:** ≥95% successful completion of scheduled contacts per week across the cohort.
- **Latency:** Tagging and Action Queue update within 2 minutes of call end; evidence tiles update hourly.
- **Security:** Supabase RLS; encryption at rest; HTTPS only; audit logs for admin actions.
- **Privacy:** No raw transcripts to supervisors by default; PII minimization; retention policy set for pilot.
- **Cost guardrails:** Unit economics tracked per call and per analysis run.

---

## 8) End‑to‑End Flow (Text Diagram)

1. **Tally form** → Zap → create `participant` in **Supabase**; consent logged; WhatsApp welcome via **2Chat**.
2. **Scheduler Zap** creates **Bland.ai** call tasks for each participant in window.
3. **Bland Pathway** runs: consent → micro‑pulse → hazard probe → close; red‑flag transfers to EAP.
4. **Bland webhook** → Zap: store audio+transcript → run **OpenAI** tagging → compute risk → write `analysis`.
5. If medium/high: create **Action Queue** item for supervisor; send optional email/WhatsApp notification.
6. Supervisor marks action done; timestamps logged.
7. **Dashboard** (Vercel) queries Supabase (RLS) for tiles and heatmaps.
8. **Evidence export** generated on demand or weekly; HTML/PDF stored and shareable.
9. Opt‑out honored at any step; scheduling halted.

---

## 9) Data Model (Supabase)

**participants**

- worker_id (uuid, pk), phone, whatsapp_id, role, site, crew, timezone, privacy_profile, consent_status, consent_source, consent_at, call_window

**supervisors**

- supervisor_id, name, email, phone, cohort_keys[], permissions

**calls**

- call_id, worker_id, scheduled_at, started_at, ended_at, channel (phone|whatsapp), status (completed|no_answer|declined|escalated), attempt_count

**call_artifacts**

- call_id (fk), audio_url, transcript_text, transcript_confidence

**analysis**

- call_id (fk), hazard_tags[], iso_refs[], risk_score (0–3), action_suggested, cohort_key, escalated (bool)

**actions**

- action_id, call_id, supervisor_id, action_type, status (open|done), created_at, first_action_at, closed_at, note

**metrics_weekly**

- week_start, cohort_key, participation_rate, median_time_to_action, top_hazards[], risk_index

**configs**

- tenant_id, eap_number, red_flag_rules, risk_weights, evidence_pack_template_version

**consents**

- worker_id, text_snapshot, source, captured_at, revoked_at

**RLS policies**

- Supervisors: restrict by cohort_key; Admin: full access; Workers: none.

---

## 10) Risk Rules (v0.1)

- Base: 0
- +1 fatigue or sleep tag
- +1 interpersonal or respect tag
- +1 repeat negative sentiment in past 14 days
- Escalate if any of: explicit self‑harm terms; harassment with threat language; “unsafe to work now” phrase.

---

## 11) Bland.ai Pathways (v0.1)

**Nodes**

1. Intro & consent (decline branch → thanks + end)
2. Micro‑pulse (3‑way: smashing it | middling | counting minutes)
3. Hazard probe (param by role/shift): fatigue, workload, interpersonal etc.
4. Close‑the‑loop + next check‑in
5. Red‑flag transfer (conditional) → stop recording; log outcome

**Per‑node variables passed from Zapier**

- Agent tone, cohort/site tokens, hazard probe text, privacy line, next check‑in time, transfer number.

---

## 12) Zaps (minimum set)

1. **Onboard Participant:** Tally → Supabase insert → 2Chat welcome
2. **Weekly Scheduler:** Cron weekly → create Bland call tasks (respect windows) → write `calls`
3. **Call Webhook Handler:** Bland → Supabase artifacts → OpenAI tagger → compute risk → write `analysis` and Action item
4. **Action Completion:** Supervisor UI webhook → update `actions` → recompute metrics
5. **Evidence Build:** Weekly cron → refresh `metrics_weekly` → render export → notify stakeholders
6. **Opt‑out Handler:** WhatsApp STOP or decline → update consent → cancel future calls
7. **Error Alerts:** Any Zap failure → email Ops

---

## 13) Front‑end (Vercel)

- **Action Queue:** Table of items with filters (risk, tag, cohort), detail drawer, mark done, send nudge.
- **Dashboard:** Four tiles + cohort heatmap; links to audit views.
- **Evidence Export:** Server route renders snapshot HTML → downloadable PDF.

---

## 14) Privacy, Security, Compliance

- **Pseudonymization:** worker_id primary key; names not used in UI. Named by exception only on red flags.
- **Data minimization:** Store transcripts for pilot analysis; redact PII if present.
- **Retention:** Default 120 days from collection or 30 days post‑pilot, whichever is sooner; deletions honored on request.
- **Audit:** All admin reads/exports logged. Consent record immutable.
- **ISO‑45003 mapping in pack:** participation, hazards, controls/actions, and governance evidence.

---

## 15) Testing & QA

- **Golden set:** 20 hand‑crafted transcripts for tagger accuracy checks.
- **Dry runs:** 5 internal calls across all branches (consent decline, red flag, WhatsApp fallback).
- **Load:** Simulate burst of 20 calls in 30 minutes; verify latency budgets.
- **Privacy drills:** Opt‑out, data export, and delete‑on‑request.

---

## 16) Rollout Plan

- Week 0: Config, onboarding pack, supervisor briefing; dry runs
- Week 1–2: Start weekly cadence; validate Action Queue use; fix early friction
- Week 3–8: Stable operations; weekly evidence refresh; light tuning only
- Week 9–12: Compile 90‑day evidence pack; pilot review; go/no‑go for expansion

---

## 17) Risks & Mitigations

- **Low pickup rate:** Pre‑notify windows; WhatsApp fallback; keep calls under 90s
- **Over‑flagging noise:** Conservative rules; quick human spot‑checks; hide low‑value tags from queue
- **Privacy concerns:** Clear privacy summary, opt‑out, aggregated views by default
- **Technical brittleness:** Keep Zaps small and observable; retries; alerting

---

## 18) Open Questions

- Supervisor roster finalization and cohort mapping?
- EAP/transfer numbers and hours?
- Evidence pack branding preferences and approver?

---

## 19) Appendices

**A) Tagger Prompt (OpenAI, v0.1)**

- System: "Extract hazard tags from transcript; be conservative; output JSON only."
- Output schema: `{"hazard_tags":[], "iso_refs":[], "sentiment":"pos|neu|neg"}`

**B) Cost & Rate Estimates (order‑of‑magnitude)**

- Calls: 20 users × ~8–10 calls each ≈ 160–200 calls
- OpenAI tagging: 200 runs; ensure context under 3k tokens per call
- Storage: transcripts + artifacts < 1 GB

**C) Evidence Pack Sections**

- Context & method; Participation trend; Risk trend; Top hazards; Actions log; Governance & privacy notes; Next steps.