# 🎓 University of Dubai — Conference Registration System (CRS)
## Product Requirements Document · v1.0

---

> **Document Status:** Draft — For Review  
> **Version:** 1.0  
> **Date:** May 2025  
> **Prepared by:** Research Affairs  
> **Audience:** IT Dept  
> **Classification:** Confidential — Internal Use Only

---

## 📋 Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Problem Statement & Current-State Analysis](#2-problem-statement--current-state-analysis)
3. [Goals & Success Metrics](#3-goals--success-metrics)
4. [Stakeholders & User Roles](#4-stakeholders--user-roles)
5. [System Architecture Overview](#5-system-architecture-overview)
6. [Functional Requirements](#6-functional-requirements)
   - 6.1 [Module 1: Authentication & Profile Management](#61-module-1-user-authentication--profile-management)
   - 6.2 [Module 2: Conference Application Form](#62-module-2-conference-application-form)
   - 6.3 [Module 3: Conference Approval Workflow](#63-module-3-conference-approval-workflow)
   - 6.4 [Module 4: PRF Auto-Generation](#64-module-4-purchase-requisition-form-prf-auto-generation)
   - 6.5 [Module 5: Dashboard & Analytics](#65-module-5-dashboard--analytics)
7. [Post-Conference Compliance Module](#7-post-conference-compliance-module)
8. [Non-Functional Requirements](#8-non-functional-requirements)
9. [GitHub Repository Structure](#9-github-repository-structure)
10. [Implementation Roadmap](#10-implementation-roadmap)
11. [Core Data Model](#11-core-data-model-entity-overview)
12. [UI/UX Design Guidelines](#12-uiux-design-guidelines)
13. [Creative & AI Enhancement Suggestions](#13-creative--ai-enhancement-suggestions)
14. [Risks & Mitigations](#14-risks--mitigations)
15. [Acceptance Criteria for Go-Live](#15-acceptance-criteria-for-go-live)
16. [Glossary](#16-glossary)
17. [Document Sign-Off](#17-document-sign-off)

---

## 1. Executive Summary

The University of Dubai (UD) currently manages faculty conference attendance through a fully **manual, paper-based process**. Faculty members complete a Microsoft Word checklist, which is routed through up to five levels of approvers before manual data entry into Excel spreadsheets. This process is error-prone, time-consuming, and provides no real-time visibility to the management.

The **Conference Registration System (CRS)** is a purpose-built, web-based platform that will digitise, automate, and intelligently manage this end-to-end workflow — from initial faculty application through multi-tier approvals, automated Purchase Requisition Form (PRF) generation, and live executive dashboards.

> **Strategic Objective:** Reduce conference processing time from an average of 10–15 working days to under 3 working days, eliminate manual data re-entry, and give leadership real-time insight into conference activity, research output, and associated expenditure across all three colleges.

---

## 2. Problem Statement & Current-State Analysis

### 2.1 Current Workflow Pain Points

- Faculty must hand-fill and deliver a Word document through multiple departments.
- There is no automated notification system; approvers are unaware of pending requests without manual follow-up.
- No central visibility: senior management cannot see live status of applications, budget consumption, or approval bottlenecks.
- Post-conference compliance (returning proceedings, library copies) is tracked informally with no reminder system.
- PRF documents must be separately prepared and manually routed through a second approval chain, duplicating effort.
- Historic data is locked in disconnected Excel files, making trend analysis and reporting manual and inconsistent.

---

## 3. Goals & Success Metrics

### 3.1 Primary Goals

1. Eliminate all paper-based and email-based conference approval workflows.
2. Automate the complete approval chain with in-system notifications and email alerts for both conference approval and PRF processing.
3. Auto-populate the PRF from approved conference application data, eliminating duplicate entry.
4. Provide a real-time executive dashboard accessible to Dean, Director of Research, VP Academic Affairs, and UD President.
5. Maintain a searchable, auditable historical record of all applications and their outcomes.
6. Support post-conference compliance tracking and reminders.

### 3.2 Success Metrics (KPIs)

| KPI | Baseline | Target (12 months post-launch) |
|---|---|---|
| Average approval cycle time | 10–15 working days | ≤ 3 working days |
| Manual data entry hours per application | ~45 minutes | 0 minutes |
| Application submission errors | ~30% (missing docs) | < 5% |
| PRF generation time | 30 minutes | < 5 minutes (auto-fill) |
| Management report generation | 4–8 hours manual | Real-time, self-service |
| Faculty satisfaction score | N/A | ≥ 4.2 / 5.0 |
| On-time post-conference compliance | ~60% (manual) | ≥ 90% |

---

## 4. Stakeholders & User Roles

### 4.1 Stakeholder Map

| Role | Access Level | Primary Responsibilities in CRS |
|---|---|---|
| **Faculty Member** | Applicant | Submit conference application, upload documents, track own requests, view PRF, complete post-conference checklist. |
| **College Dean** (Engineering & IT / Business / Law) | Approver — Level 1 | Review applications from own college, approve/reject/comment, view college-level dashboard. |
| **Director of Research** | Approver — Level 2 | Review all applications post-Dean, manage research committee stage, flag SCOPUS compliance. |
| **VP of Academic Affairs** | Approver — Level 3 | Final academic sign-off before President, view cross-college analytics. |
| **UD President** | Approver — Level 4 (Conference) / Level 5 (PRF) | Final approval, dashboard overview, digital signature, executive summary reports. |
| **Finance Department** | PRF Approver | Review and approve PRF budget lines, confirm budget availability, release funds. |
| **Procurement Department** | PRF Final Stage | Receive approved PRF, manage vendor and purchase order process. |
| **Research Committee** | Advisory | Add comments/pending issues before Dean stage (mirrors Stage II of Appendix I). |
| **System Administrator** | Admin | Manage users, roles, academic year configuration, notification templates, audit logs. |
| **HR Department** | Observer (limited) | Receive automated notifications for conference leave and advance forms. |

---

## 5. System Architecture Overview

### 5.1 Technology Stack Recommendations

| Layer | Technology / Approach |
|---|---|
| **Frontend** | React.js (TypeScript) with Tailwind CSS. Responsive design supporting desktop and tablet. Role-based UI rendering. |
| **Backend** | Node.js / Express.js REST API, or Django (Python) — to be confirmed with IT team. |
| **Database** | PostgreSQL — relational model for structured approval chains, audit logs, and form data. |
| **Authentication** | OAuth 2.0 / SAML 2.0 integration with existing UD Active Directory / Microsoft 365 SSO. MFA enforced for all approver roles. |
| **File Storage** | Supabase (or Azure Blob Storage) for uploaded documents. Version-controlled with access logs. |
| **Email Service** | Microsoft Exchange integration or SendGrid for automated notification emails with deep-link tokens. |
| **Digital Signature** | DocuSign API integration (or Adobe Sign) for binding electronic signatures on approval records. |
| **Hosting** | Azure Government / on-premise UD data centre per institutional policy. TLS 1.3 in transit, AES-256 at rest. |
| **Version Control** | GitHub (private repository under UD organisation). GitFlow branching strategy. |
| **CI/CD** | GitHub Actions for automated testing, linting, and deployment pipelines. |

### 5.2 Architecture Note

> The system follows a **three-tier architecture**: (1) a React SPA served via CDN / Azure Static Web Apps, (2) a stateless REST API layer with JWT token validation, and (3) a PostgreSQL database with read replicas for dashboard queries. All tiers are deployed within UD's private VNET with WAF protection.

---

## 6. Functional Requirements

### 6.1 Module 1: User Authentication & Profile Management

#### FR-AUTH-001 — Single Sign-On
Faculty and staff must authenticate via UD's existing **Microsoft 365 SSO**. No separate password registration. All roles are provisioned by the System Administrator.

#### FR-AUTH-002 — Role-Based Access Control (RBAC)
- Each user is assigned exactly one primary role (see Section 4). Roles determine visible menu items, accessible records, and available actions.
- Approvers can only see applications assigned to their approval stage.
- Faculty can only view and edit their own applications.
- Admins have read access to all records and write access to configuration tables.

#### FR-AUTH-003 — Faculty Profile Auto-Population
On first login, the system auto-populates the faculty profile from Active Directory:
- Full Name, Employee ID, College affiliation, Academic rank, Email address.
- Faculty confirm.

---

### 6.2 Module 2: Conference Application Form

#### FR-APP-001 — Form Sections

The digital application form captures all fields structured into logical sections:

| # | Section | Fields |
|---|---|---|
| **A** | Applicant Information | Full name (auto), Employee ID (auto), College (auto), Academic rank (auto), Contact email (auto), Submission date (auto). |
| **B** | Conference Details | Conference full name, Acronym, Website URL, Location (city & country), Start date, End date, Conference type (international/national) |
| **C** | Paper / Presentation Details | Paper title |
| **D** | Eligibility Checklist | Probationary period completed (Yes/No), First conference this academic year (Yes/No), "University of Dubai" appears in paper (Yes/No), Conference is peer-reviewed & SCOPUS-indexed (Yes/No). **All four must be Yes to proceed.** |
| **E** | Document Uploads | Acceptance letter/email (PDF, required), Conference paper draft (PDF, required), Conference registration form (PDF, optional), Conference agenda (PDF, optional), Proof of entry visa (if applicable). |
| **F** | Financial Estimate | Registration fee (AED), Flights (AED), Accommodation per night (AED), Number of nights, Per diems (AED), **Total (auto-calculated)**, Advance required (Yes/No), Substitution required (Yes/No). |
| **G** | Substitution & Leave | Substitution plan (text), Conference leave dates (date range), Substituting faculty member name. |

#### FR-APP-002 — Smart Validation
- Section D eligibility: if any answer is **"No"**, the form displays an inline warning and **prevents submission**, showing which requirement is unmet and the relevant policy reference.
- Conference dates must be in the future at time of submission.
- All required document uploads must be present before the Submit button is enabled.
- Financial totals auto-calculate in real time as fields are filled.

#### FR-APP-003 — Save as Draft
Faculty can save the form at any point and return to complete it. Drafts are retained for **90 days**. The system sends a reminder email at 7 days and 3 days before expiry.

#### FR-APP-004 — Application Reference Number
Upon submission, the system auto-generates a unique reference number in the format:

```
CRS-[YEAR]-[COLLEGE CODE]-[SEQUENTIAL NUMBER]
Example: CRS-2025-CEIT-0042
```

This reference is displayed prominently and included in all notification emails.

---

### 6.3 Module 3: Conference Approval Workflow

#### FR-WF-001 — Approval Chain Sequence

The approval workflow follows a strict **sequential chain**. Each stage must be completed before the next is triggered:

| Stage | Approver | SLA Target | Actions Available |
|---|---|---|---|
| **1** | Dean of College (CEIT / Business / Law) | 2 working days | Approve, Reject, Return to faculty with comments, Request additional information, Delegate to College Research Committee for advisory review. |
| **1A (Optional Advisory Stage)** | Research Committee (College-level Advisory Review) | 2 working days | Provide advisory feedback, Add recommendations, Highlight pending issues, Request clarifications through Dean. No direct approval/rejection authority. Request returns to Dean after review. |
| **1B (Post-Advisory Review)** | Dean of College (CEIT / Business / Law) | 2 working days | Review Research Committee feedback and proceed with: Approve, Reject, Return to faculty with comments, Escalate to Director of Research. |
| **2** | Director of Research | 2 working days | Approve, Reject, Return with comments, Request additional documents. |
| **3** | VP of Academic Affairs | 1 working day | Approve, Reject, Return with comments. |
| **4** | UD President | 1 working day | **Final Approve, Final Reject.** Digital signature captured. |

#### FR-WF-002 — Approver Actions

| Action | Description |
|---|---|
| **Approve** | Moves application to next stage. Captures approver name, digital signature, timestamp, and optional comments. |
| **Reject** | Terminates workflow. Faculty receives notification with rejection reason. Application is archived. |
| **Return for Revision** | Application sent back to faculty with specific comments. Faculty may update and resubmit. Revision history preserved. |
| **Request Information** | Approver posts a question to the faculty member without formally returning the form. Thread attached to application record. |
| **Delegate** | Approver may temporarily delegate authority to a named deputy. System logs the delegation with timestamps. |

#### FR-WF-003 — SLA Monitoring & Escalation
- At **50% of SLA elapsed**: reminder email sent to approver.
- At **100% of SLA elapsed**: escalation email sent to approver's direct superior. Dashboard flags application as **"Overdue"** in red.

#### FR-WF-004 — Comments & Audit Trail
Every action is recorded with: actor identity, timestamp, IP address, action type, and full comment text. This log is **immutable** and available to System Administrators and UD President.

#### FR-WF-005 — Notification Emails
All notification emails include: application reference number, applicant name, conference name, current stage, **direct deep-link URL** to the application in CRS, deadline reminder, and the university logo and footer.

---

### 6.4 Module 4: Purchase Requisition Form (PRF) Auto-Generation

#### FR-PRF-001 — PRF Category Selection

The PRF module supports four request categories:

| Category | Status | Notes |
|---|---|---|
| **Conference Registration** | ✅ Phase 1 focus | Auto-fill from approved conference application. |
| **Equipment** | 🔜 Available option | Manual entry of items, quantities, supplier recommendations. |
| **Visiting Faculty** | 🔜 Available option | Fields for visiting scholar details, accommodation, and honorarium. |
| **Other** | 🔜 Available option | Free-form description with standard approval chain. |

#### FR-PRF-002 — Auto-Population from Conference Application

Upon conference approval (President's signature), the system immediately creates a **draft PRF pre-filled** with:

| PRF Field | Source in Conference Application |
|---|---|
| Date | Auto: date of PRF creation |
| College / Support Department | Faculty profile — College affiliation |
| Requester Name | Faculty profile — Full name |
| Organisation Code | Mapped: "Research" (always for conference PRFs) |
| Purpose | Auto-text: `"Conference Registration — [Conference Name]"` |
| Item 1: Registration Fee | Section F — Estimated registration fee |
| Item 2: Flights | Section F — Estimated flights (AED) |
| Item 3: Accommodation | Section F — Estimated accommodation (total) |
| Item 4: Per Diems | Section F — Estimated per diems |
| Total Cost | Auto-calculated sum of all items |

#### FR-PRF-003 — Faculty Review of PRF
The faculty member receives a notification and is directed to **review the pre-filled PRF**. They may edit financial estimates if actual costs differ (with a mandatory explanation note). Once confirmed, the faculty member submits the PRF to begin the PRF approval chain.

#### FR-PRF-004 — PRF Approval Chain

| Stage | Approver | SLA Target | Notes |
|---|---|---|---|
| **1** | Dean of College | 1 working day | Budget awareness check. |
| **2** | Director of Research | 1 working day | Research funds confirmation. |
| **3** | VP of Academic Affairs | 1 working day | Academic alignment sign-off. |
| **4** | Finance Department | 2 working days | Budget availability check; may partially approve or adjust amounts. |
| **5** | UD President | 1 working day | Final binding approval with digital signature. |
| **6** | Procurement Department | N/A — notified | Receive approved PRF. Execute vendor engagement. Update purchase status in CRS. |

#### FR-PRF-005 — Quotation Attachment
Faculty or Finance may attach vendor quotations directly to the PRF record. The system tracks whether a quotation is attached and **requires quotation for any single item exceeding AED 5,000**.

---

### 6.5 Module 5: Dashboard & Analytics

#### FR-DASH-001 — Faculty Dashboard
- **My Applications**: list of all submitted applications with status badge.
  - Statuses: `Draft` · `Pending RC` · `Pending Dean` · `Pending Director` · `Pending VP` · `Pending President` · `Approved` · `Rejected` · `Returned`
- **Timeline view**: visual horizontal progress bar showing current stage and completed stages.
- **Notification centre**: in-app alerts for stage changes, approver comments, and PRF status.
- **Quick-action buttons**: Continue Draft, View Status, Download Approval Letter, View PRF.
- **Post-conference checklist**: reminder banner appears 7 days after expected return date.

#### FR-DASH-002 — Dean / Director / VP Dashboard
- Pending Approvals queue: sorted by submission date, flagged by SLA colour:
  - 🟢 Green = within SLA
  - 🟡 Amber = 50–100% of SLA elapsed
  - 🔴 Red = overdue
- College-level statistics: applications by status, by conference type, by faculty member, year-to-date.
- Budget summary: total estimated expenditure approved/pending for current academic year, broken down by college.
- Export to Excel / PDF at any time.

#### FR-DASH-003 — Executive Dashboard (VP + President)
- University-wide real-time counters: Total Applications YTD, Approved, Pending, Rejected, PRFs in process.
- **Interactive charts**:
  - Applications by college (pie chart)
  - Applications by month (bar chart)
  - Approval cycle time trend (line chart)
  - Top conferences by faculty count (ranked list)
  - Budget committed vs. spent (gauge)
- College comparison table: side-by-side view of all three colleges.
- Research output tracker: papers presented, by faculty, by conference, by SCOPUS status.
- Configurable date range filter (current academic year default).
- **One-click export**: formatted PDF executive summary report.

#### FR-DASH-004 — Finance Dashboard
- PRFs pending Finance approval with financial summaries.
- Budget consumption by college and by academic year.
- Committed vs. actual expenditure comparison (once Procurement closes the PO).

#### FR-DASH-005 — System Administrator Dashboard
- User management: add/edit/deactivate users, assign roles, manage delegation records.
- Workflow configuration: edit SLA thresholds, approval chain structure, notification templates.
- Audit log viewer: searchable, exportable log of all system events.
- Academic year management: open/close academic year cycle, archive old applications.

---

## 7. Post-Conference Compliance Module

### 7.1 Obligations Tracking

Once a conference attendance date has passed, the system automatically activates a **post-conference task list** for the faculty member:

| Obligation | Deadline | Evidence Required |
|---|---|---|
| Submit conference schedule showing faculty name and paper details to College Dean | 5 working days after return | Upload PDF / image |
| Submit copy of paper as published in conference proceedings to Library | 10 working days after return | Upload PDF |
| Provide copy of proceedings to College RC and UD-RC | 10 working days after return | Confirm in system (upload optional) |
| Submit actual expense receipts to Finance for settlement | 5 working days after return | Upload scanned receipts (if advance was issued) |
| Complete conference feedback/report form | 10 working days after return | Free-text field + optional upload |

### 7.2 Automated Reminders
- System sends email reminders at **D+3** and **D+7** for each incomplete obligation.
- If all obligations are not completed within **15 working days**, the Dean receives an automated alert.

---

## 8. Non-Functional Requirements

### 8.1 Performance
- Page load time ≤ **2 seconds** for all primary views on a standard university network (100 Mbps).
- Dashboard data refresh ≤ **5 seconds**.
- Form auto-save completes within **1 second** of field blur.
- System supports minimum **200 concurrent users** without degradation.

### 8.2 Security & Compliance
- All data encrypted in transit (**TLS 1.3**) and at rest (**AES-256**).
- Role-based data isolation: faculty cannot access other faculty records.
- All file uploads scanned for malware before storage.
- Session timeout: **30 minutes** for approver roles, **60 minutes** for faculty.
- Complete audit log retained for minimum **7 years**.
- Compliant with UAE data protection regulations and UD's Information Security Policy.
- OWASP Top 10 vulnerabilities addressed and verified by penetration testing prior to launch.

### 8.3 Availability & Reliability
- Target uptime: **99.5%** (excluding scheduled maintenance windows).
- Scheduled maintenance: Fridays 02:00–04:00 GST with at least 48 hours advance notice.
- Automated daily database backups with 30-day retention and tested restore procedure.
- Disaster recovery: **RTO ≤ 4 hours**, **RPO ≤ 1 hour**.

### 8.4 Usability & Accessibility
- Responsive design: fully functional on desktop (≥1024px) and tablet (768–1023px). Mobile read-only for status checking.
- **Arabic language support**: all UI text and email templates available in Arabic. RTL layout supported.
- **WCAG 2.1 Level AA** accessibility compliance.
- Inline contextual help text for every form field with reference to the relevant UD policy.
- Progress indicator on multi-section form showing completion percentage.

### 8.5 Integrations

| Integration | Purpose |
|---|---|
| **Microsoft 365 / Active Directory** | SSO authentication and automatic user profile population. |
| **Email (Exchange / SMTP)** | Transactional notification emails with deep-link tokens. |
| **DocuSign or Adobe Sign** | Binding e-signatures for approval records. |
| **Scopus API** *(future)* | Auto-verify conference SCOPUS indexing status. |
| **UD ERP / Finance System** *(future)* | Budget availability check and PO issuance integration. |

---

## 9. GitHub Repository Structure

### 9.1 Repository

```
github.com/university-of-dubai/conference-registration-system
```

### 9.2 Directory Layout

```
conference-registration-system/
│
├── README.md                        ← This file (PRD)
├── .gitignore
├── docker-compose.yml
├── .env.example
│
├── docs/
│   ├── PRD.md                       ← Full PRD (this document)
│   ├── architecture/
│   │   ├── system-diagram.png
│   │   └── database-erd.png
│   ├── api/
│   │   └── openapi.yaml             ← OpenAPI 3.0 specification
│   └── wireframes/
│       └── ...
│
├── frontend/                        ← React (TypeScript) application
│   ├── public/
│   ├── src/
│   │   ├── components/              ← Reusable UI components
│   │   ├── pages/
│   │   │   ├── ApplicationForm/     ← 7-section wizard
│   │   │   ├── Dashboard/           ← Faculty dashboard
│   │   │   ├── ApprovalQueue/       ← Approver queue view
│   │   │   ├── PRFModule/           ← PRF review and tracking
│   │   │   ├── PostConference/      ← Post-conference checklist
│   │   │   └── Admin/               ← System admin panel
│   │   ├── hooks/
│   │   ├── store/                   ← State management (Redux / Zustand)
│   │   ├── services/                ← API call functions
│   │   ├── types/                   ← TypeScript interfaces
│   │   └── utils/
│   ├── tailwind.config.js
│   └── package.json
│
├── backend/                         ← Node.js / Express API
│   ├── src/
│   │   ├── routes/
│   │   ├── controllers/
│   │   ├── models/
│   │   ├── middleware/
│   │   │   ├── auth.middleware.ts
│   │   │   ├── rbac.middleware.ts
│   │   │   └── audit.middleware.ts
│   │   ├── services/
│   │   │   ├── approvalWorkflow.service.ts
│   │   │   ├── prf.service.ts
│   │   │   ├── notification.service.ts
│   │   │   ├── signature.service.ts
│   │   │   └── audit.service.ts
│   │   └── utils/
│   └── package.json
│
├── database/
│   ├── migrations/                  ← Numbered SQL migration files
│   ├── seeds/                       ← Dev/test seed scripts
│   └── erd.png
│
├── infrastructure/
│   ├── terraform/                   ← Azure IaC scripts
│   ├── k8s/                         ← Kubernetes manifests
│   └── nginx/
│
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   ├── feature_request.md
│   │   └── security_vulnerability.md
│   └── workflows/
│       ├── lint.yml
│       ├── test.yml
│       ├── deploy-staging.yml
│       └── deploy-production.yml
│
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/                         ← Playwright end-to-end tests
│
└── scripts/
    ├── migrate-from-excel.js        ← Historical data import utility
    ├── seed-roles.js
    └── generate-test-data.js
```

### 9.3 Branching Strategy (GitFlow)

| Branch | Purpose |
|---|---|
| `main` | Production-ready code only. Protected — requires 2 approvals + passing CI before merge. |
| `develop` | Integration branch. All feature branches merge here first. |
| `feature/[ticket-id]-[description]` | Individual features. e.g. `feature/CRS-42-prf-autofill` |
| `hotfix/[description]` | Critical production bug fixes. Branch from `main`, merge back to both `main` and `develop`. |
| `release/[version]` | Release preparation. Version bumps, changelogs, final QA. |

### 9.4 GitHub Issues & Project Board

- **Labels**: `bug` · `feature` · `enhancement` · `documentation` · `security` · `ux`
- **GitHub Projects (Kanban)**: `Backlog → To Do → In Progress → In Review → Done`
- **Milestones**: map to 2-week sprint cycles and project phases
- **Issue templates**: Bug Report · Feature Request · Security Vulnerability (private)

---

## 10. Implementation Roadmap

| Phase | Scope | Duration | Key Deliverables |
|---|---|---|---|
| **Phase 0** — Discovery | Requirements validation, stakeholder interviews, data model design, UX wireframes, tech stack finalisation. | 4 weeks | Approved wireframes, ERD, finalised tech stack, signed-off PRD. |
| **Phase 1** — Foundation | SSO integration, user management, database setup, application form (Sections A–D), file upload, draft save, reference number generation. | 6 weeks | Working authentication, form submission to database, file storage. |
| **Phase 2** — Workflow Engine | Conference approval chain (all 5 stages), notification system, SLA monitoring, escalation logic, approver dashboard, faculty status view. | 6 weeks | End-to-end conference approval flow in staging environment. |
| **Phase 3** — PRF Module | PRF auto-population, PRF approval chain (6 stages), Finance dashboard, Procurement notification, quotation attachment. | 5 weeks | Working PRF workflow. Finance and Procurement access. |
| **Phase 4** — Dashboards & Analytics | Executive dashboard, college dashboards, charts, export (PDF/Excel), post-conference compliance module. | 4 weeks | Full dashboards. Post-conference checklists and reminders. |
| **Phase 5** — UAT & Launch | User Acceptance Testing, bug fixes, performance tuning, penetration test, Arabic localisation, go-live. | 4 weeks | Production-ready system. User training completed. |
| **Phase 6** — Post-Launch | Monitoring, feedback, Scopus API integration, ERP integration planning. | Ongoing | v1.1 enhancement releases. Integration roadmap. |

> **Total estimated timeline (Phases 0–5):** approximately **7–8 months** from project kick-off.  
> **Assumed team:** 1 Project Manager · 2 Frontend Developers · 2 Backend Developers · 1 DevOps Engineer · 1 QA Engineer.

---

## 11. Core Data Model (Entity Overview)

### 11.1 Key Entities

| Entity | Key Attributes |
|---|---|
| `users` | id, employee_id, full_name, email, role, college_id, is_active, created_at, last_login |
| `colleges` | id, name, code (CEIT/CB/CL), dean_user_id |
| `conference_applications` | id, reference_number, faculty_user_id, college_id, conference_name, start_date, end_date, paper_title, co_authors (JSONB), scopus_indexed, eligibility_flags (JSONB), financial_estimate (JSONB), status (ENUM), current_stage, academic_year |
| `application_documents` | id, application_id, document_type (ENUM), file_name, storage_path, uploaded_by, uploaded_at, is_current_version |
| `approval_records` | id, application_id, stage (ENUM), approver_user_id, action (ENUM: APPROVED/REJECTED/RETURNED/INFO_REQUEST), comment, signature_reference, timestamp, delegate_user_id |
| `prf_requests` | id, reference_number, application_id, category (ENUM), requester_user_id, purpose, items (JSONB array), total_amount, quotation_attached, status (ENUM), current_stage |
| `prf_approval_records` | id, prf_id, stage (ENUM), approver_user_id, action (ENUM), comment, adjusted_amount, signature_reference, timestamp |
| `post_conference_tasks` | id, application_id, task_type (ENUM), due_date, completed_at, evidence_path, is_compliant |
| `notifications` | id, user_id, type, reference_id, message, is_read, sent_at, email_sent_at |
| `audit_logs` | id, actor_user_id, action_type, entity_type, entity_id, old_value (JSONB), new_value (JSONB), ip_address, timestamp |

---

## 12. UI/UX Design Guidelines

### 12.1 Design Principles

| Principle | Description |
|---|---|
| **Clarity first** | Every screen must have one primary action. No hidden or ambiguous buttons. Status must always be visible. |
| **Trust through transparency** | Show the complete approval journey at all times. Faculty should never wonder "where is my application?" |
| **Reduce cognitive load** | Multi-section form with progress indicator. Auto-fill wherever possible. Inline validation — not end-of-form error dumps. |
| **Mobile-conscious** | Approvers often need to review on mobile. Approval actions must be accessible on a 375px-wide screen. |
| **Institutional identity** | Primary: UD Navy Blue `#1B3A6B`. Accent: UD Gold `#C8972A`. Professional aesthetic aligned with UD branding. |

### 12.2 Key Screens

1. Login page (SSO redirect, no password field)
2. Faculty home / My Applications dashboard
3. New Application Form (multi-step wizard, 7 sections, progress bar)
4. Application status detail view (timeline, comments thread, documents)
5. Approver queue view (filterable, sortable, SLA-highlighted list)
6. Single application review (read-only form + approve/reject/return actions in sticky footer)
7. PRF review and confirm (pre-filled editable form with change log)
8. PRF status tracker
9. Executive dashboard (charts, counters, college comparison)
10. Post-conference compliance checklist
11. System Admin panel (users, configuration, audit log)

---

## 13. Creative & AI Enhancement Suggestions

> These features go beyond replicating the current manual process and are recommended to make the CRS a strategic asset for research management at UD.

### 13.1 🤖 Intelligent Application Assistant
An AI-powered assistant that guides faculty during form completion:
- Suggests conference names from a curated database of SCOPUS-indexed conferences by discipline.
- **Flags predatory conferences** — integrates with Beall's List API to warn faculty before submission.
- Auto-suggests likely total cost based on destination country, historical UD conference data, and current flight price APIs.
- Offers a "Policy Check" button that summarises the relevant policy (R 10.3) in plain language.

### 13.2 ✅ Smart SCOPUS Verification
Integration with the Scopus API (or Scimago) allows **real-time conference indexing verification**. The application form displays a live badge:
- `✅ SCOPUS Verified` — green
- `❌ Not Found in SCOPUS` — red
- `⏳ Verification Pending` — amber

This prevents a common rejection reason before the form is submitted.

### 13.3 📊 Research Impact Tracker
A separate view (accessible to Director of Research and VP) that aggregates conference output into a **research impact profile**: papers per faculty, conference tier distribution (A\*, A, B), citations (future Scopus API link), and year-on-year growth in research activity. This data feeds directly into UD's QS and KHDA accreditation reporting.

### 13.4 📄 Automated Annual Research Report
At end of each academic year, the system **auto-generates a formatted PDF report**: "University of Dubai Annual Conference Activity Report" containing all approved conferences, total expenditure, faculty participation, and SCOPUS-indexed papers. This currently takes the research office several days to compile manually.

### 13.5 📅 Calendar Integration
Approved conference dates are automatically pushed to the faculty member's **Microsoft Outlook calendar**. The system also adds a blocked period to the Dean's team calendar for teaching coverage visibility. Substituting colleagues receive a calendar invite automatically.

### 13.6 💰 Budget Forecast Widget
Finance dashboard includes a forward-looking widget: based on pending applications and historical seasonal patterns, the system **projects end-of-year research travel expenditure**. Finance can set budget thresholds with automated alerts at 75% and 95% commitment.

### 13.7 🔗 QR Code on Approval Letter
The digitally signed approval letter (PDF) includes a **QR code** that links directly to the application record in CRS. Customs or conference organisers can verify the approval in real time. Eliminates the need to carry paper approval letters.

### 13.8 🔄 Smart Delegation & Out-of-Office Management
Approvers can configure automatic delegation rules:
> *"If I do not act within 48 hours, automatically delegate to [named deputy]."*

This prevents workflow stalls during annual leave or travel — a significant current pain point.

---

## 14. Risks & Mitigations

| Risk | Likelihood / Impact | Mitigation |
|---|---|---|
| Low user adoption among senior faculty unfamiliar with digital forms | Medium / High | Mandatory training workshop, video tutorials, faculty champions programme. Paper fallback for first 3 months with parallel running. |
| Active Directory / SSO integration delays | Medium / Medium | Begin SSO integration in Phase 0. Maintain email/password fallback for Phase 1 UAT. |
| Scope creep from stakeholders requesting new features mid-build | High / Medium | Strict change control process. New features logged in GitHub Issues and deferred to Phase 6 unless critical. |
| Data migration from Excel: inconsistent historical data | Medium / Low | Historical data imported as read-only archive. New system starts fresh from go-live date. |
| Approval chain bottlenecks persist (human behaviour, not system) | High / High | SLA monitoring with escalation. Management KPI dashboard makes bottlenecks visible to leadership. |
| DocuSign / Adobe Sign licensing cost exceeds budget | Low / Medium | Evaluate open-source e-signature alternatives (e.g., Documenso) as contingency. |
| Security breach or data leak | Low / High | Penetration testing pre-launch, MFA enforcement, role-based data isolation, WAF, monthly security reviews. |

---

## 15. Acceptance Criteria for Go-Live

The following criteria must all be met before production deployment:

- [ ] Faculty can submit a complete conference application with all required documents through the web portal.
- [ ] The application automatically triggers Stage RC notification to the Research Committee.
- [ ] Each approval stage correctly routes to the next approver upon approval, and notifies the faculty member.
- [ ] Rejection at any stage sends an email to the faculty with the reason and stops the chain.
- [ ] An approved conference application (President-signed) automatically creates a pre-filled PRF draft.
- [ ] The PRF approval chain routes through all 6 stages correctly.
- [ ] Executive dashboard displays real-time application counts, status breakdowns, and budget summaries.
- [ ] All notification emails contain correct content and direct deep-links.
- [ ] System supports Arabic language toggle across all major views.
- [ ] Load test confirms system performance with 200 concurrent users.
- [ ] Penetration test report issued with **no Critical or High severity findings**.
- [ ] User Acceptance Testing sign-off obtained from: Faculty representative, Dean, Director of Research, VP Academic Affairs, Finance, and IT.

---

## 16. Glossary

| Term | Definition |
|---|---|
| **CAO / Provost** | Chief Academic Officer / Provost — equivalent to VP of Academic Affairs in this document. |
| **CEIT** | College of Engineering & IT. |
| **CRS** | Conference Registration System — the platform described in this PRD. |
| **GitFlow** | A branching model for Git that defines a strict branching structure for project releases. |
| **KHDA** | Knowledge and Human Development Authority — Dubai's regulatory authority for higher education. |
| **MFA** | Multi-Factor Authentication. |
| **PRD** | Product Requirements Document. |
| **PRF** | Purchase Requisition Form — UD's standard form for initiating procurement. |
| **R 10.3** | UD Policy reference for Faculty Conference Attendance (Appendix I). |
| **RBAC** | Role-Based Access Control. |
| **RPO** | Recovery Point Objective — maximum acceptable data loss in a disaster. |
| **RTO** | Recovery Time Objective — maximum acceptable system downtime in a disaster. |
| **SCOPUS** | Elsevier's abstract and citation database; used as a conference quality benchmark at UD. |
| **SLA** | Service Level Agreement — the maximum time an approver should take to act. |
| **SSO** | Single Sign-On — one login credential (UD Microsoft 365) used across all systems. |
| **UAT** | User Acceptance Testing. |
| **VNET** | Virtual Network — an isolated private network in Azure. |
| **WAF** | Web Application Firewall. |
| **YTD** | Year-to-Date. |

---

## 17. Document Sign-Off

This document requires review and formal approval from the following stakeholders before development commences:

| Name & Title | Role in CRS | Signature | Date |
|---|---|---|---|
| Director of Research | Document Owner / System Sponsor | | |
| VP of Academic Affairs | Executive Sponsor | | |
| UD President | Final Approver | | |
| IT Director / CIO | Technical Authority | | |
| Dean, Engineering & IT | College Stakeholder | | |
| Dean, Business | College Stakeholder | | |
| Dean, Law | College Stakeholder | | |
| Finance Director | PRF Workflow Approver | | |

---

<div align="center">

**University of Dubai · Conference Registration System · PRD v1.0**

*Confidential — Internal Use Only*

</div>
