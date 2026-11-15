# Curai Clinical Tools Suite

Curai organizes its clinical tools directly around the chronological journey of a medical encounter: **Before the Visit**, **During the Visit**, and **After the Visit**.

Rather than operating as fragmented single-purpose utilities, all six tools interface with **One Shared Longitudinal Patient Record**, ensuring that clinical context flows seamlessly across care transitions while adhering to strict safety boundaries.

---

## The Visit Lifecycle Architecture

```
                       PATIENT CARE JOURNEY
                               │
       ┌───────────────────────┼───────────────────────┐
       ▼                       ▼                       ▼
BEFORE THE VISIT        DURING THE VISIT         AFTER THE VISIT
┌──────────────┐      ┌─────────────────┐     ┌──────────────────────┐
│  DiagnoFast  │      │   ClinScribe    │     │Prescription Analyzer │
│ Voice intake │─────▶│  Ambient notes  │────▶│ Multilingual Rx guide│
│ Waiting kiosk│      │  SOAP generator │     │ 250k drug matching   │
│ Red-flag gate│      └────────┬────────┘     └──────────┬───────────┘
└──────────────┘               │                         │
                               ▼                         ▼
                      ┌─────────────────┐     ┌──────────────────────┐
                      │     LabLens     │     │     ReferralLoop     │
                      │ Diagnostic OCR  │     │ Closed-loop consults │
                      │ Analyte trends  │     │ Back-referral tracking
                      └─────────────────┘     └──────────┬───────────┘
                                                         │
                                                         ▼
                                              ┌──────────────────────┐
                                              │    DischargeCare     │
                                              │ Transition checklist │
                                              │ Inpatient task gates │
                                              └──────────────────────┘
```

---

## Tools Directory

| Tool | Encounter Phase | Primary Users | Detailed Documentation |
|---|---|---|---|
| **DiagnoFast** | Before the Visit | Patients, Triage Nurses, Reception | [Read DiagnoFast Guide](diagnofast.md) |
| **ClinScribe** | During the Visit | Clinicians, Attending Physicians, Scribes | [Read ClinScribe Guide](clinscribe.md) |
| **LabLens** | During the Visit | Pathologists, Clinicians, Patients | [Read LabLens Guide](lablens.md) |
| **Prescription Analyzer** | After the Visit | Patients, Family Caregivers, Pharmacists | [Read Prescription Analyzer Guide](prescription_analyzer.md) |
| **ReferralLoop** | After the Visit | Referring Physicians, Specialists, Care Teams | [Read ReferralLoop Guide](referralloop.md) |
| **DischargeCare** | After the Visit | Inpatient Teams, Family Caregivers, Care Coordinators | [Read DischargeCare Guide](dischargecare.md) |

---

## Core Safety & Architectural Principles Across All Tools

1. **AI Output Is Always a Draft**: No tool automatically commits unreviewed AI inferences into authoritative health records or FHIR bundles. Every extraction or summary exists in a pending state until authorized by a human.
2. **Deterministic Fallbacks**: Critical clinical rules (emergency red-flag symptoms, medical shorthand decoding, analyte reference interval bounds) are governed by deterministic, verifiable code rather than probabilistic LLMs.
3. **Cryptographic Provenance**: Every observation, note version, and confirmed medication retains full provenance—including author, reviewer, timestamp, and underlying source document citation.
4. **Data Minimization & Patient Consent**: Data extraction operates under purpose-bound consent. Voice recordings and transcripts are purged upon clinician sign-off unless research retention consent is explicitly granted.
