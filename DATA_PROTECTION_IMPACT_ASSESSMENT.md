# Data Protection Impact Assessment

## Processing Purpose
AI-assisted operational triage of court intake records to improve routing efficiency and reviewer workload management.

## Data Types
- Case narrative
- Filing metadata
- Case category/subcategory
- Source channel
- Synthetic examples of identifiers such as DOB, phone, address, email, and SSN
- Sensitivity and public-safety indicators

## Sensitivity
The design assumes data may include restricted court records, sealed information, protected addresses, victim statements, minor-related information, and public-safety indicators.

## Privacy-by-Design Controls
- Redaction before modeling
- Pseudonymized case keys
- Raw sensitive text excluded from public-safe outputs
- Aggregate dashboard metrics
- Audit-log hashes instead of raw narratives
- Human review for sensitive cases

## Residual Risks
- False negative PII detection
- Over-broad staff access
- Export of sensitive data from dashboards
- Model drift or reviewer overreliance

## Required Production Approvals
Security, privacy, legal/court governance, operations leadership, AI governance board, and product owner.
