# Program Sprint Planning

**Date:** July 6, 2026
**Facilitator:** Nicole Greene

---

## Agenda

> Organized by initiative, sorted by release date (closest to delivery first).
> Five teams running in phased sequence July 6 – January 5, 2027.
> See `teams.md` for full service ownership. See `services.md` for microservice definitions.

---

## Initiative: Automated Claims Processing

**Release Target:** January 5, 2027
**`1:40`** | 👥 Identity & Access, Claims Core, Intelligence & Workflow, Comms & Content, Payments

> **Scope:** Initiatives 0–5 (Login & Account Management, Digital Claims Submission, Claims Status & Notifications, Validation & Routing, Adjuster Workflow, Payment Processing)
> **Total Adjusted SP:** ~462

---

## Phase 1 — Foundation

### Identity & Access — Login & Account Management (Initiative 0)

- **Status:** To Do
- **Start date:** July 6, 2026
- **End date:** August 3, 2026
- **Epics:** User Authentication, Account Registration & Onboarding, Password & Security Management, Account Settings & Profile Management, Admin & Assessor Account Management
- **Adjusted SP:** ~64 (30 SP/sprint, ~4.3 weeks)
- 🛑 **Blockers:** None — must deliver first, unblocks all other teams
- 📝 **Notes:** Foundational dependency for the entire platform. Token validation API and admin account management flows must be published by August 3 for all downstream teams.

---

## Phase 2 — Core Claims Domain

> Begins August 4 once Identity & Access APIs are live.

### Claims Core — Digital Claims Submission (Initiative 1)

- **Status:** To Do
- **Start date:** August 4, 2026
- **End date:** September 8, 2026
- **Epics:** Online & Mobile Submission Form, Document & Photo Upload, Auto-Save & Resume, Reference Number Generation
- **Adjusted SP:** ~65 (30 SP/sprint, ~4.3 weeks)
- 🛑 **Blockers:** Identity & Access must be complete
- 📝 **Notes:** Critical path epic. Intelligence & Workflow, Comms & Content, and Payments teams are blocked until this delivers. Claims Service event contracts (`claim.submitted`) must be published at the end of this phase.

---

## Phase 3 — Parallel Workstreams

> Begins September 9 once Claims Core delivers Digital Claims Submission.

### Claims Core — Claims Status & History (Initiative 2, partial)

- **Status:** To Do
- **Start date:** September 9, 2026
- **End date:** September 22, 2026
- **Epics:** Real-Time Claims Status Tracking, Claims History Dashboard, Estimated Resolution Timeline
- **Adjusted SP:** ~20 of 38 total Initiative 2 SP
- 🛑 **Blockers:** Digital Claims Submission must be complete
- 📝 **Notes:** Runs in parallel with Comms & Content's notification work. Claims Core owns the state machine and data; Comms consumes events to trigger alerts.

### Comms & Content — Claims Status Notifications (Initiative 2, partial)

- **Status:** To Do
- **Start date:** September 9, 2026
- **End date:** September 22, 2026
- **Epics:** Automated Email & SMS Notifications
- **Adjusted SP:** ~18 of 38 total Initiative 2 SP
- 🛑 **Blockers:** Digital Claims Submission must be complete; `claim.status_changed` event contract from Claims Core
- 📝 **Notes:** Runs fully in parallel with Claims Core's Phase 3 work. Event-driven — no direct dependency on Claims Core's internal state.

### Intelligence & Workflow — Automated Claims Validation & Routing (Initiative 3)

- **Status:** To Do
- **Start date:** September 9, 2026
- **End date:** November 3, 2026
- **Epics:** Automated Completeness Checks, Fraud Detection & Flagging, Rules-Based Routing, Straight-Through Processing
- **Adjusted SP:** ~120 (30 SP/sprint, ~8 weeks)
- 🛑 **Blockers:** Digital Claims Submission must be complete
- 📝 **Notes:** Longest workstream — drives the critical path through Phase 3. Lowest confidence (50%) across the entire program — monitor closely for scope expansion. `claim.approved` and `claim.routed` event contracts must be published before Phase 4.

---

## Phase 4 — Workflow & Comms Completion

> Begins November 4 once Intelligence & Workflow delivers Validation & Routing.

### Intelligence & Workflow — Adjuster Workflow Management, Part 1 (Initiative 4, partial)

- **Status:** To Do
- **Start date:** November 4, 2026
- **End date:** December 1, 2026
- **Epics:** Adjuster Dashboard & Claims Queue, Decision Recording & Audit Trail
- **Adjusted SP:** ~50 of 90 total Initiative 4 SP
- 🛑 **Blockers:** Automated Claims Validation & Routing must be complete
- 📝 **Notes:** Runs in parallel with Comms & Content's messaging and document work. `claim.approved` event published at end of this phase unblocks Payments.

### Comms & Content — Adjuster Workflow Management, Part 2 (Initiative 4, partial)

- **Status:** To Do
- **Start date:** November 4, 2026
- **End date:** November 24, 2026
- **Epics:** In-App Messaging with Policyholders, Document Review & Annotation Tools
- **Adjusted SP:** ~40 of 90 total Initiative 4 SP
- 🛑 **Blockers:** Automated Claims Validation & Routing must be complete; Document Service upload capability from Phase 2
- 📝 **Notes:** Runs fully in parallel with Intelligence & Workflow's Phase 4 work.

---

## Phase 5 — Payments

> Begins December 2 once Intelligence & Workflow publishes the `claim.approved` event.

### Payments — Payment Processing Integration (Initiative 5)

- **Status:** To Do
- **Start date:** December 2, 2026
- **End date:** January 5, 2027
- **Epics:** Payment Processing System Integration, Automated Payment Initiation on Approval, Multiple Payment Method Support, Payment Status Tracking & Confirmation
- **Adjusted SP:** ~85 (30 SP/sprint, ~5.5 weeks)
- 🛑 **Blockers:** Adjuster Workflow Management must be complete; `claim.approved` event from Intelligence & Workflow
- 📝 **Notes:** PCI compliance requirements apply — maintain hard isolation from other services. Final epic in the delivery chain. No float — if Phase 4 slips, this date slips directly.

---

## Action Items

| #   | Action | Owner | Due Date |
| --- | ------ | ----- | -------- |
| 1   | Publish token validation API contract | Identity & Access | August 3, 2026 |
| 2   | Publish admin account management API | Identity & Access | August 3, 2026 |
| 3   | Publish `claim.submitted` and `claim.status_changed` event contracts | Claims Core | September 8, 2026 |
| 4   | Publish `claim.approved` and `claim.routed` event contracts | Intelligence & Workflow | November 3, 2026 |

---

## Continuous Exploration (CX) Board Review

> Review initiative progress right to left.

| Initiative | Stage | Notes |
| --- | --- | --- |
| Automated Claims Processing | Planning | Five teams defined, services decomposed, phased sprint plan updated. Phase 1 begins July 6. |

---

## Delivery Timeline Summary

| Phase | Team | Initiative | Start | End | SP |
| --- | --- | --- | --- | --- | --- |
| 1 | Identity & Access | Login & Account Management | Jul 6 | Aug 3 | ~64 |
| 2 | Claims Core | Digital Claims Submission | Aug 4 | Sep 8 | ~65 |
| 3 | Claims Core | Claims Status (status/history) | Sep 9 | Sep 22 | ~20 |
| 3 | Comms & Content | Claims Status (notifications) | Sep 9 | Sep 22 | ~18 |
| 3 | Intelligence & Workflow | Validation & Routing | Sep 9 | Nov 3 | ~120 |
| 4 | Intelligence & Workflow | Adjuster Workflow (queue/decisions) | Nov 4 | Dec 1 | ~50 |
| 4 | Comms & Content | Adjuster Workflow (messaging/docs) | Nov 4 | Nov 24 | ~40 |
| 5 | Payments | Payment Processing Integration | Dec 2 | Jan 5 | ~85 |

---

## Summary

> Share this summary in Slack after the meeting.

- **Key decisions:** Five specialized teams, phased delivery. Login & Account Management added as required Phase 1 prerequisite with admin/assessor account support. Simple phase-gate model with natural idle periods between phases.
- **Upcoming risks:** Intelligence & Workflow's Validation & Routing work (120 SP, 50% confidence) is the highest-risk workstream and the critical path gate for Phases 4 and 5. Any slip here delays Payments and the final release date directly.
- **Next program sprint planning date:** July 20, 2026
