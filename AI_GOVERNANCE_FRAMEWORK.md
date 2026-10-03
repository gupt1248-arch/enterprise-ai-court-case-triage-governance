# AI Governance Framework

## Purpose
Govern AI-assisted court intake triage in a way that improves operational efficiency while maintaining privacy, security, public trust, public safety, and human accountability.

## Approved Use
- Queue routing support
- Duplicate and data-quality detection
- Reviewer workload prioritization
- Aggregate operational reporting
- Controlled POC evaluation of AI tools

## Prohibited Use
- Predicting case outcomes
- Recommending guilt, liability, sentence length, custody outcomes, bond, or eligibility decisions
- Providing legal advice
- Automatically denying, approving, dismissing, or escalating a legal action without human authority
- Sending restricted data to unapproved external AI services

## Governance Gates
1. Business need and workflow fit approved
2. Privacy impact assessment completed
3. Data classification and retention plan approved
4. Security review completed
5. Model performance meets minimum threshold
6. Public-safety escalation tested
7. Audit logging validated
8. Human reviewer training completed
9. Production support and incident-response process assigned
10. Product Director / Governance Board Go-No-Go decision recorded

## Model Lifecycle
- Baseline: TF-IDF + Logistic Regression for controlled pilot
- Shadow benchmark: BERT-style semantic model, no production decisions
- Monitoring: macro F1, category-level recall, restricted-case error rate, override rate, drift, reviewer feedback
- Retirement: model removed if drift, safety issue, privacy issue, or reviewer trust issue exceeds tolerance
