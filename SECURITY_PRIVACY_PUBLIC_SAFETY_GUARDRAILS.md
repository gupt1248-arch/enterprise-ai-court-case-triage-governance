# Security, Privacy & Public Safety Guardrails

## Operating Assumption
All incoming court records must be treated as highly sensitive until classified otherwise. The prototype uses synthetic data, but the control design assumes real restricted court records.

## Implemented Prototype Controls

| Control | Implementation |
|---|---|
| Data classification | Records are classified as Internal, Confidential, or Restricted-Court Data before inference. |
| PII detection | SSN, phone, email, DOB, street address, and contextual names are detected. |
| Redaction before modeling | NLP models use redacted text, not raw sensitive text. |
| Pseudonymization | Direct case IDs are replaced by salted SHA-256 case keys. |
| Public safety escalation | Protection order, threat, weapon/firearm, emergency, minor/guardian, and sealed-record indicators trigger mandatory review. |
| Human-in-the-loop | AI only recommends routing; it cannot make legal or public-safety decisions. |
| Confidence thresholding | Restricted cases use stricter confidence rules and mandatory review. |
| Auditability | Prediction, model version, input hash, confidence, flags, action, and reviewer decision are logged. |
| Scope controls | No outcome prediction, guilt scoring, sentencing, eligibility denial, legal advice, or autonomous case disposition. |

## Production Controls Required
- SSO/MFA and role-based access control
- Encryption in transit and at rest
- Key management and secret rotation
- DLP scanning for exports, logs, dashboards, and notebooks
- Immutable audit logging
- Retention and deletion tied to court schedules and litigation holds
- Approved connector registry and data processing agreements
- Security review before each model or connector rollout
- Incident-response procedure for data leakage or unsafe recommendations

## Public Safety Design Principle
The model should accelerate escalation, not suppress it. Any record with credible threat, weapon/firearm, emergency hearing, protected address, no-contact order, minor/guardian, or sealed-record signal must be routed to human review regardless of model confidence.
