# Program Sprint Planning

**Date:** July 6, 2026
**Facilitator:** Nicole Greene

---

## Agenda

> Organized by team with their full timeline — no idle gaps.
> Five teams running continuously July 6 – January 5, 2027.
> See `teams.md` for full service ownership. See `services.md` for microservice definitions.

---

## Initiatives 1–6: Automated Claims Processing

**Release Target:** January 5, 2027
**`2:00`** | 👥 Identity & Access, Claims Core, Intelligence & Workflow, Comms & Content, Payments

> **Feature Scope (Initiatives 1–5):** ~446 SP adjusted
> **Quality/Infrastructure Scope (Initiative 6):** ~215 SP adjusted, distributed across all teams
> **Total Program:** ~661 SP adjusted

> **Strategy:** Early phases include infrastructure spike work, testing frameworks, and integration scaffolding (Initiative 6). Teams transition into core feature work as dependencies unblock. Initiative 6 runs in parallel with feature work across all five teams. Zero idle time across the 27-week program.

---

## Team Schedules — Full Timeline

### Team 1: Identity & Access

#### Sprint 1–2: July 6 – July 27 — Login & Account Management (Feature Work)
- **Epics:** Authentication, Registration & Onboarding, Password & Security, Account Settings
- **Adjusted SP:** ~48
- **Blockers:** None — foundational work
- 📝 **Notes:** Token validation API must be published by July 27 for all downstream teams.

#### Sprint 3–7: July 28 – September 7 — Platform Infrastructure & Hardening
- **Work:** Shared auth libraries, token caching strategy, session management optimization, security audit (OWASP top 10), OAuth2/OIDC compliance review
- **Initiative 6 Epics:** Security & Compliance Hardening, Infrastructure Spikes & Vendor Evaluation
- **Adjusted SP:** ~40
- 📝 **Notes:** Do not wait idle. Concurrent with Claims Core's Digital Claims Submission. Publish reusable auth SDKs for frontend and backend teams.

#### Sprint 8–13: September 8 – October 19 — Testing & Observability
- **Work:** Auth integration test harnesses, distributed tracing for token validation, alerting on failed auth patterns, load testing (target 10k req/sec), chaos engineering for session failover
- **Initiative 6 Epics:** Testing & QA Frameworks, Observability & Monitoring
- **Adjusted SP:** ~45
- 📝 **Notes:** Leverage claim submission volume projections from Claims Core to size auth infrastructure.

#### Sprint 14–18: October 20 – November 24 — Compliance & Hardening (Phase 2)
- **Work:** SOC 2 compliance audit, password policy hardening, MFA enforcement options for enterprise customers, session timeout policies, regulatory documentation
- **Initiative 6 Epics:** Security & Compliance Hardening, Production Readiness & On-Call
- **Adjusted SP:** ~35
- 📝 **Notes:** Run in parallel with Adjuster Workflow work. Non-blocking prep for compliance reviews post-launch.

#### Sprint 19–22: November 25 – January 5 — Release Stabilization & On-Call Prep
- **Work:** Production runbooks, on-call training, incident response drills, auth metrics dashboard, customer support playbooks
- **Initiative 6 Epics:** Production Readiness & On-Call
- **Adjusted SP:** ~25
- 📝 **Notes:** Final push to production readiness. All team members trained on escalation procedures.

**Total Adjusted SP for Team 1: ~193** (spans entire program)

---

### Team 2: Claims Core

#### Sprint 1–2: July 6 – July 27 — Architecture & Spikes (Concurrent with Identity & Access Phase 1)
- **Work:** Claims domain model design, event schema design, database schema and indexing strategy, claims state machine POC, integration with Identity Service, API contract definition
- **Initiative 6 Epics:** Infrastructure Spikes & Vendor Evaluation
- **Adjusted SP:** ~35
- 📝 **Notes:** Do not wait for Identity & Access. Spike on dependency injection, async event handling, and event sourcing patterns if applicable.

#### Sprint 3–6: July 28 – September 1 — Digital Claims Submission (Feature Work)
- **Epics:** Online & Mobile Submission Form, Document & Photo Upload, Auto-Save & Resume, Reference Number Generation
- **Adjusted SP:** ~65
- **Blockers:** Identity & Access APIs available
- 📝 **Notes:** Publish `claim.submitted`, `claim.status_changed` event contracts by September 1 for downstream teams.

#### Sprint 7–8: September 2 – September 15 — Claims Status & History (Feature Work)
- **Epics:** Real-Time Claims Status Tracking, Claims History Dashboard, Estimated Resolution Timeline
- **Adjusted SP:** ~20
- 📝 **Notes:** Run in parallel with Comms & Content's notification work. Status data model completed by September 8.

#### Sprint 9–13: September 16 – October 19 — API Optimization & Caching
- **Work:** Read replica strategy for claims queries, Redis caching layer for status dashboards, materialized views for claims history, query performance tuning (target <100ms P99), database connection pooling
- **Initiative 6 Epics:** Infrastructure Spikes & Vendor Evaluation, Observability & Monitoring
- **Adjusted SP:** ~45
- 📝 **Notes:** Critical for scale — Comms and Intelligence teams will query claims heavily. Start observability/APM integration.

#### Sprint 14–17: October 20 – November 17 — Analytics & Reporting Infrastructure
- **Work:** Claims metrics collection (submission rate, approval rate, time to resolution), analytics event schema, data warehouse integration, reporting dashboard for ops team
- **Initiative 6 Epics:** Observability & Monitoring
- **Adjusted SP:** ~40
- 📝 **Notes:** Run in parallel with Adjuster Workflow and Comms work. Enable stakeholders to monitor program KPIs in real time.

#### Sprint 18–22: November 18 – January 5 — Release Hardening & Scale Testing
- **Work:** Load testing (target peak claim volume 2x max), stress testing under payment processing volume, data migration tooling from legacy system, production cutover runbooks, rollback procedures, claim archival strategy
- **Initiative 6 Epics:** Testing & QA Frameworks, Production Readiness & On-Call
- **Adjusted SP:** ~35
- 📝 **Notes:** Coordinate with Payments team on end-to-end load tests. Prepare ops team for launch day.

**Total Adjusted SP for Team 2: ~240** (spans entire program)

---

### Team 3: Intelligence & Workflow

#### Sprint 1–2: July 6 – July 27 — Fraud Detection Infrastructure Spike (Concurrent with Phase 1)
- **Work:** Fraud detection model evaluation, ML infrastructure POC, feature engineering for claim attributes, baseline model setup, integration patterns with Claims Service
- **Initiative 6 Epics:** Infrastructure Spikes & Vendor Evaluation
- **Adjusted SP:** ~40
- 📝 **Notes:** Do not wait for Claims Core. Partner with data science/ML team if available. Publish fraud detection API contract.

#### Sprint 3–5: July 28 – September 1 — Rules Engine Spike & Routing Design
- **Work:** Rules engine evaluation (Drools, Easy Rules, custom), claim routing POC, adjuster assignment algorithm design, completeness check rules catalog, straight-through processing thresholds
- **Initiative 6 Epics:** Infrastructure Spikes & Vendor Evaluation
- **Adjusted SP:** ~38
- 📝 **Notes:** Run concurrent with Claims Core's submission work. Rules engine must be configurable by business users post-launch.

#### Sprint 6–13: September 2 – October 27 — Validation & Routing (Feature Work)
- **Epics:** Automated Completeness Checks, Fraud Detection & Flagging, Rules-Based Routing, Straight-Through Processing
- **Adjusted SP:** ~120
- **Blockers:** Digital Claims Submission available
- 📝 **Notes:** Longest workstream — drives critical path. Publish `claim.approved`, `claim.routed` event contracts by October 27. Monitor fraud model accuracy weekly.

#### Sprint 14–17: October 28 – November 24 — Adjuster Workflow Management (Feature Work)
- **Epics:** Adjuster Dashboard & Claims Queue, Decision Recording & Audit Trail
- **Adjusted SP:** ~50
- 📝 **Notes:** Publish `claim.approved` event for Payments team by November 24.

#### Sprint 18–22: November 25 – January 5 — Workflow Optimization & Fraud Hardening
- **Work:** Adjuster performance analytics, fraud model retraining pipeline, rules engine optimization for latency, A/B testing framework for routing strategies, adjuster SLA monitoring, fraud false-positive investigation tooling
- **Initiative 6 Epics:** Observability & Monitoring, Production Readiness & On-Call
- **Adjusted SP:** ~40
- 📝 **Notes:** Run parallel with Payments launch. Prepare for post-launch fraud tuning based on real volume.

**Total Adjusted SP for Team 3: ~288** (spans entire program)

---

### Team 4: Comms & Content

#### Sprint 1–2: July 6 – July 27 — WebSocket & Messaging Infrastructure Spike (Concurrent with Phase 1)
- **Work:** WebSocket architecture evaluation, real-time messaging POC, connection pooling and failover, message queue selection (RabbitMQ, Kafka, etc.), integration with Claims Service events
- **Initiative 6 Epics:** Infrastructure Spikes & Vendor Evaluation
- **Adjusted SP:** ~35
- 📝 **Notes:** Do not wait. High technical risk — spike early. Publish messaging API contract.

#### Sprint 3–4: July 28 – August 18 — Document Service Architecture & Upload Infrastructure
- **Work:** File storage backend evaluation, virus scanning integration, document indexing for search, access control model, multipart upload optimization
- **Initiative 6 Epics:** Infrastructure Spikes & Vendor Evaluation, Testing & QA Frameworks
- **Adjusted SP:** ~28
- 📝 **Notes:** Concurrent with Claims Core's submission work. Document Service must support upload by September 1.

#### Sprint 5–8: August 19 – September 15 — Document Upload (Feature Work) + Notifications (Feature Work)
- **Document Epics:** Document & Photo Upload (partnered with Claims Core)
- **Notification Epics:** Automated Email & SMS Notifications
- **Adjusted SP:** ~18 (notifications) + support for Claims Core uploads
- 📝 **Notes:** Notifications are event-driven from Claims Core. Minimal coupling required.

#### Sprint 9–10: September 16 – October 7 — Notification Quality & Testing
- **Work:** Notification delivery testing (email/SMS), templating system enhancement, localization for multi-region support, notification retry/backoff logic, delivery SLA monitoring (target 95% delivered in <5 min)
- **Initiative 6 Epics:** Testing & QA Frameworks, Observability & Monitoring
- **Adjusted SP:** ~30
- 📝 **Notes:** Run in parallel with Intelligence team's routing work. No blockers.

#### Sprint 11–14: October 8 – November 3 — In-App Messaging (Feature Work)
- **Epics:** In-App Messaging with Policyholders, Document Review & Annotation Tools
- **Adjusted SP:** ~40
- **Blockers:** Validation & Routing work from Intelligence team
- 📝 **Notes:** Messaging and document annotation are core to adjuster workflow. WebSocket infrastructure tested and ready.

#### Sprint 15–22: November 4 – January 5 — Messaging Scale Testing & Content Hardening
- **Work:** Load testing messaging (target 5k concurrent connections), document annotation latency optimization, bulk messaging for notifications, rich media support, accessibility audit (WCAG 2.1 AA), customer support content library
- **Initiative 6 Epics:** Testing & QA Frameworks, Observability & Monitoring, Production Readiness & On-Call
- **Adjusted SP:** ~45
- 📝 **Notes:** Coordinate with Payments team on full end-to-end messaging during payment notifications. Build self-service content for common questions.

**Total Adjusted SP for Team 4: ~196** (spans entire program)

---

### Team 5: Payments

#### Sprint 1–3: July 6 – August 17 — PCI Compliance & Integration Architecture (Concurrent with Phases 1–2)
- **Work:** PCI compliance audit and gap analysis, payment processor integration spike (Stripe, Adyen, Square, etc.), payment method tokenization design, compliance documentation, incident response playbooks
- **Initiative 6 Epics:** Infrastructure Spikes & Vendor Evaluation, Security & Compliance Hardening
- **Adjusted SP:** ~42
- 📝 **Notes:** Do not wait for Claims. Critical security/compliance work must be done early. Publish payment integration API contract.

#### Sprint 4–6: August 18 – September 7 — Mock Payment System & Testing Framework
- **Work:** Mock payment processor for integration testing, test data generation for various payment methods and failure scenarios, payment API test harness, latency testing framework, fraud detection integration testing
- **Initiative 6 Epics:** Testing & QA Frameworks
- **Adjusted SP:** ~38
- 📝 **Notes:** Enables other teams to test end-to-end flows with simulated payments. No team blocked waiting for real payment infrastructure.

#### Sprint 7–9: September 8 – September 30 — Payment Processing Integration (Architecture Phase)
- **Work:** Payment initiation workflow design, webhook handling for payment status updates, idempotency key strategy, transaction logging and reconciliation design, PCI isolation architecture
- **Initiative 6 Epics:** Infrastructure Spikes & Vendor Evaluation, Observability & Monitoring
- **Adjusted SP:** ~35
- 📝 **Notes:** Foundations for feature work. Validate integration patterns with payment processor vendor.

#### Sprint 10–13: October 1 – October 27 — Staging Integration & Partner Validation
- **Work:** Staging environment payment processor setup, end-to-end staging tests, partner (payment processor) sign-off on integration, payment method support verification (direct deposit, check, card, etc.)
- **Initiative 6 Epics:** Testing & QA Frameworks, Security & Compliance Hardening
- **Adjusted SP:** ~36
- 📝 **Notes:** Preparatory work for feature implementation. No blockers from upstream teams yet.

#### Sprint 14–17: October 28 – November 24 — Production Integration Setup & Cutover Planning
- **Work:** Production payment processor setup, regulatory filing and licensing verification, payment SLA agreements, customer support escalation paths, payment reconciliation reports, rollback procedures
- **Initiative 6 Epics:** Security & Compliance Hardening, Production Readiness & On-Call
- **Adjusted SP:** ~35
- 📝 **Notes:** Run parallel with Adjuster Workflow feature work. Wait for `claim.approved` event contract from Intelligence team (due October 27).

#### Sprint 18–22: November 25 – January 5 — Payment Processing Integration (Feature Work) + Release Hardening
- **Epics:** Payment Processing System Integration, Automated Payment Initiation on Approval, Multiple Payment Method Support, Payment Status Tracking & Confirmation
- **Adjusted SP:** ~85
- **Blockers:** `claim.approved` event from Intelligence & Workflow (available November 24)
- 📝 **Notes:** Final feature sprint. Coordinate with Claims Core and Comms on end-to-end tests. On-call training for launch. Monitor payment success rate (target >99%).

**Total Adjusted SP for Team 5: ~271** (spans entire program)

---

## Key Dependencies & Event Contracts

| Phase | Producer | Event / Deliverable | Consumers | Due Date |
|---|---|---|---|---|
| 1 | Identity & Access | Token validation API | All teams | July 27, 2026 |
| 2 | Claims Core | `claim.submitted` event | Intelligence, Comms, Audit | September 1, 2026 |
| 2 | Claims Core | `claim.status_changed` event | Comms, Audit | September 1, 2026 |
| 3 | Intelligence & Workflow | `claim.approved` event | Payments, Audit | October 27, 2026 |
| 3 | Intelligence & Workflow | `claim.routed` event | Claims Core, Audit | October 27, 2026 |
| 4 | Intelligence & Workflow | `claim.approved` event (final) | Payments launch | November 24, 2026 |

---

## Action Items

| #   | Action | Owner | Due Date |
| --- | ------ | ----- | -------- |
| 1   | Publish token validation API contract | Identity & Access | July 27, 2026 |
| 2   | Publish fraud detection API contract | Intelligence & Workflow | July 27, 2026 |
| 3   | Publish messaging/WebSocket architecture | Comms & Content | July 27, 2026 |
| 4   | Publish payment integration API contract | Payments | August 17, 2026 |
| 5   | Deploy mock payment system | Payments | September 7, 2026 |
| 6   | Publish `claim.submitted` and `claim.status_changed` event contracts | Claims Core | September 1, 2026 |
| 7   | Complete fraud model baseline | Intelligence & Workflow | September 8, 2026 |
| 8   | Publish `claim.approved` and `claim.routed` event contracts | Intelligence & Workflow | October 27, 2026 |
| 9   | Staging payment processor sign-off | Payments | October 27, 2026 |
| 10  | Production payment processor setup complete | Payments | November 17, 2026 |

---

## Risk Register

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Fraud detection model accuracy below threshold | Medium | High | Baseline model by Sept 1; weekly retraining; fallback to manual review |
| Payment processor integration delays | Medium | Critical | Spike completed by Aug 31; staging validation by Oct 20; vendor sign-off required |
| WebSocket scaling under peak load | Low | High | Load test during sprint 15–22; target 5k concurrent; failover testing in sprint 11–14 |
| Claims database query performance degradation | Low | Medium | Caching layer (Sprint 9–13); read replicas; materialized views; APM monitoring |
| Compliance audit findings post-sprint 1 | Medium | Medium | Early PCI audit (Sprint 1–3); compliance checklist published; remediation sprint budgeted |

---

## Delivery Timeline Summary

**All teams active July 6 – January 5, 2027. No idle periods.**

| Team | Sprint 1–2 | Sprint 3–6 | Sprint 7–13 | Sprint 14–17 | Sprint 18–22 |
|---|---|---|---|---|---|
| **Identity & Access** | Login & Acct Mgmt | Platform Infra | Testing & Observability | Compliance & Hardening | Release Stabilization |
| **Claims Core** | Arch & Spikes | Digital Submission | API Optimization | Analytics & Reporting | Release Hardening |
| **Intelligence & Workflow** | Fraud + Rules Spike | Routing Design | Validation & Routing | Adjuster Workflow | Workflow Optimization |
| **Comms & Content** | WebSocket + Document Spike | Document Upload | Notification Quality | In-App Messaging | Scale Testing & Hardening |
| **Payments** | PCI & Integration Spike | Mock Payment System | Payment Integration Arch | Staging & Cutover | Payment Feature + Hardening |

---

## Summary

> Share this summary in Slack after the meeting.

- **Key decisions:** Zero-idle timeline — all five teams active throughout the 27-week program. Early phases prioritize infrastructure spikes, testing frameworks, and vendor validation. Feature work gates on dependencies, but no team waits idle.
- **Upcoming risks:** (1) Fraud model accuracy — establish baseline by Sept 8; (2) Payment processor integration — complete staging sign-off by Oct 27; (3) WebSocket scale — load test during Nov–Jan.
- **Critical path:** Claims Core (Digital Submission) → Intelligence & Workflow (Validation & Routing) → Payments (Feature Work). Any slip in Intelligence & Workflow cascades directly to release date.
- **Next program sprint planning date:** July 20, 2026
