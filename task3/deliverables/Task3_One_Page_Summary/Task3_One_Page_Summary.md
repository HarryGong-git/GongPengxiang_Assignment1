# Task 3 - One Page Summary

## Jurisdiction-Aware Credit Decision Governance Monitor

This project designs a jurisdiction-aware governance monitor for Revolut's AI-assisted credit decisioning. It is built around one product principle: **shared governance schema, not shared sensitive-data pipeline**. The tool uses synthetic credit application data to show how the same credit decisioning problem produces different evidence outputs under US and EU regulatory choices.

| Question | Plain-language answer |
|---|---|
| What the tool does | It monitors AI-assisted credit decision outputs for explanation quality, proxy-risk signals, EU bias-testing metrics, drift and pre-deployment governance evidence, then generates jurisdiction-specific evidence packages. |
| Why it is needed | A spreadsheet can list rules, but it cannot enforce data-path separation, version rule changes, retain audit logs or route weak evidence to accountable owners. The jurisdiction choice changes data access, computation modules, evidence outputs and escalation owners; it is not just a report-template switch. |
| How the US and EU differ | US mode focuses on specific adverse-action reason quality, reason-code confidence and proxy-discrimination review. EU mode assumes creditworthiness AI is a high-risk AI use case and checks lifecycle governance evidence, controlled bias testing and post-deployment monitoring. |
| What data it uses | The prototype uses 1,400 synthetic applications: 700 US processed records and 700 EU audit records. The US processed dataset excludes age, gender_audit, age_band, protected_group_flag and audit_group. The EU audit dataset retains audit-only fields only in a segregated path for controlled bias testing. |
| What it outputs | US and EU evidence packages use a shared schema: jurisdiction, model version, rule version, risk signal, evidence generated, confidence level, owner, required action, deadline, escalation level and audit reference. |
| How human oversight works | Human review is risk-tiered. Minor signals create monitoring tickets; moderate issues trigger sampled review; severe governance gaps, sensitive-data leakage or configuration failures trigger model governance review or emergency suspension. |
| What it deliberately does not do | It does not make final lending decisions, issue legal opinions, certify EU AI Act conformity, automatically repair models or treat SHAP-style attribution as legally sufficient adverse-action reasons. The synthetic figures demonstrate workflow mechanics and are not empirical claims about Revolut customers. |

