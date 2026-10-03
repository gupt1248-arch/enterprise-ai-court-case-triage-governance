# Model Card: Sensitive Court Data AI Triage

## Model Name
TF-IDF + Logistic Regression Category Routing Model, version `tfidf-lg-v1.0-redacted-inputs`

## Intended Use
Assist court operations teams with initial case category routing after PII redaction and sensitivity classification.

## Not Intended For
Legal outcomes, guilt/liability prediction, sentencing, legal advice, public-safety determinations, eligibility decisions, or autonomous case disposition.

## Training Data
Synthetic records representing operational intake categories. In production, training data would require governance approval, redaction, documented provenance, retention compliance, and access control.

## Inputs
Redacted, normalized case title and case description.

## Outputs
Predicted category, confidence score, guardrail action, and escalation reason.

## Performance
| model                                          | use_case                    |   accuracy |   macro_f1 |   mean_confidence | status                       |
|:-----------------------------------------------|:----------------------------|-----------:|-----------:|------------------:|:-----------------------------|
| TF-IDF + Logistic Regression                   | Baseline category routing   |          1 |          1 |             0.958 | Recommended controlled pilot |
| TF-IDF + LinearSVC                             | Subcategory routing         |          1 |          1 |                   | Specialized routing model    |
| BERT-style semantic benchmark (offline shadow) | Advanced semantic benchmark |          1 |          1 |             0.961 | Shadow mode only             |

## Primary Risks
- Incorrect routing of sensitive matters
- Overconfidence on rare categories
- Incomplete redaction
- Drift due to changing forms/workflows
- Misuse as a legal decisioning tool

## Mitigations
- Mandatory human review for restricted/public-safety records
- Higher confidence thresholds for sensitive data
- Audit logs with model version and override reason
- Shadow testing for advanced models
- Monitoring by category and county
