# Enterprise AI Court Case Triage & Governance

> **Portfolio Project | AI Product Operations · NLP · Responsible AI · Security · Privacy · Public Safety**

An executive-level AI product evaluation demonstrating how natural-language processing can support court case intake and routing while operating under the assumption that source records contain **highly sensitive judicial information**.

> **Portfolio data notice:** The public GitHub repository uses synthetic case records and contains no real court records or personally identifiable information. The architecture, security controls, privacy protections, governance framework, human-review mechanisms, and public-safety guardrails are intentionally designed as if the platform were processing restricted real-world court data.

## Executive Summary

Court operations teams review high volumes of incoming case records across criminal, civil, domestic/family, and administrative matters. Manual intake can be time-intensive and inconsistent, but judicial data cannot be treated like ordinary enterprise data.

This project evaluates AI-assisted case triage using a controlled operating model built around three non-negotiable criteria:

1. **Privacy** — minimize, classify, redact, and govern sensitive information before model inference.
2. **Security** — restrict access, prevent uncontrolled data egress, preserve auditability, and establish production security requirements.
3. **Public Safety** — prevent unsafe autonomous routing of high-risk matters and preserve human decision authority.

The system is designed as **decision support, not autonomous legal decision-making**.

## Business Objective

Evaluate whether AI can reduce repetitive case-intake review while maintaining appropriate controls for highly sensitive court information.

The project evaluates:

- case category and subcategory classification;
- TF-IDF + Logistic Regression baseline modeling;
- TF-IDF + Linear SVM specialized routing;
- BERT-style semantic benchmarking in shadow mode;
- sentiment/risk signals for operational prioritization only;
- PII/sensitivity detection and redaction;
- confidence-based escalation;
- mandatory human review for sensitive or high-risk cases;
- model monitoring, audit logging, and governance gates.

## Operating Architecture

```text
Case Intake
    ↓
Data Quality Validation
    ↓
Sensitive Data / PII Detection
    ↓
Redaction + Pseudonymization
    ↓
Approved NLP Models
    ↓
Confidence + Public-Safety Guardrails
    ↓
Human Review / Override
    ↓
Final Operational Routing
    ↓
Audit Log + Monitoring + Governance Review
```

## Privacy, Security & Public-Safety Guardrails

| Control Area | Guardrail |
|---|---|
| Data minimization | Only fields required for the defined routing use case are processed |
| PII protection | Sensitive fields are detected, redacted, or pseudonymized before modeling |
| Data egress | Modeling is designed for controlled/local processing; unapproved external model calls are prohibited |
| Access control | Production design requires role-based access, SSO/MFA, least privilege, and access recertification |
| Encryption | Production design requires encryption in transit and at rest |
| Secrets | Credentials and keys must be stored outside source code and repositories |
| Sensitive-case handling | High-risk and sensitive case types trigger mandatory human review |
| Confidence controls | Low-confidence predictions are not eligible for straight-through routing |
| Human authority | AI recommendations can be confirmed, corrected, or overridden by authorized reviewers |
| Public safety | Risk signals can increase review priority but cannot determine guilt, dangerousness, sentencing, or case outcome |
| Auditability | Predictions, model versions, confidence, reviewer actions, overrides, and timestamps are recorded |
| Model governance | Advanced models are evaluated in shadow mode before any controlled production use |
| Monitoring | Accuracy, Macro F1, confidence, overrides, drift, routing errors, and incidents are monitored |
| Incident response | Defined escalation, containment, investigation, and remediation workflow |

## Model Strategy

The recommended deployment pattern intentionally favors transparency and controlled escalation:

**1. TF-IDF + Logistic Regression — Controlled Pilot**  
Interpretable baseline for category routing and operational benchmarking.

**2. TF-IDF + Linear SVM — Specialized Routing**  
Evaluated for subcategory classification.

**3. BERT-Style Semantic Model — Shadow Mode**  
Runs offline against the same evaluation population without affecting live routing until performance, privacy, security, and governance gates are satisfied.

Model performance should never be interpreted independently of critical-misroute rate, human override rate, subgroup/category performance, confidence calibration, and public-safety impact.

## Human-in-the-Loop Decision Framework

```text
AI Prediction
     ↓
Sensitivity / Risk Check
     ↓
Confidence Threshold
     ↓
┌───────────────────────────────┐
│ Sensitive / High Risk / Low  │──→ Mandatory Human Review
│ Confidence                   │
└───────────────────────────────┘
     ↓ otherwise
AI-Assisted Routing Candidate
     ↓
Authorized Human Confirmation
     ↓
Auditable Final Decision
```

The AI system **does not** make findings of guilt, predict legal outcomes, recommend sentencing, determine dangerousness, or replace judicial/legal judgment.

## Repository Structure

```text
enterprise-ai-court-case-triage-governance/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── data/
│   ├── AandM_Sensitive_Court_Data_Governance_Release_v2.csv
│   └── AandM_Sensitive_Court_Data_Dictionary_v2.csv
│
├── notebooks/
│   └── Sensitive_Court_Data_AI_Triage_Governance.ipynb
│
├── src/
│   └── sensitive_case_ai_pipeline.py
│
├── dashboard/
│   └── executive_dashboard_sensitive_governance.html
│
├── docs/
│   ├── EXECUTIVE_SUMMARY.md
│   ├── SECURITY_PRIVACY_PUBLIC_SAFETY_GUARDRAILS.md
│   ├── AI_GOVERNANCE_FRAMEWORK.md
│   ├── DATA_PROTECTION_IMPACT_ASSESSMENT.md
│   ├── MODEL_CARD.md
│   ├── GO_NO_GO_CHECKLIST.md
│   ├── INCIDENT_RESPONSE_PLAYBOOK.md
│   ├── TECHNICAL_METHODOLOGY.md
│   ├── access_control_matrix.csv
│   ├── ai_risk_register.csv
│   └── data_governance_control_matrix.csv
│
├── outputs/
│   ├── model_metrics_governed.csv
│   ├── scored_cases_with_guardrails.csv
│   ├── audit_log_sample.csv
│   ├── human_review_queue_sample.csv
│   └── visualizations/
│
└── presentation/
    └── AandM_Sensitive_Court_AI_Governance_Executive_v2.pptx
```

## Project Files

### Executive
- [Executive Presentation](presentation/AandM_Sensitive_Court_AI_Governance_Executive_v2.pptx)
- [Interactive Executive Dashboard](dashboard/executive_dashboard_sensitive_governance.html)
- [Executive Summary](docs/EXECUTIVE_SUMMARY.md)

### Technical
- [End-to-End Notebook](notebooks/Sensitive_Court_Data_AI_Triage_Governance.ipynb)
- [Reusable Pipeline](src/sensitive_case_ai_pipeline.py)
- [Technical Methodology](docs/TECHNICAL_METHODOLOGY.md)

### Data
- [Governed Portfolio Dataset](data/AandM_Sensitive_Court_Data_Governance_Release_v2.csv)
- [Data Dictionary](data/AandM_Sensitive_Court_Data_Dictionary_v2.csv)

### Governance
- [Security, Privacy & Public-Safety Guardrails](docs/SECURITY_PRIVACY_PUBLIC_SAFETY_GUARDRAILS.md)
- [AI Governance Framework](docs/AI_GOVERNANCE_FRAMEWORK.md)
- [Data Protection Impact Assessment](docs/DATA_PROTECTION_IMPACT_ASSESSMENT.md)
- [Model Card](docs/MODEL_CARD.md)
- [Go / No-Go Checklist](docs/GO_NO_GO_CHECKLIST.md)
- [Incident Response Playbook](docs/INCIDENT_RESPONSE_PLAYBOOK.md)

## Executive Recommendation

Proceed only with a **controlled AI-assisted routing pilot** using the transparent baseline model. Keep the semantic/BERT model in shadow mode until the following gates are independently satisfied:

- privacy and data-handling controls;
- security architecture and access controls;
- model performance and critical-misroute thresholds;
- confidence calibration;
- public-safety escalation behavior;
- audit-log completeness;
- reviewer override and adoption results;
- governance and stakeholder approval.

AI should augment court operations while preserving human accountability and institutional control.

## Production Requirements

This public portfolio implementation is not a production court system. A real deployment would additionally require organization-approved infrastructure and controls including:

- SSO/MFA and role-based access control;
- encryption at rest and in transit;
- enterprise secrets/key management;
- DLP and approved data-classification policies;
- immutable/centralized audit logging;
- secure model registry and artifact provenance;
- vulnerability and dependency management;
- vendor/model/connector security review;
- formal retention and deletion policies;
- legal, privacy, security, and records-management review;
- documented incident-response ownership;
- periodic model validation and access recertification.

## How to Run

```bash
git clone <your-repository-url>
cd enterprise-ai-court-case-triage-governance
python -m venv .venv
```

Activate the environment and install dependencies:

```bash
pip install -r requirements.txt
jupyter notebook
```

Open:

```text
notebooks/Sensitive_Court_Data_AI_Triage_Governance.ipynb
```

## Disclaimer

This is an independent portfolio project. It is not an official Indiana Supreme Court, Alvarez & Marsal, or client system, product, engagement, or endorsement. The public dataset is synthetic. The project is intended to demonstrate AI product evaluation, analytics, security/privacy thinking, governance, and responsible deployment design.
