# Faculty Member Flow - Conference Registration System
## University of Dubai

---

## 5-Phase Journey

1. **Phase 1:** Authentication & Profile Setup
2. **Phase 2:** Application Creation & Submission (with validation)
3. **Phase 3:** Application Approval Workflow (4 stages + optional RC advisory)
4. **Phase 4:** PRF Auto-Generation & Review
5. **Phase 5:** Post-Conference Compliance

---

## Complete Flow Diagram

```
┌─────────────────────────────────────────────────────────────────────────┐
│ PHASE 1: AUTHENTICATION & PROFILE SETUP                                 │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
                        Faculty logs in via SSO
                                    │
                                    ▼
                    Profile Auto-Populated from AD
                    (Name, ID, College, Email)
                                    │
                                    ▼

┌─────────────────────────────────────────────────────────────────────────┐
│ PHASE 2: APPLICATION CREATION & SUBMISSION                              │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
        Complete 7-Section Application Form
  • Applicant Info • Conference Details • Paper Details
  • Eligibility Checklist • Document Uploads
  • Financial Estimate • Substitution & Leave
                                    │
                                    ▼
                        Smart Validation Check
                    (Eligibility: All 4 must be YES)
                                    │
                    ┌───────────────┴───────────────┐
                    │                               │
                VALIDATION FAILS            VALIDATION PASSES
                    │                               │
                    ▼                               ▼
              Fix Errors & Resubmit         Submit Application
                    │                    (Reference # Generated)
                    │                               │
                    └───────────────┬───────────────┘
                                    │
                                    ▼

┌─────────────────────────────────────────────────────────────────────────┐
│ PHASE 3: APPLICATION APPROVAL WORKFLOW (7-10 Working Days)              │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
                    ┌────────────────────────────┐
                    │  STAGE 1: COLLEGE DEAN     │
                    │  SLA: 2 working days       │
                    └────────────────────────────┘
                                    │
                    ┌───────────────┼───────────────┐
                    │               │               │
                APPROVED       REJECTED         DELEGATED
                    │               │           TO RC COMMITTEE
                    │               │               │
                    │               │               ▼
                    │               │   ┌─────────────────────────┐
                    │               │   │ STAGE 1A: RC ADVISORY   │
                    │               │   │ SLA: 2 working days     │
                    │               │   │ (Feedback only)         │
                    │               │   └─────────────────────────┘
                    │               │               │
                    │               │               ▼
                    │               │   ┌─────────────────────────┐
                    │               │   │ STAGE 1B: DEAN REVIEW   │
                    │               │   │ (Post-RC Decision)      │
                    │               │   └─────────────────────────┘
                    │               │               │
                    │               ▼               │
                    │          [APPLICATION        │
                    │           ARCHIVED]          │
                    │                              │
                    └──────────────┬───────────────┘
                                   │
                                   ▼
                    ┌────────────────────────────┐
                    │ STAGE 2: DIRECTOR OF       │
                    │ RESEARCH                   │
                    │ SLA: 2 working days        │
                    └────────────────────────────┘
                                   │
                                   ▼
                    ┌────────────────────────────┐
                    │ STAGE 3: VP ACADEMIC       │
                    │ AFFAIRS                    │
                    │ SLA: 1 working day         │
                    └────────────────────────────┘
                                   │
                                   ▼
                    ┌────────────────────────────┐
                    │ STAGE 4: PRESIDENT FINAL   │
                    │ APPROVAL (Digital Sig)     │
                    │ SLA: 1 working day         │
                    └────────────────────────────┘
                                   │
                                   ▼
                            ✅ APPROVED
                                   │
                                   ▼

┌─────────────────────────────────────────────────────────────────────────┐
│ PHASE 4: PRF AUTO-GENERATION & REVIEW (8-10 Working Days)               │
└─────────────────────────────────────────────────────────────────────────┘
                                   │
                    PRF Auto-Generated (Immediate)
                    Pre-filled from Application Data
                                   │
                                   ▼
                    Faculty Reviews & May Edit Costs
                    (Add quotations if > AED 5,000)
                                   │
                                   ▼
                        Faculty Submits PRF
                                   │
        ┌─────────────────────────────────────────────────┐
        │         PRF APPROVAL CHAIN (6 STAGES)           │
        ├─────────────────────────────────────────────────┤
        │ Dean → Director → VP → Finance → President      │
        │              → Procurement → Faculty Confirmation│
        └─────────────────────────────────────────────────┘
                                   │
                                   ▼
                        ✅ PRF APPROVED
                    (Travel Bookings Confirmed)
                                   │
                                   ▼

┌─────────────────────────────────────────────────────────────────────────┐
│ PHASE 5: POST-CONFERENCE COMPLIANCE (15 Working Days)                   │
└─────────────────────────────────────────────────────────────────────────┘
                                   │
                (Activated Day After Conference Ends)
                                   │
        Faculty Completes 5 Obligations:
        1. Conference schedule with faculty name/paper
        2. Published paper copy to Library
        3. Proceedings copy to Research Committee
        4. Actual expense receipts to Finance
        5. Conference feedback/report form
                                   │
        Automated Reminders at D+3, D+7, D+15
                                   │
                                   ▼
                    ✅ COMPLIANCE COMPLETE
            (All obligations submitted by deadline)
                                   │
                                   ▼
                        Application Closed
                      Faculty Ready for Next Conference

```

---

## Key Timeline Summary

| Phase | Duration | Status |
|-------|----------|--------|
| **Phase 1** | Immediate | 1-time setup |
| **Phase 2** | 30–60 min | Faculty action |
| **Phase 3** | 7–10 working days | Approval chain |
| **Phase 4** | 8–10 working days | Faculty + PRF chain |
| **Phase 5** | 15 working days | Faculty compliance |
| **TOTAL** | ~20–25 working days | End-to-end |

---

## Expected Outcomes

✅ **Previous Manual Process:** 10–15 working days + extensive follow-up  
✅ **CRS System:** 7–10 working days + automated reminders  
✅ **Target:** Reduce approval cycle by 50% and eliminate manual errors

