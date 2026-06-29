# Microservices Architecture: Automated Claims Processing

---

## Service 1: Identity Service
Handles authentication, session management, MFA, and password management.

**Maps to:** Initiative 0 — Epics 1 & 3

**Responsibilities:**
- Login / logout flows
- Session token issuance and validation
- Multi-factor authentication (MFA)
- Password reset and change password

**Notes:** Foundational dependency — all other services rely on it for token validation.

---

## Service 2: User/Account Service
Owns user profiles, onboarding, account settings, and notification preferences.

**Maps to:** Initiative 0 — Epics 2 & 4

**Responsibilities:**
- Account registration and onboarding
- Profile and personal information management
- Notification preferences
- Linked policy management

**Notes:** Kept separate from Identity so profile changes don't require touching auth infrastructure.

---

## Service 3: Claims Service
Core domain service — owns the claim lifecycle from submission through resolution.

**Maps to:** Initiative 1 (all epics), Initiative 2 — Epics 1, 3 & 4

**Responsibilities:**
- Claim submission forms (web and mobile)
- Auto-save and resume incomplete submissions
- Reference number generation
- Real-time claims status tracking
- Claims history dashboard
- Estimated resolution timeline

**Notes:** Central aggregate owner for claim data. Other services react to claim events rather than directly modifying claim state.

---

## Service 4: Document Service
Manages upload, storage, retrieval, and annotation of files across the platform.

**Maps to:** Initiative 1 — Epic 2, Initiative 4 — Epic 3

**Responsibilities:**
- Document and photo upload
- Secure file storage and retrieval
- Document annotation and markup tools for adjusters

**Notes:** Shared by policyholders (submission) and adjusters (review). Isolated so storage backends can be swapped independently.

---

## Service 5: Notification Service
Delivers email, SMS, and in-app alerts using templates triggered by platform events.

**Maps to:** Initiative 2 — Epic 2

**Responsibilities:**
- Automated email and SMS notifications
- Notification templates per claim stage
- Delivery status tracking

**Notes:** Fire-and-forget from other services via events. No direct dependencies on core claim state.

---

## Service 6: Fraud & Validation Service
Validates claim completeness and detects potentially fraudulent submissions.

**Maps to:** Initiative 3 — Epics 1 & 2

**Responsibilities:**
- Automated completeness checks on submission
- Fraud detection and flagging for manual review

**Notes:** Isolated because fraud detection likely requires its own ML infrastructure and independent update cadence.

---

## Service 7: Routing & Workflow Service
Owns the rules engine, adjuster queue management, and straight-through processing logic.

**Maps to:** Initiative 3 — Epics 3 & 4, Initiative 4 — Epics 1 & 4

**Responsibilities:**
- Rules-based claim routing to adjusters or teams
- Straight-through processing for simple/low-value claims
- Adjuster dashboard and claims queue
- Decision recording and audit trail

**Notes:** Encapsulates business rules that change frequently without requiring changes to the claims data model.

---

## Service 8: Messaging Service
Provides real-time in-app messaging between adjusters and policyholders.

**Maps to:** Initiative 4 — Epic 2

**Responsibilities:**
- Bidirectional in-app messaging
- Message history and thread tracking
- Read receipts and delivery status

**Notes:** Warrants its own service due to WebSocket/real-time requirements that differ from the rest of the stack.

---

## Service 9: Payment Service
Handles payment initiation, method management, and payout status tracking.

**Maps to:** Initiative 5 (all epics)

**Responsibilities:**
- Integration with payment processing systems
- Automated payment initiation on claim approval
- Multiple payment method support (direct deposit, check, etc.)
- Payment status tracking and confirmation

**Notes:** PCI compliance requirements justify hard isolation — minimal blast radius around payment data.

---

## Service 10: Audit/Event Log Service
Append-only audit trail capturing events emitted across all services.

**Maps to:** Initiative 4 — Epic 4 (cross-cutting)

**Responsibilities:**
- Centralized event ingestion from all services
- Immutable audit log storage
- Audit query and reporting

**Notes:** Write-only append log. Other services emit events; this service persists them. Serves compliance and forensic needs across the entire platform.

---

## Runtime Dependency Order

```
Identity Service
  └─ User/Account Service
       └─ Claims Service
            ├─ Fraud & Validation Service
            ├─ Document Service
            └─ Routing & Workflow Service
                 └─ Payment Service

Notification Service     ← async, event-driven
Messaging Service        ← async, real-time
Audit/Event Log Service  ← async, append-only
```
