# Echo Pilot Charter & Trial Plan
## Bare Funeral Services - Psychosocial Risk Detection Pilot

**Document Version:** 1.0  
**Date:** September 2025 
**Pilot Period:** 12 weeks (16 Oct - 16 Dec 2025)  
**Status:** Draft for Approval

---

## Executive Summary

This pilot will test Echo's ability to reach frontline funeral workers reliably, surface early psychosocial risk signals aligned to ISO 45003, trigger timely supervisor interventions, and produce board-ready evidence of due diligence. The trial includes ~40 participants across treatment, control, and robustness testing arms to validate both effectiveness and system resilience.

---

## 1. Pilot Objectives & Success Criteria

### Primary Objectives
1. **Reach:** Demonstrate reliable engagement with frontline staff through 90-second phone/WhatsApp check-ins
2. **Understand:** Surface early, explainable psychosocial risk signals aligned to ISO 45003 domains
3. **Act:** Trigger and track timely micro-interventions by supervisors with measurable outcomes
4. **Prove:** Produce board-ready evidence of due diligence and improvement

### Success Metrics (Minimum Viable Thresholds)
- **Coverage:** ≥60% weekly active participation in treatment arm
- **Signal Quality:** Actionable risk flags with controlled false-positive rate (<10%)
- **Actioning:** Median time-to-intervention within 48-hour SLA; ≥80% actions closed per week
- **Risk Movement:** Directional improvement on targeted ISO 45003 domains
- **Trust:** Positive worker sentiment on usefulness and boundaries (≥70% favorable)

### Board-Ready Outcomes
- ISO 45003-aligned evidence pack demonstrating participation, risk trends, and interventions
- Audit trail of actions taken, response times, and exception handling
- Recommendation for scaling to full workforce (~200 employees)

---

## 2. Trial Design & Population

### Target Population
**Total:** ~30 frontline workers from Bare Funeral Services  
**Teams:** Funeral directors, arrangers, transfer team, call-center schedulers  
**Selection Criteria:** Workers in shift-based, high-load roles experiencing psychosocial pressures

### Trial Arms

#### Arm A: Treatment Group (n≈18)
- **Experience:** Full Echo weekly check-ins + supervisor cohort dashboards
- **Supervisors:** 2-3 frontline supervisors receive heatmaps and action lists
- **Data:** Individual guidance private; cohort-level analytics only

#### Arm B: Control Group (n≈9)
- **Experience:** Business-as-usual, no Echo intervention
- **Measurement:** Existing incident/absence data and baseline surveys
- **Purpose:** Establish counterfactual for risk movement analysis

#### Arm C: Robustness Subgroup (n≈6)
- **Composition:** Volunteers drawn from both Arms A and B
- **Purpose:** Stress-test system through gaming prompts, inconsistent answers, escalation attempts
- **Protection:** Tagged in backend, never flagged to management; no performance consequences
- **Validation:** False-positive rate containment and system resilience

### Randomization & Ethics
- **Method:** Stratified random assignment by team and role
- **Consent:** All participants provide explicit opt-in consent
- **Transparency:** Red-team participation disclosed in pilot information
- **Union Consultation:** Worker representative consulted on design and consent

---

## 3. Scope & Boundaries

### What Echo Will Do
- **Core Capability:** 90-second phone/WhatsApp check-ins, weekly cadence
- **Risk Domains:** Workload/job demands, fatigue/sleep, traumatic events, role clarity, support/civility, after-hours pressures
- **Supervisor Outputs:** Cohort heatmaps, weekly action lists, time-to-intervention tracking
- **Worker Experience:** Human, plain-language calls; reschedule/opt-out anytime; private guidance
- **Reporting:** Weekly KPIs, ISO 45003 evidence pack, audit trails

### What Echo Will NOT Do
- **Therapy or counseling:** Echo is not a therapeutic intervention
- **Surveillance:** No productivity tracking or disciplinary use
- **Individual exposure:** No raw recordings to managers; individual content private
- **Medical data:** No health information collection beyond fatigue/sleep patterns

### Named-by-Exception Policy
**Pre-agreed escalation triggers only:**
- Self-harm intent or threats
- Violence threats toward others
- Intoxication on duty
- Critical fatigue affecting safety

**All exception paths:**
- Transparent to the worker
- Logged and auditable
- Pre-agreed response protocols

---

## 4. Privacy & Data Governance

### Privacy-by-Design Profile
- **Identity Visibility:** Cohort-level analytics only; individual content private
- **Data Minimization:** Name, mobile, team/site, manager, roster windows, optional incident/absence feed
- **Retention:** 12 months default (configurable)
- **Security:** Encryption in transit/at rest, access logging, data residency compliance
- **Rights:** "What Echo stores about me" view, opt-out anytime, data export on request

### Data Processing Agreement
- **Legal Basis:** Legitimate interest in workplace safety and duty of care
- **Purpose Limitation:** Psychosocial risk detection and intervention only
- **Cross-border:** Data residency as required by local regulations
- **Sub-processors:** Limited to telephony/WhatsApp providers
- **Audit Rights:** Bare retains right to audit data handling and access

---

## 5. Technical Implementation

### Channels & Infrastructure
- **Primary:** Outbound telephony with human-like AI agent
- **Secondary:** WhatsApp integration for scheduling and follow-up
- **Fallback:** SMS for critical communications
- **No App Required:** Zero friction for frontline workers

### Data Architecture
- **Orchestration:** Consent management, scheduling, prompt selection, tone variants
- **Risk Engine:** Domain scoring, confidence levels, false-positive controls
- **Action Engine:** Assignment routing, SLA timers, receipt generation
- **Privacy Layer:** Role-based access, cohort aggregation, exception gates
- **Reporting:** Real-time dashboards, weekly KPI generation, evidence pack export

### Security & Compliance
- **Encryption:** End-to-end for all communications and data storage
- **Access Controls:** Role-based permissions with audit logging
- **Data Residency:** Configurable based on Bare's requirements
- **Breach Notification:** 24-hour notification protocol

---

## 6. Content & Operations

### Agent Design
- **Tone:** Human, brief, respectful; never corporate or clinical
- **Variants:** Calm/banter styles adapted to individual preferences
- **Language:** Plain English, industry-appropriate terminology
- **Timing:** Pre-shift/smoko windows for optimal engagement

### Hazard Mapping (ISO 45003 Aligned)
- **Workload & Job Demands:** Volume, complexity, time pressure
- **Fatigue & Sleep:** Shift patterns, rest quality, recovery time
- **Traumatic Events:** Exposure frequency, support availability, coping resources
- **Role Clarity & Conflict:** Expectations, boundaries, decision authority
- **Support & Civility:** Manager availability, team dynamics, harassment indicators
- **Remote/After-hours Pressures:** On-call demands, work-life boundaries

### Micro-Psychometrics
- **Approach:** Subtle personality/state items distributed over weeks
- **Purpose:** Improve risk explanations without survey fatigue
- **Privacy:** Individual responses never shared with management

---

## 7. Supervisor Operations

### Training & Playbooks
- **Heatmap Interpretation:** Reading cohort trends, identifying hotspots
- **Action Lists:** Prioritizing interventions, following playbooks
- **Boundaries:** What NOT to do (no witch-hunts, no individual targeting)
- **Logging:** Recording actions taken and outcomes achieved

### Service Level Agreements
- **Time-to-Intervention:** 48-hour maximum for high-priority flags
- **Action Closure:** 80% of actions closed within one week
- **Follow-up:** "You said, we did" receipts to workers
- **Escalation:** Clear protocols for exception handling

### Support Resources
- **EAP Integration:** Pre-established contact protocols
- **Critical Incident:** 24/7 on-call procedures
- **WHS Coordination:** Safety team notification pathways

---

## 8. Communication & Change Management

### Worker Launch Strategy
- **Information Pack:** One-page plain-English explanation
- **Key Messages:** "Not HR, not surveillance, but safety support"
- **Sample Flow:** 90-second call demonstration
- **Trust Building:** Examples of "you said, we did" outcomes

### Manager Briefing
- **Purpose:** Understanding Echo's role in safety management
- **Process:** How to read dashboards and take action
- **Boundaries:** Individual privacy protection and exception protocols
- **Success Metrics:** What good performance looks like

### Ongoing Communication
- **Weekly Updates:** Participation rates, actions taken, trust receipts
- **Mid-point Review:** Cadence and tone adjustments based on feedback
- **Transparency Reports:** Regular "what Echo learned" summaries

---

## 9. Timeline & Milestones

### Pre-Launch (Weeks -3 to 0)
**Week of 22 Sep 2024:**
- [ ] Pilot charter signed and approved
- [ ] Data Processing Agreement executed
- [ ] Privacy Impact Assessment completed

**Week of 29 Sep 2024:**
- [ ] Data feeds and channel setup completed
- [ ] Agent prompt library finalized
- [ ] Supervisor training delivered
- [ ] Communication materials ready

**Week of 6 Oct 2024:**
- [ ] Dry run with 5 internal testers
- [ ] Timing, consent, and escalation protocols validated
- [ ] Final go/no-go decision

### Pilot Execution (Weeks 1-8)
**Week of 13 Oct 2024 - Launch:**
- [ ] Treatment group onboarding
- [ ] First weekly check-ins initiated
- [ ] Supervisor dashboards activated

**Weeks 2-7 - Operations:**
- [ ] Weekly KPI monitoring and reporting
- [ ] Mid-point review and adjustments (Week 4)
- [ ] Exception handling and audit trails
- [ ] Trust receipt generation

**Week of 8 Dec 2024 - Close-out:**
- [ ] Final data collection and analysis
- [ ] Control vs treatment comparison
- [ ] Board-ready evidence pack generation
- [ ] Scale recommendation delivered

---

## 10. Risk Management

### Identified Risks & Mitigations

**Low Participation/Engagement:**
- *Risk:* Workers ignore calls or provide minimal responses
- *Mitigation:* Optimize timing for pre-shift/smoko windows; keep calls to 90 seconds; demonstrate prior fixes

**Trust & Privacy Concerns:**
- *Risk:* Workers perceive surveillance or disciplinary use
- *Mitigation:* Strict cohort-only analytics; crystal-clear consent and boundaries; no raw voice to managers

**Supervisor Inaction:**
- *Risk:* Managers don't act on risk flags or miss SLA targets
- *Mitigation:* Training on playbooks; weekly time-to-intervention reporting; action closure tracking

**System Gaming/False Positives:**
- *Risk:* Red-team or malicious users generate noise
- *Mitigation:* Backend tagging of robustness subgroup; false-positive rate monitoring; prompt adjustment protocols

**Exception Handling Failures:**
- *Risk:* Critical situations mishandled or escalated inappropriately
- *Mitigation:* Pre-agreed escalation protocols; transparent exception paths; audit logging

### Contingency Plans
- **Participation <40%:** Adjust timing, tone, and communication strategy
- **False Positive Rate >15%:** Review prompts and thresholds; adjust risk engine parameters
- **Supervisor SLA Misses:** Escalate to senior management; provide additional training
- **Critical Exception:** Immediate escalation to EAP and WHS; full audit trail

---

## 11. Governance & Decision Gates

### Steering Committee
- **Sponsor:** Bare Founder/CEO
- **Operations Lead:** Head of Operations
- **Safety Lead:** WHS Manager
- **People Lead:** Head of People & Culture
- **Worker Representative:** Union/Employee rep
- **Echo Lead:** Pilot Manager

### Decision Gates
1. **Pre-Launch Gate (6 Oct):** Go/no-go based on dry run results
2. **Mid-Point Gate (Week 4):** Continue/adjust/terminate based on early metrics
3. **Close-Out Gate (8 Dec):** Scale recommendation based on full results

### Success Criteria for Scaling
- All primary success metrics achieved
- No critical privacy or safety incidents
- Positive worker sentiment and trust indicators
- Clear evidence of risk reduction and intervention effectiveness

---

## 12. Deliverables & Artifacts

### Weekly Deliverables
- **KPI Dashboard:** Coverage, signal quality, time-to-intervention metrics
- **Action Summary:** Interventions taken, outcomes achieved, SLA performance
- **Trust Receipts:** "You said, we did" communications to workers
- **Exception Audit:** Any escalations handled and outcomes

### Final Deliverables
- **Close-Out Report:** Comprehensive analysis of pilot results
- **Board Evidence Pack:** ISO 45003-aligned documentation of due diligence
- **Scale Recommendation:** Go/no-go decision with supporting rationale
- **Lessons Learned:** Process improvements and system refinements

### Data & Privacy Deliverables
- **Data Export:** All pilot data provided to Bare in agreed format
- **Deletion Certificate:** Confirmation of data removal from Echo systems
- **Privacy Impact Report:** Assessment of privacy implications and mitigations

---

## 13. Success Definition & Scale Criteria

### Pilot Success (Minimum Viable)
- ≥60% weekly participation in treatment arm
- Actionable risk signals with <10% false positive rate
- 48-hour median time-to-intervention
- ≥80% action closure rate
- Positive worker sentiment on trust and usefulness

### Scale Recommendation Criteria
- All pilot success metrics achieved or exceeded
- Clear evidence of psychosocial risk reduction
- Supervisor adoption and action-taking demonstrated
- No critical privacy, safety, or trust incidents
- Cost-benefit analysis supports full deployment

### Board-Ready Evidence
- ISO 45003 compliance demonstration
- Quantified risk reduction in targeted domains
- Audit trail of interventions and outcomes
- Worker engagement and trust metrics
- Supervisor effectiveness and satisfaction

---

## 14. Appendices

### Appendix A: ISO 45003 Alignment
Detailed mapping of pilot activities to ISO 45003 guidance on psychosocial risk management, including identification, assessment, control, and review processes.

### Appendix B: Privacy Impact Assessment
Comprehensive assessment of data collection, processing, and sharing activities, including risk identification and mitigation strategies.

### Appendix C: Escalation Protocols
Detailed procedures for handling named-by-exception situations, including contact information, response timelines, and audit requirements.

### Appendix D: Technical Specifications
Detailed technical architecture, data flows, security controls, and integration requirements.

### Appendix E: Communication Templates
Sample worker information sheets, supervisor training materials, and ongoing communication templates.

---

**Document Control:**
- **Author:** Echo Pilot Team
- **Reviewers:** Bare Steering Committee
- **Approval:** [Pending]
- **Next Review:** Mid-point gate (Week 4)
- **Distribution:** Steering Committee, Pilot Team, Worker Representative

---

*This charter serves as the single source of truth for pilot objectives, scope, and success criteria. Any proposed changes must be approved by the steering committee and documented in the change control log.*
