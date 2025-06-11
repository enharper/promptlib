**Auditor Feature: Guideline Uploader & Curator**

---

## Team
| Role | Name / Agent | Primary Responsibilities |
|------|--------------|--------------------------|
| Product Manager | **Eric Harper** | Vision, scope, prioritisation, cross-team alignment |
| Backend Engineer (Rails 8) | TBD | File storage, text-extraction pipeline, JSON guideline model, API |
| Frontend Engineer (Hotwire/Turbo + Tailwind/Flowbite) | TBD | Guideline curation UI, state management |
| ML / NLP Engineer | TBD (LLM “Extractor” agent) | Model prompt design, post-processing heuristics |
| QA Engineer | TBD | Test plans, fixture docs, end-to-end & cross-browser testing |
| Security & Compliance | TBD | Document-handling policies, PII redaction, HIPAA alignment |
| UX / UI Designer | TBD (or design-assist LLM) | User flows, empty-states, micro-copy |
| DevOps | TBD | Storage quotas, background workers, deployment gating |
| Documentation Writer | TBD (“DocsBot”) | Admin + end-user guides, API reference |

---

## Executive Summary
The **Auditor Guideline Uploader & Curator** lets Serva Tempus customers attach client-specific billing-guideline documents (PDF or Excel) to a client record. The platform automatically extracts individual rules into structured JSON. A new, lightweight curation UI allows users to deselect rules that are irrelevant to routine invoice audits (e.g., “Firm must notify in case of data breach”). The result is a clean, actionable ruleset used by the existing Auditor engine, improving audit accuracy, reducing false positives, and shortening onboarding from days to minutes.

---

## Business Goals / Key Benefit
| Goal | Target Impact | Measurement |
|------|---------------|-------------|
| **Reduce onboarding time** for a new client’s guidelines | ↓ from **3 days → < 2 hours** | Median time between “Upload” and “First successful audit” |
| **Increase audit precision** (fewer irrelevant flags) | ↓ false-positive rate **30 %** | % of audit flags overridden by users |
| **Boost customer satisfaction (CSAT)** | +15 pp on onboarding surveys | Average CSAT score post-onboarding |
| **Lower support load** related to guideline setup | −25 % support tickets | Ticket volume tagged “guideline extraction” |

---

## Background & Overview
Law-firm and ALSP clients supply billing guidelines in unstructured PDFs or Excel workbooks. Serva Tempus’ Auditor currently requires manual configuration of each rule in the app, a slow, error-prone task often delegated to our support team. Additionally, many clauses in these documents (security, reporting, marketing, etc.) are irrelevant to everyday billing audits, causing noise if blindly enforced.

The proposed feature automates extraction using an LLM-powered pipeline, then empowers users to **curate** the extracted rules with a few clicks—keeping invoice-related guidelines and discarding the rest.

**Technical context**

* Rails 8 monolith, PostgreSQL 15, Hotwire/Turbo, Tailwind + Flowbite  
* Solid Queue for background jobs (single-DB setup)  
* Storage: Active Storage on S3-compatible bucket  
* HIPAA-compliant, no data leaves the VPC except via OpenAI API with BAA  

---

## Scope & High-Level Requirements
| ID | Requirement / Use Case | Notes & Constraints |
|----|------------------------|---------------------|
| **R1** | User uploads PDF or XLS/XLSX to a Client record | ≤ 50 MB, virus-scanned, stored in S3 |
| **R2** | System extracts text & splits into discrete guideline candidates | OCR for scanned PDFs; tabular parser for Excel |
| **R3** | LLM classification → JSON output | Schema: `{id, text, category, severity?, applies_to_billing (bool)?, comments}` |
| **R4** | Present extracted guidelines in a paginated table with checkboxes | Hotwire partial updates; bulk-select; search/filter |
| **R5** | Default selection = “applies_to_billing” predictions; user can toggle | Persist interim selections in DB |
| **R6** | On “Save”, only selected guidelines become active audit rules | Create `BillingGuideline` records |
| **R7** | Version history & re-curation | Keep original upload + JSON; allow future edits |
| **R8** | Role-based permissions | Org admins & “Billing Analyst” role can upload/curate |
| **R9** | Error handling & notifications | Email + in-app toast on extraction failure |
| **R10** | Accessibility & keyboard navigation | WCAG 2.1 AA compliance |

---

## Out of Scope
* Automated mapping of guidelines to specific invoice line-item codes.  
* Support for image-only formats (TIFF, BMP).  
* Real-time co-editing by multiple users.  
* Bulk deletion of existing active guidelines (handled elsewhere).

---

## Risks of **Not** Doing This Project
| Risk | Likely Impact |
|------|--------------|
| Continued manual guideline entry | High onboarding cost; churn risk |
| Audit noise lowers trust | Users ignore flags, diminishing product value |
| Competitors launch similar automation | Loss of competitive edge in RFPs |
| Support team overload | Escalating COGS, slower response times |

---

## Success Criteria & Metrics
1. **Time-to-Audit**: median hours from guideline upload → first audit < 2 h  
2. **False-Positive Rate**: < 5 % of flags marked “not applicable” after curation  
3. **CSAT Onboarding Survey**: ≥ 90 % “satisfied” or higher  
4. **Extraction Precision/Recall**: P ≥ 0.85, R ≥ 0.90 on benchmark set  
5. **System Reliability**: < 1 % extraction job failures/operator intervention  

---

## Dependencies
* **OpenAI LLM API** quota (or Azure OpenAI) with JSON mode  
* **OCR service** (Tesseract container or AWS Textract)  
* **Role & permission** tables already in Serva Tempus  
* **Tailwind/Flowbite** upgrade for checkbox table components  
* **S3 lifecycle** rules for large uploads  

---

## Requested ETA
Pilot with two design-partner law firms by **August 15 2025**; GA by end of **Q3 FY25**.

---

## Deployment Plan
1. **Feature flag** `auditor_guideline_uploader`  
2. **Canary release** → staging → design partners → 10 % prod rollout  
3. Monitor job failure & API latency dashboards; progressive rollout  
4. Rollback via LaunchDarkly if extraction error rate > 5 %  

---

## Measurement & Feedback Loop
* Telemetry: `upload_started`, `extraction_complete`, `curation_saved`  
* Post-onboarding survey 24 h after first audit  
* Weekly metrics review in Product Ops dashboard (Looker)  
* In-app feedback widget on curation screen (“Was this helpful?”)  

---

## Go-To-Market (GTM)
* Beta outreach to customers with > 10 active clients  
* Blog post & webinar showcasing 90 % faster onboarding  
* Sales deck with before/after workflow screenshots  
* Updated SOC 2 report including document-processing controls  

---