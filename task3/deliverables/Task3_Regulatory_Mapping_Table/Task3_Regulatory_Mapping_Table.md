# Task3_Regulatory_Mapping_Table

Task 3 - Regulatory Mapping Table
Page 1
Task 3 - Regulatory Mapping Table
Jurisdiction-Aware Credit Decision Governance Monitor | US and EU rule-to-tool mapping
This mapping table is the legal-policy backbone of the prototype. It shows that the US and EU modules do not merely use different labels. They have different data
permissions, computation modules, outputs and human owners.
Jurisdicti
 on
 Regulatory concern
 Legal / policy basis
 Tool response
 Data access rule
 Output generated
 Human owner
 Limitation
US
Specific adverse action
reasons for declined or
unfavourably treated
applicants
ECOA / Regulation B 12
CFR 1002.9; CFPB
Circular 2022-03
Use SHAP-style attribution only as
an internal aid, then map to
approved reason codes and flag
low-confidence cases.
No protected attributes in US
live explanation path.
Draft adverse action
evidence package and
sampled review queue.
US Compliance
Lead
Tool does not issue the final
legal notice.
US
Proxy discrimination and
digital redlining risk
ECOA fair lending risk
management; CFPB public
guidance on AI and digital
redlining
Monitor postcode, thin-file and
income-instability concentration
as proxy-risk signals.
Live path uses non-protected
variables; demographic
analysis is separated into
privileged review if approved.
Fair lending internal
review trigger.
Fair Lending
Review Counsel
Without direct demographic
labels, proxy testing can
under-detect harm.
US
Sensitive-data
contamination in live
credit tooling
Internal policy boundary
aligned with data
minimisation and fair
lending controls
Physically hard-drop audit-only
fields before US processed data
enters the tool.
US processed file excludes
age, gender_audit,
age_band,
protected_group_flag and
audit_group.
Data contract pass/fail
control.
Data Governance
Lead
Does not remove the need
for separately approved fair
lending analysis.
EU
Creditworthiness AI as
high-risk AI
EU AI Act Annex III for
creditworthiness / credit
score high-risk
classification.
Default EU credit decision use
case into high-risk AI governance
workflow.
Governance checklist does
not require live sensitive-data
use.
Pre-deployment
evidence completeness
gate.
EU AI Governance
Lead
Tool does not provide
conformity certification.
EU
Bias testing and lifecycle
risk management
EU AI Act high-risk AI
obligations, including data
governance, risk
management and human
oversight. Sensitive or
special-category audit
fields require a separate
lawful basis, access
control, logging,
minimisation and retention
controls.
Run group performance and
approval disparity tests in
segregated audit environment.
Sensitive or special-category
fields only in audit
environment with lawful
basis, access control, logs,
minimisation and retention
controls.
Bias testing evidence
package.
EU Model Risk
Lead
Synthetic audit labels
demonstrate method, not
real protected-class
prevalence.
EU
Post-deployment
monitoring and material
change
EU AI Act high-risk AI
lifecycle governance and
post-deployment /
post-market monitoring
expectations.
Monitor PSI drift, reason-code
instability and performance shift
by audit group.
Production monitoring data
plus audit-only comparison
where approved.
Drift ticket and model
governance review
trigger.
Model Monitoring
Lead
Drift detection does not
identify every causal source
of model degradation.
