# Conference Registration System (CRS)
## Faculty Member Complete Role & Flow Documentation

**System:** University of Dubai – Conference Registration System  
**Role:** Faculty Member (Applicant)  
**Document Version:** 1.0  
**Date:** May 2026

---

## Table of Contents
1. [Overview](#overview)
2. [Phase 1: Authentication & Profile Setup](#phase-1-authentication--profile-setup)
3. [Phase 2: Application Creation & Submission](#phase-2-application-creation--submission)
4. [Phase 3: Application Approval Workflow](#phase-3-application-approval-workflow)
5. [Phase 4: PRF Auto-Generation & Review](#phase-4-prf-auto-generation--review)
6. [Phase 5: Post-Conference Compliance](#phase-5-post-conference-compliance)
7. [Faculty Dashboard Features](#faculty-dashboard-features)
8. [Key Dates & SLAs](#key-dates--slas)
9. [Notifications & Communication](#notifications--communication)
10. [Common Scenarios & Resolution Paths](#common-scenarios--resolution-paths)

---

## Overview

The faculty member journey in the CRS consists of five major phases:

1. **Authentication & Setup** – SSO login with auto-populated profile
2. **Application Submission** – Multi-section form with smart validation
3. **Approval Tracking** – Four sequential approval stages with optional advisory review
4. **PRF Management** – Auto-generated purchase requisition form with faculty review
5. **Post-Conference Compliance** – Obligation tracking with automated reminders

**Total Timeline (typical):** 15–25 working days from submission to President approval + 10–15 working days for post-conference compliance

---

## Phase 1: Authentication & Profile Setup

### Overview
Faculty members access the CRS using their University of Dubai Single Sign-On (SSO) credentials via Microsoft 365. No separate password registration is required. On first login, their profile is automatically populated from Active Directory.

### Step-by-Step Process

| Step | Action | Details |
|------|--------|---------|
| 1.1 | Navigate to CRS Portal | Faculty visits the UD Conference Registration System URL |
| 1.2 | Click "Login with UD SSO" | Redirected to Microsoft 365 authentication page |
| 1.3 | Enter UD credentials | Username (email) and password; MFA may be required |
| 1.4 | Grant consent (if first-time) | Authorize CRS to access profile data from Active Directory |
| 1.5 | Profile auto-populated | System fetches: Full Name, Employee ID, College affiliation, Academic rank, Email |
| 1.6 | Review & Confirm Profile | Faculty reviews auto-filled data, makes any corrections (optional) |
| 1.7 | Proceed to Dashboard | Faculty is logged in and can access the home dashboard |

### Auto-Populated Profile Fields
- **Full Name** – From AD
- **Employee ID** – From AD
- **College Affiliation** – CEIT (College of Engineering & IT), Business, or Law
- **Academic Rank** – Professor, Associate Professor, Assistant Professor, Lecturer
- **Contact Email** – UD email address (from AD)

### Key Requirements
- MFA may be enforced for approver roles during login
- Session timeout: 60 minutes for faculty (30 minutes for approvers)
- All user roles are provisioned by System Administrator
- Faculty can only view and edit their own applications

---

## Phase 2: Application Creation & Submission

### Overview
Faculty complete a digital conference application form with seven logical sections. The form includes smart validation, auto-calculation of financial totals, and the ability to save as draft.

### Form Sections & Fields

#### **Section A: Applicant Information** (Auto-filled)
| Field | Source | Editable |
|-------|--------|----------|
| Full Name | AD | No |
| Employee ID | AD | No |
| College | AD | No |
| Academic Rank | AD | No |
| Contact Email | AD | No |
| Submission Date | System | No (auto-set on submit) |

#### **Section B: Conference Details** (Required)
| Field | Type | Constraints |
|-------|------|-------------|
| Conference Full Name | Text | Required, max 200 chars |
| Acronym | Text | Optional, max 50 chars |
| Website URL | URL | Required, must be valid URL |
| Location – City | Text | Required |
| Location – Country | Dropdown | Required |
| Start Date | Date | Required, must be future date |
| End Date | Date | Required, must be ≥ start date |
| Conference Type | Radio | International or National |

#### **Section C: Paper / Presentation Details**
| Field | Type | Constraints |
|-------|------|-------------|
| Paper Title | Text | Required, max 300 chars |

#### **Section D: Eligibility Checklist** ⚠️ **Critical**
All four questions must be answered **YES** to proceed. If any is **NO**, the form is locked and displays an error message with the reason and relevant policy reference (Policy R 10.3).

| Question | Answer | Failure Impact |
|----------|--------|-----------------|
| Probationary period completed? | Yes/No | If No → Cannot submit |
| First conference this academic year? | Yes/No | If No → Cannot submit |
| "University of Dubai" appears in paper? | Yes/No | If No → Cannot submit |
| Conference is peer-reviewed & SCOPUS-indexed? | Yes/No | If No → Cannot submit |

#### **Section E: Document Uploads** (Required)
| Document | Format | Required | Notes |
|----------|--------|----------|-------|
| Acceptance Letter/Email | PDF | ✅ Required | From conference organizers |
| Conference Paper Draft | PDF | ✅ Required | Full paper or extended abstract |
| Conference Registration Form | PDF | Optional | Conference-provided form |
| Conference Agenda | PDF | Optional | Program schedule |
| Proof of Entry Visa | PDF/Image | Conditional | Only if traveling to country requiring visa |

**Upload constraints:**
- Individual file size: max 10 MB
- Total upload size: max 50 MB
- All uploads scanned for malware before storage
- File versions tracked with upload timestamp

#### **Section F: Financial Estimate** (Required)
All amounts in AED (Arab Emirates Dirham)

| Item | Type | Auto-calculated |
|------|------|-----------------|
| Registration Fee | Currency | No (faculty enters) |
| Flights | Currency | No (faculty estimates) |
| Accommodation per night | Currency | No (faculty estimates) |
| Number of nights | Integer | No (faculty enters) |
| **Accommodation Total** | Currency | ✅ Yes (nights × per-night rate) |
| Per Diems | Currency | No (faculty enters) |
| **Grand Total** | Currency | ✅ Yes (sum of all items) |
| Advance Required? | Yes/No | No (faculty indicates) |
| Quotations Attached? | Yes/No | – (optional, required if item > AED 5,000) |

#### **Section G: Substitution & Leave**
| Field | Type | Constraints |
|-------|------|-------------|
| Substitution Plan | Text area | 200–500 chars, describes teaching coverage |
| Conference Leave – Start Date | Date | Required |
| Conference Leave – End Date | Date | Required, must be ≥ start date |
| Substituting Faculty Member Name | Dropdown / Text | Required, must be faculty from same college |

### Smart Validation Rules

The system performs real-time and pre-submission validation:

1. **Eligibility Validation** – If any Section D answer is "No", display inline warning with policy reference and prevent submission
2. **Date Validation** – Conference dates must be in the future; end date ≥ start date
3. **URL Validation** – Conference website must be a valid, reachable URL (optional check for malicious sites)
4. **Document Uploads** – All required documents must be present before Submit button is enabled
5. **Financial Auto-Calculation** – Accommodation total and grand total update in real-time as user enters values
6. **Quotation Check** – If any item > AED 5,000 and no quotation attached, warn but don't block (inform that Finance may request)

### Save as Draft

Faculty can save their progress at any point without submitting:

- **Draft retention:** 90 days from creation
- **Auto-delete:** After 90 days, draft is permanently deleted
- **Reminders:** System sends reminder emails at day 80 and day 85
- **Revision history:** Each save tracked with timestamp; faculty can view previous versions (future feature)

### Application Submission

#### Pre-Submission Checklist
- [ ] All required fields in Sections A–G are filled
- [ ] Eligibility Checklist (Section D) is all "YES"
- [ ] All required documents are uploaded
- [ ] Financial estimate is complete
- [ ] I have confirmed the substitution plan with my colleague

#### Submission Action
When faculty clicks **Submit**:

1. System validates all required fields and documents
2. If validation fails, error message displays which sections have issues
3. If validation passes:
   - Application status changes from "Draft" to "Pending RC" (Pending Research Committee, if advisory stage applies) or "Pending Dean" (if skipping RC)
   - **Application Reference Number** is auto-generated in format: `CRS-[YEAR]-[COLLEGE CODE]-[SEQUENTIAL #]`
     - Example: `CRS-2025-CEIT-0042`
     - CEIT = College of Engineering & IT
     - BUS = Business
     - LAW = Law
   - Faculty receives confirmation email with reference number, application summary, and link to view application
   - Application is routed to first approver (Dean or Research Committee, depending on college policy)
   - Faculty dashboard is updated with new application tile

#### Submission Confirmation Email
Faculty receives automated email containing:
- Application reference number (prominent)
- Applicant name and college
- Conference name and dates
- Total estimated cost
- Current approval stage
- Deep-link button to view application in CRS
- Deadline for first approver action
- Footer with UD logo and support contact

---

## Phase 3: Application Approval Workflow

### Overview
After submission, the application enters a four-stage approval chain, with an optional advisory stage (Research Committee review delegated by Dean). Each stage has a defined Service Level Agreement (SLA) and escalation triggers.

### Approval Chain Sequence

```
Stage 1: College Dean (2 days SLA)
  └─ Optional: Delegate to Research Committee (2 days advisory review)
     └─ Stage 1B: Dean reviews RC feedback
     
Stage 2: Director of Research (2 days SLA)

Stage 3: VP of Academic Affairs (1 day SLA)

Stage 4: UD President (1 day SLA) + Digital Signature

→ APPROVED: Auto-trigger PRF generation
→ REJECTED at any stage: Application archived, faculty notified
→ RETURNED: Sent back to faculty for revisions
```

### Stage-by-Stage Details

#### **Stage 1: College Dean Review**
| Attribute | Value |
|-----------|-------|
| **Approver** | Dean of faculty's college (CEIT, Business, or Law) |
| **SLA** | 2 working days |
| **Actions Available** | Approve, Reject, Return for revision, Request info, Delegate to RC |
| **Escalation** | At 50% SLA (1 day): Reminder email sent. At 100% SLA (2 days): Second reminder + flagged as "Urgent" in dashboard |

**Dean's Possible Actions:**

| Action | Outcome | Faculty Notification |
|--------|---------|---------------------|
| **Approve** | Application moves to Stage 2 (Director of Research) | Email: "Approved by [Dean Name] on [date]" with stage progress |
| **Reject** | Application archived, workflow stops | Email: Rejection reason + feedback + option to resubmit next cycle |
| **Return for Revision** | Sent back to faculty with specific comments | Email: "Returned for revision" + detailed feedback + link to edit + new submission deadline |
| **Request Information** | Post a question without formally returning; question thread attached to application | Email: "Additional information requested" + question + link to respond |
| **Delegate to RC** | Routes to Research Committee for advisory review (Stage 1A) | Email: "Delegated to Research Committee for advisory review" |

#### **Stage 1A: Research Committee Advisory Review** (Optional)
*Only if Dean delegated at Stage 1*

| Attribute | Value |
|-----------|-------|
| **Approver** | College-level Research Committee (5–7 faculty) |
| **SLA** | 2 working days |
| **Actions Available** | Provide feedback, add recommendations, highlight issues, request clarifications |
| **Authority** | Advisory only – no approval/rejection power |

**RC Responsibilities:**
- Review application for research merit and conference quality
- Flag if conference is not SCOPUS-indexed or has concerns
- Provide written feedback on research contribution
- Recommend approval or request Dean escalation to Director of Research
- Return application to Dean for final decision

#### **Stage 1B: Dean Review (Post-RC)**
*Only if RC advisory review was completed*

| Attribute | Value |
|-----------|-------|
| **Approver** | Same Dean from Stage 1 |
| **SLA** | 2 working days (fresh 2-day clock) |
| **Actions Available** | Review RC feedback → Approve, Reject, Return, Request info, Escalate to Director |

Dean reviews RC comments and makes final decision. If approving, moves to Stage 2. If escalating to Director, skips Stage 2 (unless Director sends back to Dean).

#### **Stage 2: Director of Research Review**
| Attribute | Value |
|-----------|-------|
| **Approver** | Director of Research (university-wide) |
| **SLA** | 2 working days |
| **Actions Available** | Approve, Reject, Return for revision, Request additional documents |
| **Focus** | SCOPUS compliance, research alignment with UD strategic goals |

**Possible Actions:** Same as Dean (Approve → Stage 3, Reject → End, Return → Back to faculty, Request Info → Question thread)

#### **Stage 3: VP of Academic Affairs Review**
| Attribute | Value |
|-----------|-------|
| **Approver** | VP of Academic Affairs (university-wide) |
| **SLA** | 1 working day |
| **Actions Available** | Approve, Reject, Return for revision |
| **Focus** | Cross-college alignment, workload impact, policy compliance |

**Note:** Shorter SLA. This is often a formality if earlier stages passed.

#### **Stage 4: UD President Final Approval**
| Attribute | Value |
|-----------|-------|
| **Approver** | UD President |
| **SLA** | 1 working day |
| **Actions Available** | **Final Approve** (with digital signature), **Final Reject** |
| **Authority** | Binding, irreversible |
| **Signature** | DocuSign or Adobe Sign integration – President's digital signature captured |

**Upon Final Approval:**
- Application status changes to "Approved"
- Faculty receives "Approval Letter" (PDF, digitally signed)
- PRF auto-generation is **immediately triggered** (see Phase 4)
- Email sent to faculty with approval letter attachment and link to PRF

### Application Status Badges (Faculty Dashboard)

| Status | Meaning | What Faculty Can Do |
|--------|---------|---------------------|
| **Draft** | Unsaved or saved but not submitted | Edit, continue, delete |
| **Pending RC** | Awaiting Research Committee advisory (if delegated) | View comments, respond if info requested |
| **Pending Dean** | Awaiting Dean approval at Stage 1 or 1B | View, check for updates |
| **Pending Director** | Awaiting Director of Research (Stage 2) | View |
| **Pending VP** | Awaiting VP of Academic Affairs (Stage 3) | View |
| **Pending President** | Awaiting President final approval (Stage 4) | View |
| **Approved** | President approved; PRF generation in progress | Download approval letter, review PRF |
| **Rejected** | Rejected at any stage; workflow ended | View rejection reason, optionally resubmit next cycle |
| **Returned** | Sent back for revision by approver | Edit form, provide additional documents, resubmit |

### SLA Monitoring & Escalation

The system actively monitors approval timelines:

- **At 50% SLA elapsed:** Reminder email sent to current approver
- **At 100% SLA elapsed:** 
  - Second reminder email to approver
  - Application flagged as **"Urgent"** (red) in approver's dashboard
  - VP of Academic Affairs and Director of Research receive escalation alert
  - Faculty receives notification that approval is delayed

**Example (Stage 1, 2-day SLA):**
- Day 0, 8:00 AM: Dean receives application
- Day 1, 8:00 AM: Reminder email sent (50%)
- Day 2, 8:00 AM: Second reminder + urgent flag (100%)

### Comments & Audit Trail

Every action in the workflow is recorded immutably:

| Captured Data | Details |
|---------------|---------|
| **Actor Identity** | Name, role, email of approver who took action |
| **Timestamp** | Date and time (to the second) |
| **IP Address** | Source IP for security audit |
| **Action Type** | Approve, Reject, Return, Request Info, Delegate |
| **Comments** | Full text of any feedback or questions |
| **Status Before/After** | Application status transition |

**Access:**
- Faculty can view a summary of comments and current stage
- System Administrator has full audit log access (immutable)
- UD President can view detailed audit trail for any application

### Workflow Termination

#### **Rejection** – Application ends immediately
- Faculty receives rejection email with reason and comments
- Application archived (no longer appears in active list but remains in historical records)
- Faculty may resubmit a new application in the next academic year
- Dean receives confirmation that rejection was recorded

#### **Return for Revision** – Application goes back to faculty
- Faculty receives "Returned" email with detailed feedback and specific requested changes
- Faculty can edit the application (all form sections remain accessible)
- System tracks revision version number (v1, v2, etc.)
- Faculty must resubmit within **14 calendar days** (or application expires and is archived)
- Resubmission re-enters the approval chain from Stage 1 or Stage 1B, depending on what stage returned it

---

## Phase 4: PRF Auto-Generation & Review

### Overview
Upon President approval of the conference application, the system automatically generates a pre-filled Purchase Requisition Form (PRF) based on the approved application data. Faculty reviews and confirms financial estimates, then submits the PRF to begin its own approval chain.

### PRF Auto-Generation Trigger

**Condition:** President clicks "**Final Approve**" on the conference application

**Timing:** Immediate (within seconds of President approval)

**What Happens:**
1. System creates new PRF record linked to the conference application
2. PRF is pre-populated with data from the approved application (see auto-fill mapping below)
3. PRF status set to "Draft – Faculty Review"
4. Faculty receives email notification: "Your PRF has been generated and is ready for review"
5. Email contains deep-link to PRF in CRS and summary of pre-filled amounts

### PRF Auto-Fill Mapping

| PRF Field | Source in Application | Example |
|-----------|----------------------|---------|
| **Date** | System | Today's date (date of PRF creation) |
| **College / Department** | Faculty profile | College of Engineering & IT |
| **Requester Name** | Faculty profile | Dr. Fatima Al-Mansouri |
| **Employee ID** | Faculty profile | EMP-004521 |
| **Organisation Code** | Fixed mapping | "Research" (for all conference PRFs) |
| **Purpose** | Auto-generated text | "Conference Registration – IEEE International Conference on AI Safety" |
| **Item 1 – Registration Fee** | Section F, field "Registration fee" | AED 3,500 |
| **Item 2 – Flights** | Section F, field "Flights" | AED 2,100 |
| **Item 3 – Accommodation** | Section F, calculated as "nights × per-night rate" | AED 1,800 (6 nights × 300) |
| **Item 4 – Per Diems** | Section F, field "Per diems" | AED 1,200 |
| **Total Cost** | Sum of items 1–4 | AED 8,600 |
| **Budget Code** | Mapped to college | Automatically selected |

### Faculty PRF Review

#### Step 1: Faculty Notified
Faculty receives email with subject: **"Your Conference PRF is Ready for Review – Action Required"**

Email includes:
- Conference name and dates
- Pre-filled PRF summary (each line item with amount)
- Total estimated cost
- Deep-link button: "Review PRF in CRS"
- Deadline to submit (typically 3 working days)

#### Step 2: Faculty Opens PRF in CRS

In the Faculty Dashboard, a new tile appears:
- Status badge: **"PRF – Awaiting Review"**
- Buttons: "Review PRF" | "Download PDF"

Faculty clicks **"Review PRF"** and sees:

- All auto-filled fields (read-only: date, college, requester, purpose)
- Editable financial line items
- Notes field for any changes or explanations
- Quotation upload section
- "Submit PRF" button (disabled until faculty confirms)

#### Step 3: Faculty May Edit Costs (Optional)

If actual quotes received or estimates change, faculty can:

**For each line item where cost differs:**
1. Click to edit the amount
2. Enter new amount
3. In the "Notes" field, type explanation: e.g., "Actual flight quote from Emirates is AED 2,250 instead of estimate"
4. System validates that new total is not exceedingly different from original (warning if > 20% variance, but allows override)

**Quotation Uploads:**
- If any single item > AED 5,000, quotation is recommended (or required, depending on finance policy)
- Faculty can upload vendor quotes (PDF, image, email screenshot) as evidence
- Quotations are viewable by Finance and President during PRF approval

#### Step 4: Faculty Confirms and Submits PRF

**Confirmation Checklist (in-app):**
- [ ] I have reviewed all financial estimates
- [ ] The amounts are reasonable and accurate
- [ ] I have added notes for any changes
- [ ] I have uploaded quotations for items > AED 5,000 (if applicable)

Once checked, **"Submit PRF"** button becomes enabled.

Faculty clicks **"Submit PRF"** → PRF enters the PRF Approval Chain (see below).

**Confirmation Email:**
Faculty receives: "Your PRF has been submitted for approval – Reference #PRF-2025-CEIT-0042"

---

### PRF Approval Chain

The PRF follows a **sequential 6-stage chain**, with Faculty review confirmation as a 7th (final) step.

#### **Stage PRF-1: Dean Review**
| Attribute | Value |
|-----------|-------|
| **Approver** | College Dean (same as conference Stage 1) |
| **SLA** | 1 working day |
| **Action** | Approve (budget awareness), Reject, Request revision |

**Dean's Check:** "Is this within my college's research budget allocation?"

#### **Stage PRF-2: Director of Research**
| Attribute | Value |
|-----------|-------|
| **Approver** | Director of Research |
| **SLA** | 1 working day |
| **Action** | Approve (research fund availability), Reject, Request revision |

**Director's Check:** "Are research funds available and properly allocated?"

#### **Stage PRF-3: VP of Academic Affairs**
| Attribute | Value |
|-----------|-------|
| **Approver** | VP of Academic Affairs |
| **SLA** | 1 working day |
| **Action** | Approve, Reject, Request revision |

**VP's Check:** "Is this academically justified and compliant with university policy?"

#### **Stage PRF-4: Finance Department**
| Attribute | Value |
|-----------|-------|
| **Approver** | Finance Director or Designated Approver |
| **SLA** | 2 working days |
| **Actions** | Approve, **Partially Approve** (adjust amounts), Reject, Request revision |
| **Special** | May adjust line item amounts if budget unavailable; must provide written explanation |

**Finance's Check:** "Is budget available? Are individual items reasonable? Are quotations sufficient?"

**Finance May:**
- Approve all items as-is
- Reduce one or more items if budget is tight (with explanation to faculty)
- Request additional quotations for large items
- Reject if total exceeds annual research travel budget

#### **Stage PRF-5: UD President**
| Attribute | Value |
|-----------|-------|
| **Approver** | UD President |
| **SLA** | 1 working day |
| **Actions** | **Final Approve** (digital signature), **Final Reject** |
| **Signature** | DocuSign or Adobe Sign capture |

**President's Final Check:** "Is this aligned with UD's strategic research priorities and budget constraints?"

#### **Stage PRF-6: Procurement Department**
| Attribute | Value |
|-----------|-------|
| **Approver** | Procurement Manager |
| **SLA** | N/A – Notified async |
| **Action** | Acknowledge receipt, initiate vendor engagement, create purchase orders |

**Procurement's Role:**
- Receives approved PRF notification
- Contacts vendors to confirm pricing and availability
- Arranges flights, accommodation, conference registration
- Updates PRF status with actual bookings
- Sends faculty updates on bookings (email notifications)

#### **Stage PRF-7: Faculty Confirmation (Post-Procurement)**
| Attribute | Value |
|-----------|-------|
| **Trigger** | Procurement completes bookings and updates PRF with final details |
| **Faculty Action** | Review procurement updates, accept or request modifications |
| **SLA** | 1 working day |

**Faculty Receives Email:** "Your conference travel has been booked – Please review and confirm"

**Procurement Details Shown:**
- Flight confirmation numbers and itinerary
- Hotel booking confirmation and address
- Conference registration confirmation
- Estimated total cost (may differ from PRF if vendor discounts applied)

**Faculty Can:**
- Click **"Accept"** – Confirms all bookings, PRF closes as "Approved & Booked"
- Click **"Request Modifications"** – Highlights specific issues; Procurement reassesses
- Add **"Comments"** – Questions or special requests before final closure

**Once Accepted:** PRF status → "**Approved & Finalized**" | Faculty is ready to travel

---

## Phase 5: Post-Conference Compliance

### Overview
Once the faculty member returns from the conference (after the end date has passed), the system automatically activates a post-conference compliance checklist. Faculty must complete five obligations within strict deadlines, with automated reminders.

### Compliance Obligations Tracking

System automatically activates on the day **after** the conference end date.

| # | Obligation | Deadline | Evidence Required | Notes |
|---|------------|----------|-------------------|-------|
| **1** | Submit conference schedule showing faculty name and paper details | 5 working days after return | PDF or image of official conference schedule | Proof that faculty participated and paper was presented |
| **2** | Submit copy of published paper to Library | 10 working days after return | PDF of full proceedings or published paper | Contributes to UD library digital collection |
| **3** | Provide copy of proceedings to College RC and UD RC | 10 working days after return | Can be same PDF as #2, or just confirm receipt | Documentation of research output |
| **4** | Submit actual expense receipts to Finance for settlement | 5 working days after return | Scanned receipts (PDF/image) – only if advance was issued | Receipts for flights, accommodation, meals, local transport, registration |
| **5** | Complete conference feedback/report form | 10 working days after return | Free-text form (500–1000 words) + optional supporting docs | Captures faculty's insights on conference value and research dissemination |

### Automatic Reminders

Faculty receives automated email reminders for **incomplete obligations:**

| Schedule | Trigger | Content |
|----------|---------|---------|
| **D+3** (3 days after conference end) | If any obligation incomplete | "Reminder: Three obligations due by [date]. Please upload your conference schedule, proceedings, and receipts." |
| **D+7** (7 days after conference end) | If any obligation incomplete | "Reminder: Your post-conference obligations are due within [3] days. Current status: [list incomplete items]" |
| **D+15** (15 days after conference end) | If ANY obligation still incomplete | Email sent to both faculty AND Dean: "Post-conference compliance incomplete. Faculty may be flagged for policy non-compliance." |

### Faculty Compliance Submission Process

#### Step 1: Access Compliance Dashboard
Faculty dashboard shows banner: **"Post-Conference Checklist – 5 tasks to complete by [date]"**

Clicking the banner opens a checklist view with:
- Progress bar (0/5 completed)
- Task list with individual upload fields
- Deadline dates highlighted
- Status badges: ⏳ Pending | ✅ Submitted | ⚠️ Overdue

#### Step 2: Submit Evidence for Each Obligation

**Obligation 1 – Conference Schedule:**
- Faculty uploads PDF/image
- System stores with timestamp
- Status → "✅ Submitted"

**Obligation 2 – Published Paper:**
- Faculty uploads PDF
- System stores with timestamp
- Library receives automated notification with download link

**Obligation 3 – Proceedings Copy:**
- Faculty can upload or simply check box: "Copy provided to College RC in person"
- If checked, timestamp recorded
- If upload, URL sent to College RC via email

**Obligation 4 – Expense Receipts:**
- Only required if faculty received advance payment
- Faculty can upload multiple files (scans of all receipts)
- Finance receives notification and reviews for reimbursement processing
- Optional note field: Faculty can highlight any missing receipts with explanation

**Obligation 5 – Feedback Report:**
- Text editor opens in-app
- Faculty types 500–1000 word reflection:
  - Key learnings from conference
  - How the research aligns with UD strategic goals
  - Networking or collaboration opportunities identified
  - Recommendations for future participation
- Optional file upload for supporting evidence (presentation slides, photos, certificates)
- Submit → Stored and sent to Director of Research

#### Step 3: Compliance Completion

Once all 5 obligations are submitted:
- Faculty receives confirmation email: "Post-conference compliance complete!"
- College Dean receives notification (for awareness)
- Finance receives notification (if receipts submitted, confirms reimbursement processing has begun)
- Application status changes to **"Closed – Compliant"**
- Compliance date recorded in system

#### Compliance Failure / Non-Compliance

If faculty **does not complete** obligations by D+15:
- Faculty flagged in system as "Non-Compliant"
- Dean receives escalation alert
- Automatic email to faculty: "Post-conference obligations are overdue. Failure to comply may affect eligibility for future conferences."
- HR Department may be notified (depending on institutional policy)

**Faculty can still submit late:** Up to 30 days after conference end date, with explanation noted in system.

---

## Faculty Dashboard Features

### Overview
The Faculty Dashboard is the central hub where faculty manage all their applications and track progress through the CRS workflow.

### Dashboard Sections

#### **1. My Applications**
**View:** Card-based list of all submitted applications (most recent first)

**For Each Application Card:**
- Conference name (large, clickable)
- Application reference number (CRS-2025-CEIT-0042)
- Status badge with color:
  - 🔵 Blue: Pending approval
  - 🟢 Green: Approved
  - 🔴 Red: Rejected
  - 🟡 Yellow: Returned / Requires action
- Current stage (e.g., "Pending VP of Academic Affairs")
- Submission date and approver names
- Quick-action buttons:
  - **View Status** – See detailed timeline
  - **Edit** (if in Draft or Returned status)
  - **Download Approval Letter** (if Approved)
  - **View PRF** (if PRF generated)

**Filters & Search:**
- Filter by status (Draft, Pending, Approved, Rejected, Returned)
- Filter by academic year
- Search by conference name or reference number
- Sort by submission date or status

#### **2. Timeline View**
**Purpose:** Visual representation of application progress through approval stages

**Display Format:** Horizontal progress bar showing:
- Completed stages (filled, green checkmarks)
- Current stage (highlighted, blue)
- Remaining stages (empty circles)
- SLA elapsed time (progress indicator within current stage)

**Example (Application at Stage 3: VP Review):**
```
[✅ Dean (2 days)] → [✅ Director (2 days)] → [● VP (1 day)] → [○ President]
                                                    60% complete
```

**Interactive:** Click any stage to view:
- Approver name and title
- Approval date/time (if completed)
- Comments left by approver
- SLA status (on time or overdue)

#### **3. Notification Centre**
**Purpose:** In-app alerts for status changes and action items

**Alerts Include:**
- Stage transitions ("Your application has been approved by the Dean and is now pending Director review")
- Approver comments ("Dean returned your application for revision – see feedback")
- PRF updates ("Your PRF has been generated and is ready for review")
- Compliance reminders ("Post-conference obligations – 3 tasks pending")
- SLA warnings ("Your application approval is approaching deadline – estimated resolution in 1 day")

**Notification Types:**
- 🔔 In-app banner (dismissible)
- 📧 Email notification (with deep-link)
- 📱 Mobile push notification (if mobile app enabled)

**Marked as Read:** Faculty can dismiss notifications; they remain in activity log

#### **4. Quick-Action Buttons**
**Visible by Application Status:**

| Status | Buttons |
|--------|---------|
| **Draft** | Edit | Delete | Continue Draft | Save as Completed |
| **Pending [Stage]** | View Status | Track Progress | View Comments | Download Partial PDF |
| **Returned** | Edit Form | View Feedback | Resubmit | Request Clarification |
| **Approved** | Download Approval Letter | View PRF | Print | Email to Self |
| **Rejected** | View Rejection Reason | Resubmit Next Year | Contact Dean |

#### **5. Post-Conference Checklist Banner**
**Appears:** 7 days after conference end date

**Banner Shows:**
- Checklist progress: "3 of 5 tasks complete"
- Time remaining: "Due in 7 days"
- Quick-upload buttons for each obligation
- Current status of each item (⏳ Pending | ✅ Submitted | ⚠️ Overdue)

**Click Banner:** Opens full compliance view (see Phase 5 details above)

#### **6. PRF Status Tracker** (when applicable)
**Shows:** Current PRF approval status through all 6 stages

**Visual:** Similar to application timeline, but shows PRF-specific stages:
```
[✅ Dean (1 day)] → [✅ Director (1 day)] → [● Finance (2 days)] → [○ President] → [○ Procurement]
                                                   Status: Received, reviewing...
```

**Current Stage Details:**
- Approver name
- Time in current stage
- Any comments or requests for revision
- Estimated completion date (based on SLA)

---

## Key Dates & SLAs

### Application Approval SLAs

| Stage | Approver | SLA | Escalation Point | Escalation Action |
|-------|----------|-----|------------------|-------------------|
| **1** | College Dean | 2 working days | 1 day (50%) | Reminder email |
| **1A** | Research Committee (if delegated) | 2 working days | 1 day (50%) | Reminder email |
| **1B** | College Dean (post-RC) | 2 working days | 1 day (50%) | Reminder email |
| **2** | Director of Research | 2 working days | 1 day (50%) | Reminder email |
| **3** | VP of Academic Affairs | 1 working day | 12 hours (50%) | Reminder email |
| **4** | UD President | 1 working day | 12 hours (50%) | Urgent flag + escalation alert |

**Note:** Working days = Monday–Friday, excluding UAE public holidays

**Target Total Cycle Time:** 7–10 working days (if no returns or rejections)

### PRF Approval SLAs

| Stage | Approver | SLA |
|-------|----------|-----|
| **PRF-1** | College Dean | 1 working day |
| **PRF-2** | Director of Research | 1 working day |
| **PRF-3** | VP of Academic Affairs | 1 working day |
| **PRF-4** | Finance Department | 2 working days |
| **PRF-5** | UD President | 1 working day |
| **PRF-6** | Procurement | N/A (async notification) |
| **PRF-7** | Faculty Confirmation | 1 working day |

**Target Total PRF Cycle Time:** 8–10 working days

### Post-Conference Compliance Dates

| Obligation | Deadline (from conference end date) | Notes |
|------------|-----------------------------------|-------|
| Conference schedule | 5 working days | Hard deadline |
| Receipts (if advance issued) | 5 working days | Hard deadline |
| Published paper to Library | 10 working days | Soft deadline (can be extended by Director) |
| Proceedings copy | 10 working days | Can be submitted in-person; no document needed |
| Feedback report | 10 working days | Soft deadline |
| **All obligations complete** | **15 working days** | After this, Faculty flagged as Non-Compliant |

---

## Notifications & Communication

### Notification Types & Channels

#### **Email Notifications** (Primary)
**Recipient:** Faculty's UD email address (from AD)

**Occasions & Content:**

| Occasion | Subject | Content Summary | Includes Deep-Link? |
|----------|---------|-----------------|---------------------|
| Application submitted | "Application Received – [Ref #]" | Confirmation, summary, next steps | Yes, to application |
| Approved by stage | "[Stage]: Approved – Next step is [Stage]" | Approver name, date, next deadline | Yes, to application |
| Rejected | "Application Rejected" | Rejection reason, feedback, resubmission info | Yes, to feedback |
| Returned for revision | "Returned for Revision – [Ref #]" | Detailed feedback, required changes, deadline | Yes, to edit form |
| Information requested | "Additional Information Requested" | Question from approver, link to respond | Yes, to Q&A thread |
| PRF generated | "Your PRF is Ready for Review" | Summary of pre-filled amounts, review deadline | Yes, to PRF |
| PRF approved | "PRF Approved – Awaiting Procurement" | PRF status, next steps | Yes, to PRF |
| Procurement bookings | "Your Conference Travel is Booked" | Flight/hotel confirmations, contact info | Yes, to PRF details |
| Post-conf reminder | "Post-Conference Obligations – Reminder" | List of pending tasks, upload links, deadline | Yes, to compliance checklist |
| SLA escalation | "Approval Delayed – Action Recommended" | Current stage, elapsed time, expected delay | Yes, to application |
| Compliance deadline | "Compliance Deadline Approaching" | Days remaining, incomplete items | Yes, to compliance checklist |

**Email Design Standards:**
- University of Dubai header (logo, color scheme)
- Clear, concise subject line with reference number
- Greeting with faculty name
- Body text in plain English (Arabic available as option)
- Prominent call-to-action button (e.g., "Review Application")
- Footer with: UD footer, support email, help documentation link
- Mobile-responsive design

#### **In-App Notifications**
**Location:** Notification Centre in Faculty Dashboard

**Display:** 
- Bell icon with unread count badge
- Dismissible banner at top of page (for urgent items)
- Chronological list in Notification Centre sidebar

**Persistence:** Remain in history for 90 days; older notifications archived

#### **SMS Notifications** (Optional)
**Triggered:** Only for critical SLA escalations (if enabled by admin)

**Example:** "Your CRS application approval is delayed. Please log in to check status. [Link]"

#### **Mobile Push Notifications** (Future)
**If mobile app deployed:** Push alerts for status changes and urgent reminders

---

## Common Scenarios & Resolution Paths

### Scenario 1: Application Validation Fails at Submission

**Situation:**
Faculty completes form but clicks Submit. System returns error: "Eligibility Checklist: 'SCOPUS-indexed' must be Yes to proceed."

**Resolution Path:**
1. Faculty reviews error message (highlighted in red)
2. Faculty navigates back to Section D (Eligibility Checklist)
3. Faculty confirms with conference organizers whether conference is SCOPUS-indexed
4. If YES: Updates answer to "Yes" and resubmits
5. If NO: Conference is ineligible; faculty cannot submit (must choose different conference or policy changes)

**System Support:**
- Error message includes policy reference: "See Policy R 10.3 for SCOPUS requirements"
- Help icon next to question links to policy in plain language
- Suggested alternatives shown: "Popular SCOPUS-indexed conferences in your discipline"

---

### Scenario 2: Application Returned by Dean for Revision

**Situation:**
Faculty receives email: "Application Returned for Revision" with feedback: "Please update financial estimate – flights seem underestimated for [destination]."

**Resolution Path:**
1. Faculty receives email with link to application
2. Faculty logs into CRS, sees status badge: "🟡 Returned – Revision Required"
3. Faculty views approver feedback in "Comments" section
4. Faculty clicks "Edit Application"
5. Faculty revises Section F (Financial Estimate), changing flights from AED 1,800 to AED 2,400
6. Faculty adds note in "Revision Comments" field: "Updated based on current Emirates pricing; attached new quote."
7. Faculty uploads new flight quotation (PDF)
8. Faculty clicks "Resubmit"
9. Application re-enters workflow at Stage 1 (Dean again) with v2 notation
10. Dean receives notification: "Application [Ref#] v2 resubmitted for review"
11. Faculty receives confirmation email

**Timeline:** Faculty must resubmit within 14 calendar days or application expires.

---

### Scenario 3: Application Stuck in Approval (Overdue SLA)

**Situation:**
Faculty submitted application 3 working days ago; status still shows "Pending Dean" (SLA was 2 days).

**Resolution Path:**
1. Faculty dashboard shows SLA status: "🔴 Overdue – 1 day past deadline"
2. Faculty can click "Request Escalation" button
3. System sends email to Dean's supervisor and VP: "Application [Ref#] is overdue – escalation requested"
4. Faculty receives confirmation: "Escalation requested – VP has been notified"
5. VP may contact Dean directly to unblock
6. Within 1 business day, Dean typically approves or provides feedback

**Prevention:** System automatically escalates at 100% SLA without faculty action, but faculty can manually request escalation anytime.

---

### Scenario 4: Finance Partially Approves PRF (Budget Constraints)

**Situation:**
PRF for AED 8,600 reaches Finance. Finance review shows only AED 7,000 is available in college research budget. Finance partially approves.

**Resolution Path:**
1. Faculty receives email: "PRF – Partial Approval by Finance"
2. Email shows:
   - Item 1 (Registration): AED 3,500 ✅ Approved
   - Item 2 (Flights): AED 2,100 ✅ Approved
   - Item 3 (Accommodation): AED 1,800 ⚠️ Reduced to AED 1,200 (Finance note: "Choose 4-night accommodation instead of 6-night")
   - Item 4 (Per Diems): AED 1,200 ❌ Removed
   - **Revised Total:** AED 7,800 (still exceeds budget slightly)

3. Faculty receives notification: "Your PRF requires revision – Finance has adjusted amounts due to budget constraints. Review and respond."
4. Faculty can:
   - **Accept the reduction:** Click "Accept Revised PRF" → Moves to VP stage
   - **Request partial funding from personal budget:** Click "Negotiate" → Opens messaging thread with Finance Director → Finance can increase allocation if justified
   - **Withdraw conference application:** Not recommended, but an option

5. If Faculty negotiates, Finance responds within 2 working days
6. If Finance increases allocation, PRF moves forward. If not, Faculty either accepts reduced funding or withdraws.

---

### Scenario 5: Faculty Returns Late from Conference; Post-Compliance Tasks Overdue

**Situation:**
Faculty returns from conference on the 15th but was delayed and only submits compliance documents on day 18. System flags as "Overdue."

**Resolution Path:**
1. Faculty sees notification: "Post-Conference Obligation Overdue – Submit documentation"
2. Faculty uploads receipts with note: "Delayed return from conference due to flight cancellation; submitting receipts now."
3. System records submission with timestamp
4. Finance receives notification but understands the delay
5. Director of Research receives Dean alert but is aware of the reason
6. Compliance status: "Submitted (Late)" with explanation flag
7. No penalty if reason is documented and reasonable (e.g., flight delay, illness)
8. If no explanation and >30 days late: Faculty flagged as Non-Compliant; may affect future conference eligibility

**Prevention:** Faculty can pre-emptively email Dean/Finance if delay is foreseen, with expected submission date.

---

### Scenario 6: PRF Created but Faculty Realizes Cost Estimate is Wrong

**Situation:**
PRF is pre-filled with AED 2,100 for flights, but faculty just received a quote for AED 2,900. Faculty needs to correct before Finance reviews.

**Resolution Path:**
1. PRF status: "Draft – Faculty Review" (not yet submitted to Dean)
2. Faculty logs into PRF view
3. Faculty clicks "Edit" on Flights line item
4. Faculty changes amount from AED 2,100 to AED 2,900
5. Faculty enters note: "Actual quote from Emirates attached. Flight dates: [dates]. Seat selection and baggage included."
6. Faculty uploads quotation PDF
7. Faculty clicks "Update Total" (system recalculates to AED 9,300)
8. Faculty can add override explanation: "Higher cost due to limited availability for conference dates and required departures."
9. Faculty reviews all items and notes
10. Faculty clicks "Submit PRF for Approval"
11. Dean receives PRF (revised total) with faculty explanation
12. PRF continues through approval chain

**Key:** Faculty can edit costs anytime before submitting to first approver (Dean). Once submitted, costs become locked; further edits require approval chain reversal (for now; future versions may allow more flexibility).

---

## Additional Features & Future Enhancements

### Current Phase 1 Features
- ✅ Application form with 7 sections
- ✅ Smart validation and eligibility checks
- ✅ Multi-stage approval workflow (4 stages + optional RC advisory)
- ✅ Auto-generated PRF from approved application
- ✅ Faculty PRF review and cost editing
- ✅ PRF approval chain (6 stages)
- ✅ Post-conference compliance tracking with reminders
- ✅ Faculty dashboard with application list, timeline, notifications
- ✅ SLA monitoring and escalation
- ✅ Audit trail and digital signatures

### Planned Phase 2+ Enhancements

#### **AI-Powered Intelligent Assistant**
- Suggests SCOPUS-indexed conferences by discipline
- Flags predatory conferences (integrates with Beall's List)
- Auto-suggests cost estimates based on historical data and flight price APIs
- Policy checker button for instant Policy R 10.3 summary

#### **Smart SCOPUS Verification**
- Real-time badge showing SCOPUS indexing status:
  - ✅ SCOPUS Verified (green)
  - ❌ Not Found (red)
  - ⏳ Verification Pending (amber)
- Prevents rejection at Director stage due to missing SCOPUS evidence

#### **Research Impact Tracker**
- Dashboard showing faculty papers presented, conference tiers (A*, A, B)
- Citation tracking (future Scopus API integration)
- Year-on-year growth analytics
- Feeds into UD QS/KHDA accreditation reporting

#### **Automated Annual Research Report**
- System auto-generates PDF: "UD Annual Conference Activity Report"
- Includes: all approved conferences, total expenditure, faculty participation, SCOPUS papers
- Currently takes research office 3+ days; system will generate in minutes

#### **Calendar Integration**
- Approved conference dates pushed to faculty's Outlook calendar
- Substitute colleague automatically invited to calendar block
- Dean's team calendar updated for teaching coverage visibility

#### **Budget Forecast Widget**
- Finance dashboard shows forward-looking projection
- Based on pending applications + historical patterns
- Alerts at 75% and 95% annual budget commitment

#### **QR Code on Approval Letter**
- Digitally signed approval letter includes QR code
- QR links to live application record in CRS
- Customs/conference organizers can verify in real-time
- Eliminates need to carry paper letter

#### **Smart Delegation & Out-of-Office Management**
- Approvers set rules: "If I don't act within 48 hours, delegate to [deputy]"
- Prevents workflow stalls during annual leave/travel
- Automatic escalation with delegation audit trail

---

## Support & Help Resources

### Faculty Help Documentation
- **Video tutorials:** 5–10 minute walkthroughs for each phase (available in English & Arabic)
- **FAQ guide:** Common questions and troubleshooting
- **Policy reference:** Inline links to Policy R 10.3 and UD conference travel guidelines
- **Contact support:** helpdesk@ud.ae | CRS Support Portal (in-app)

### Training & Onboarding
- Mandatory 30-minute workshop for all new faculty (recorded, available on-demand)
- College Dean's office provides local guidance
- System Administrator available for role-based queries

### Feedback & Improvement
Faculty can submit feedback via in-app "Report Issue" button → CRS support team triages and prioritizes

---

## Summary

The Faculty Member's journey through the Conference Registration System is structured to be **efficient, transparent, and compliant**:

1. **Simple onboarding** via SSO with auto-populated profile
2. **Guided form submission** with smart validation and draft saving
3. **Visible approval workflow** with SLA tracking and escalation
4. **Automated PRF generation** reducing manual data entry
5. **Post-conference accountability** with timely reminders
6. **Transparent dashboard** showing all applications and status at a glance

**Expected outcome:** From application submission to President approval: **7–10 working days** (vs. 10–15 days in manual process)

**Faculty satisfaction goal:** ≥ 4.2 / 5.0

---

**End of Faculty Complete Flow Documentation**

*For questions or clarifications, contact: CRS Support – helpdesk@ud.ae*
