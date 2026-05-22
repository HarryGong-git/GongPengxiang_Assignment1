# Task3_Model_Card_or_Tool_Card

Task 3 - Model Card / Tool Card
Page 1
Task 3 - Model Card / Tool Card
Jurisdiction-Aware Credit Decision Governance Monitor | Tool Governance Card
 Field
 Content
Tool name
Jurisdiction-Aware Credit Decision Governance Monitor
Purpose
Generate jurisdiction-bound governance evidence for AI-assisted credit decisioning.
Intended users
Chief Compliance Officer, US Compliance Lead, EU AI Governance Lead, Model Risk, Data Governance and
Fair Lending Counsel.
Not intended for
Consumer-facing explanation, final legal advice, final credit decisioning or regulatory certification.
Data used
Synthetic credit applications, US processed data, EU audit-only dataset, jurisdiction_config and rule mapping.
Data excluded
US processed path excludes age, gender_audit, age_band, protected_group_flag and audit_group.
EU audit-only controls
Audit-only sensitive data requires lawful basis, access control, logs, data minimisation and retention limits before
use in the segregated audit environment.
Core metrics
US reason-code confidence, proxy denial gaps, EU approval disparity, FNR/FPR disparity, PSI drift and
evidence completeness.
Human oversight
Risk-tiered Level 0 to Level 4 workflow with sampled review before business-blocking action.
Known limitations
Synthetic data, no live legal update feed, no immutable audit ledger and no production integration.
Self-governance controls
Role-based access, audit logs, configuration versioning, rollback mechanism and four-eyes approval.
Prototype Metric Snapshot
- US low-confidence reason rate: 25.9%.
- US postcode proxy denial gap: 31.8%.
- EU approval disparity ratio: 0.35.
- EU pre-deployment completeness: 87.5%.
