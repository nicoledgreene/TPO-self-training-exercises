# Estimating: Automated Claims Processing

---

## Initiative 0: Login & Account Management
Provide policyholders, adjusters, and admins with secure authentication and self-service account management capabilities.

> **Note:** Foundational dependency for all other initiatives — must be delivered first.

**Estimate:** `[40 70%]` → Adjusted (90th %): ~64 story points

### Epics

#### Epic 1: User Authentication (Login / Logout)
Build secure login and logout flows for policyholders and adjusters, including session management.

#### Epic 2: Account Registration and Onboarding
Allow new policyholders to create an account and complete initial profile setup.

#### Epic 3: Password and Security Management
Support password reset, change password, and multi-factor authentication (MFA).

#### Epic 4: Account Settings and Profile Management
Enable users to view and update personal information, notification preferences, and linked policies.

#### Epic 5: Admin & Assessor Account Management
Support creation, management, and role assignment for internal admin and assessor accounts with appropriate access controls.

---

## Initiative 1: Digital Claims Submission
Enable policyholders to submit claims online or via mobile with document and photo upload capabilities.

**Estimate:** `[40 70%]` → Adjusted (90th %): ~65 story points

### Epics

#### Epic 1: Online and Mobile Claim Submission Form
Build the core submission form experience across web and mobile.

#### Epic 2: Document and Photo Upload
Allow policyholders to attach supporting documents and photos to a claim.

#### Epic 3: Auto-Save and Resume Incomplete Submissions
Preserve in-progress submissions so policyholders can return and complete them later.

#### Epic 4: Confirmation and Reference Number Generation
Generate and deliver a reference number upon successful claim submission.

---

## Initiative 2: Claims Status & Notifications
Provide policyholders with real-time visibility into the status of their claim and automated updates throughout the process.

**Estimate:** `[25 75%]` → Adjusted (90th %): ~38 story points

### Epics

#### Epic 1: Real-Time Claims Status Tracking
Display live claim status to policyholders throughout the review and resolution process.

#### Epic 2: Automated Email and SMS Notifications
Send automated updates at each stage of the claims process via email and SMS.

#### Epic 3: Claims History Dashboard
Give policyholders a single view of all past and active claims.

#### Epic 4: Estimated Resolution Timeline
Surface an expected resolution date on each claim based on type and complexity.

---

## Initiative 3: Automated Claims Validation & Routing
Automatically validate submitted claims for completeness and route them to the appropriate adjuster or processing queue.

> **Note:** Depends on Initiative 1 (Digital Claims Submission) being in place.

**Estimate:** `[60 50%]` → Adjusted (90th %): ~120 story points

### Epics

#### Epic 1: Automated Completeness Checks
Validate that all required fields and documents are present on submission.

#### Epic 2: Fraud Detection and Flagging
Identify and flag potentially fraudulent claims for manual review.

#### Epic 3: Rules-Based Routing
Route claims to the appropriate adjuster or team based on type, value, and complexity rules.

#### Epic 4: Straight-Through Processing
Automatically approve and process simple or low-value claims without adjuster intervention.

---

## Initiative 4: Adjuster Workflow Management
Provide claims adjusters with digital tools to efficiently review, communicate, and resolve assigned claims.

**Estimate:** `[50 60%]` → Adjusted (90th %): ~90 story points

### Epics

#### Epic 1: Adjuster Dashboard and Claims Queue
Give adjusters a centralized view of their assigned claims with prioritization and filtering.

#### Epic 2: In-App Messaging with Policyholders
Enable direct, tracked communication between adjusters and policyholders within the platform.

#### Epic 3: Document Review and Annotation Tools
Allow adjusters to view, annotate, and mark up submitted documents in-app.

#### Epic 4: Decision Recording and Audit Trail
Capture adjuster decisions and maintain a full audit trail for each claim.

---

## Initiative 5: Payment Processing Integration
Automate payment initiation and tracking once a claim has been approved, reducing payout time.

**Estimate:** `[45 55%]` → Adjusted (90th %): ~85 story points

### Epics

#### Epic 1: Payment Processing System Integration
Connect the claims platform to the payment processing system to trigger payouts.

#### Epic 2: Automated Payment Initiation on Approval
Automatically initiate payment when a claim is approved without manual intervention.

#### Epic 3: Multiple Payment Method Support
Support direct deposit, check, and other payment methods based on policyholder preference.

#### Epic 4: Payment Status Tracking and Confirmation
Notify policyholders of payment status and confirm successful delivery.

---

---

## Summary

| Initiative | Median SP | Confidence | Adjusted SP (90th %) |
|---|---|---|---|
| Login & Account Management | 40 | 70% | ~64 |
| Digital Claims Submission | 40 | 70% | ~65 |
| Claims Status & Notifications | 25 | 75% | ~38 |
| Automated Claims Validation & Routing | 60 | 50% | ~120 |
| Adjuster Workflow Management | 50 | 60% | ~90 |
| Payment Processing Integration | 45 | 55% | ~85 |
| **Total** | **260** | | **~462** |
