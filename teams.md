# Team Structure: Automated Claims Processing

---

## Team 1: Identity & Access
Owns authentication, session management, and user account data.

**Services:**
- Service 1: Identity Service
- Service 2: User/Account Service

**Core Responsibilities:**
- Login, logout, MFA, and password management
- User registration and onboarding
- Profile, account settings, and notification preferences
- Admin and assessor account creation, management, and role assignment

**Recommended Size:** 3–4 engineers

**Notes:** Foundational team — delivers first. Once APIs stabilize, minimal ongoing coordination required with other teams. All other teams depend on token validation from this service.

---

## Team 2: Claims Core
Owns the central claims domain — the highest-value, highest-complexity area of the platform.

**Services:**
- Service 3: Claims Service
- Service 10: Audit/Event Log Service

**Core Responsibilities:**
- Claim submission, auto-save, and reference number generation
- Claim lifecycle and status tracking
- Claims history dashboard and resolution timelines
- Platform-wide audit trail and event log

**Recommended Size:** 4–5 engineers

**Notes:** Largest team due to domain complexity. Audit is included here because claims events are the primary driver of the audit log. This team sets the event contracts that Comms, Intelligence, and Payments teams consume.

---

## Team 3: Intelligence & Workflow
Owns fraud detection, validation logic, routing rules, and adjuster workflow management.

**Services:**
- Service 6: Fraud & Validation Service
- Service 7: Routing & Workflow Service

**Core Responsibilities:**
- Automated completeness validation on submission
- Fraud detection and flagging
- Rules-based claim routing to adjusters
- Straight-through processing for simple claims
- Adjuster queue, prioritization, and decision recording

**Recommended Size:** 3–4 engineers (ideally includes ML or data science skill)

**Notes:** Highest algorithmic complexity. Fraud detection may require a separate ML pipeline. Routing rules will change frequently as business needs evolve — design for configurability.

---

## Team 4: Comms & Content
Owns all communication and document management across the platform.

**Services:**
- Service 4: Document Service
- Service 5: Notification Service
- Service 8: Messaging Service

**Core Responsibilities:**
- Document and photo upload, storage, and retrieval
- Document annotation tools for adjusters
- Automated email and SMS notifications
- Real-time in-app messaging between adjusters and policyholders

**Recommended Size:** 3–4 engineers

**Notes:** Three services but all are communication-layer concerns with no core claims logic. Notifications and messaging are event-driven — this team consumes events from Claims Core rather than holding domain state. Document Service is shared infrastructure; treat it as an internal platform dependency.

---

## Team 5: Payments
Owns all payment processing, method management, and payout tracking.

**Services:**
- Service 9: Payment Service

**Core Responsibilities:**
- Integration with external payment processing systems
- Automated payment initiation on claim approval
- Multiple payment method support (direct deposit, check, etc.)
- Payment status tracking and confirmation

**Recommended Size:** 2–3 engineers

**Notes:** Hard boundary for PCI compliance — payment data must not bleed into other services. This team should own their own deployment pipeline and access controls. Triggered by an event from Intelligence & Workflow when a claim is approved.

---

## Cross-Team Interfaces

These contracts must be defined early to prevent blocking dependencies between teams.

| Producer | Event / API | Consumers |
|---|---|---|
| Identity & Access | Auth token validation API | All teams |
| Claims Core | `claim.submitted` event | Intelligence & Workflow, Comms & Content, Audit |
| Claims Core | `claim.status_changed` event | Comms & Content, Audit |
| Intelligence & Workflow | `claim.approved` event | Payments, Audit |
| Intelligence & Workflow | `claim.routed` event | Claims Core, Audit |
| Payments | `payment.initiated` event | Claims Core, Comms & Content, Audit |

---

## Delivery Order

Teams should be stood up and deliver in this sequence to respect foundational dependencies:

```
Phase 1:  Identity & Access        ← unblocks everything
Phase 2:  Claims Core              ← unblocks Intelligence, Comms, Payments
Phase 3:  Intelligence & Workflow  ← parallel with Comms & Content
          Comms & Content          ← parallel with Intelligence & Workflow
Phase 4:  Payments                 ← depends on Intelligence & Workflow approval event
```
