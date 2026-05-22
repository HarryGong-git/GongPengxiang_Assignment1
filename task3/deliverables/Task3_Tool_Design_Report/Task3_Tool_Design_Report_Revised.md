# Task 3 - Tool Design Report

**Jurisdiction-Aware Credit Decision Governance Monitor**  
**Option C with quantitative prototype**  
**Student:** Pengxiang Gong  
**Matriculation ID:** G2505431H  
**Course:** MH6822 Regulatory Technology

## 1. Executive Summary

This report designs and partially implements a jurisdiction-aware governance monitor for Revolut's AI-assisted credit decisioning. The tool demonstrates one central product choice: it shares a governance and evidence schema, not a global sensitive-data pipeline. The project therefore does not present jurisdiction awareness as a front-end dropdown. The jurisdiction choice changes data contracts, allowed fields, computation modules, evidence outputs, review owners and escalation triggers.

The selected use case is AI-assisted credit decisioning or credit scoring fairness across the United States and the European Union. In the US path, the tool focuses on adverse action reason quality, proxy-discrimination signals and fair lending review. In the EU path, the tool assumes creditworthiness or credit-score AI enters a high-risk AI governance workflow and focuses on pre-deployment evidence, controlled audit bias testing and post-deployment monitoring.

The quantitative prototype uses 1,400 synthetic credit applications: 700 US processed records and 700 EU audit records. It generates jurisdiction-bound evidence signals, including US reason-code confidence, US postcode and thin-file proxy gaps, EU approval disparity, EU false negative / false positive rate gaps, PSI-style drift metrics and EU pre-deployment evidence completeness. The numbers are synthetic and should not be interpreted as empirical findings about Revolut or its customers. Their purpose is to demonstrate how a RegTech product can route data, compute jurisdiction-bound metrics and escalate evidence to accountable owners.

The tool is deliberately bounded. It does not make credit decisions, issue legal opinions, certify EU AI Act conformity, automatically repair models or convert SHAP-style attribution into final adverse action notices. It produces evidence, risk signals and escalation routes so that compliance, model risk and legal teams can exercise judgement.

## 2. Selected Entity and Use Case

The named entity is Revolut. The US scenario is framed as Revolut-operated or Revolut-partnered credit products because public US secured-card disclosures identify Lead Bank as issuer and final eligibility decision-maker for that product (Revolut, 2026b). The tool therefore serves the credit decision governance function rather than assuming a single legal creditor model across every product.

This scope choice is important. A cross-border digital financial institution may have comparable onboarding, monitoring and model-governance workflows across markets, while still having different legal entity structures, partner-bank arrangements and regulatory responsibilities by product. The project does not assume one global credit model or one pooled customer dataset. It studies a more realistic governance problem: how a compliance function can maintain comparable evidence discipline while respecting jurisdiction-specific data rights, evidence obligations and escalation routes.

The selected domain is AI-assisted credit decisioning / credit scoring fairness. This is appropriate for a RegTech assignment because it combines consumer impact, model risk, explainability, fairness monitoring, data-access controls and regulatory evidence design. Credit decisions affect access to important financial services, and automated or semi-automated models can scale both consistency and harm. A governance tool therefore needs to do more than report accuracy; it must show how evidence is produced, which data is allowed, which owner is accountable and what happens when the tool detects weak explanations, proxy signals, drift or incomplete governance evidence.

## 3. Regulatory Divergence: US vs EU

The US and EU do not merely ask for the same model report in different formats. The US side is anchored in individualised adverse action explanation and fair lending review. ECOA / Regulation B requires creditors to provide specific reasons for adverse action, and CFPB guidance on complex algorithms emphasises that model complexity does not excuse vague or insufficient reasons (CFPB, 2022; CFPB, 2023; CFPB, 2025). In this project, the US module therefore focuses on reason-code quality, low-confidence explanation flags and proxy-risk signals such as postcode risk band, thin-file status and income-instability concentration.

The EU side places stronger emphasis on lifecycle governance of high-risk AI systems. EU AI Act Annex III includes AI systems used to evaluate creditworthiness or establish a credit score, subject to relevant exceptions (European Commission AI Act Service Desk, 2024). The EU design problem is therefore not only whether an applicant can receive a reason code. It is whether the institution can evidence high-risk AI governance: risk management, data governance, controlled bias testing, technical documentation, logging, human oversight and post-deployment monitoring (EU AI Act, 2024a; EU AI Act, 2024b; European Commission, 2024).

These are different political and regulatory choices. The US approach emphasises individual accountability after the credit decision: can the creditor explain the principal reasons for unfavourable treatment? The EU approach emphasises institutional lifecycle accountability: can the provider or deployer evidence that a high-risk AI use case is governed before and after deployment? A US module that only reports aggregate bias metrics would miss the adverse action problem. An EU module that only generates individual reason codes would miss the lifecycle governance problem.

| Design dimension | United States | European Union | Tool implication |
|---|---|---|---|
| Primary question | Can the creditor provide specific, accurate reasons for adverse action and detect fair lending risk? | Can high-risk AI governance be evidenced before and after deployment? | Different computation modules, not report skins. |
| Sensitive-data posture | US live path hard-drops direct protected / audit-only fields and relies on proxy-risk signals or separately approved privileged review. | EU audit path may use audit-only fields only in a segregated, lawful, access-controlled environment for bias testing. | Shared governance schema, not shared sensitive-data pipeline. |
| Explanation posture | SHAP-style attribution is an internal aid and must be mapped to approved reason codes. | Explanation is part of broader high-risk AI transparency, documentation and oversight evidence. | The same model score can generate different compliance evidence. |
| Lifecycle posture | Output is a draft adverse action evidence package and fair lending review trigger. | Output is pre-deployment evidence, bias testing, drift monitoring and human oversight workflow. | Jurisdiction affects workflow timing, not only reporting language. |

## 4. Product Philosophy: Shared Governance, Not Shared Sensitive-Data Pipeline

The tool uses a common evidence schema, configuration layer, audit log and escalation ladder. It does not use a common sensitive-data pipeline. This is the central architecture choice because a single global data pool would be convenient for analytics but dangerous for legal basis, access control, data minimisation and fair lending contamination.

The shared layer normalises management reporting: jurisdiction, model version, data version, rule version, risk signal, evidence generated, confidence level, owner, required action, deadline, escalation level and audit log reference. This gives senior management a comparable view of governance status without pretending the underlying legal rights and data permissions are identical.

The jurisdiction-bound layer changes what can be computed and who must act. In the US path, protected audit fields are removed before the processed data enters the tool. In the EU path, audit-only fields are kept in a segregated bias-testing path where a lawful basis, access control, logging, data minimisation and retention controls would be required in a real deployment. This means the product is jurisdiction-aware at the level of data contracts, not just labels.

## 5. System Architecture

The architecture has six layers:

1. **Shared governance schema:** normalises evidence fields, owner fields and escalation fields.
2. **Jurisdiction-specific data paths:** separates the US hard-drop processed path from the EU segregated audit path.
3. **Jurisdiction-bound computation modules:** runs US reason/proxy modules and EU high-risk/bias/drift modules.
4. **Common evidence package:** gives management a consistent evidence structure.
5. **Risk-tiered human oversight:** routes judgement by severity instead of sending all cases to manual review.
6. **Configuration version control:** treats rule changes as governed events with owner, effective date, approval and rollback.

This design prevents the jurisdiction selector from being decorative. If the jurisdiction changes, the allowed fields, computation modules, evidence packages and review owners change.

## 6. Data Architecture

### 6.1 US hard-drop path

In the US path, application data flows through a hard-drop stage that removes `age`, `gender_audit`, `age_band`, `protected_group_flag` and `audit_group` before the processed file enters the tool. The US processed file supports reason-code candidate generation and proxy-risk monitoring but does not hold direct audit attributes. This reduces the risk that explanation tooling becomes a hidden source of sensitive-data contamination in live credit operations.

This boundary does not mean the tool ignores fair lending risk. Instead, it uses non-protected proxy signals, including postcode risk band, thin-file status and income-instability concentration, as internal fair lending review signals. These signals do not prove unlawful discrimination by themselves and should not be used as consumer-facing adverse action reasons. They identify where legal, compliance and model-risk staff should focus review.

### 6.2 EU segregated audit path

In the EU path, live credit decisioning remains free of sensitive audit attributes. A separate EU audit dataset contains `audit_group`, `gender_audit`, `age_band` and `protected_group_flag` for controlled bias testing. These fields are not used for live approval decisions. In a real deployment, audit-only sensitive fields would require lawful basis, data minimisation, role-based access, logging, retention limits and data-protection review.

The EU path therefore acknowledges that high-risk AI governance may require bias testing, but it does not treat the AI Act as a free pass to process special-category data. The tool itself becomes part of the governance perimeter and must be governed through access control, logs, data contracts and a tool card.

## 7. Synthetic Data Method

The synthetic dataset contains credit score, income, debt-to-income ratio, employment length, loan amount, postcode risk band, thin-file status, income-instability flag, model score, decision and observed default outcome. Audit-only fields include `gender_audit`, `age_band`, `protected_group_flag` and `audit_group`. The data generation deliberately creates plausible correlations between audit group, thin-file status, postcode risk and credit score so that the proxy-risk and bias-testing modules have meaningful signals to detect.

Because the data is synthetic, the analysis is a method demonstration rather than a factual claim about Revolut customers. That limitation is useful for the assignment: it allows the design to show sensitive-data controls and fairness metrics without exposing real personal data.

## 8. Regulatory Mapping Table: From Legal Concern to Tool Rule

The regulatory mapping table is the legal and policy backbone of the prototype. It prevents the jurisdiction logic from becoming decorative. The table connects each regulatory concern to a tool response, data-access rule, output, human owner and limitation.

The mapping table should be read before the `jurisdiction_config` file. The mapping table explains *why* a rule exists; the configuration file makes the rule executable. For example, the US adverse-action concern is translated into a reason-code module, a low-confidence flag and a sampled review queue. The EU high-risk AI concern is translated into a pre-deployment evidence gate, controlled audit bias testing and post-deployment monitoring.

Where legal basis is uncertain, the project uses cautious language and labels the control as an internal governance control rather than inventing a statutory obligation. This is important because a RegTech product should not turn legal uncertainty into false precision. The tool produces evidence for human judgement; it does not certify legality.

## 9. Jurisdiction Configuration Layer

`Task3_Jurisdiction_Config.json` stores `rule_id`, jurisdiction, legal basis, data-access posture, computation module, output requirement, human review trigger, owner, version, effective date, approval status and rollback mechanism. This makes rule change a governed event rather than an invisible code edit.

| Config field | Why it exists |
|---|---|
| `rule_id` and version | Keeps evidence tied to a specific rule and avoids untraceable policy changes. |
| `legal_basis` and URL | Forces the tool designer to connect each computation to a real regulatory or governance concern. |
| `data_access` | Prevents a rule from silently using fields that are not permitted in that jurisdictional path. |
| `human_review_trigger` | Defines the point where automation must hand off to accountable human judgement. |
| Owner and rollback | Makes rule maintenance operational rather than aspirational. |

The most important configuration risk is jurisdiction configuration drift. This is not ordinary model drift. It occurs when the rule layer itself changes incorrectly, for example if a US hard-drop rule is disabled or an EU audit-only field is accidentally permitted downstream while evidence packages still appear clean. The tool therefore treats configuration change as a controlled event with four-eyes approval, audit log and rollback.

## 10. Shared Evidence Schema

Every module writes to the same evidence schema: `jurisdiction`, `model_version`, `data_version`, `rule_version`, `risk_signal`, `evidence_generated`, `confidence_level`, `required_owner`, `required_action`, `deadline`, `escalation_level` and `audit_log_reference`.

The shared schema lets senior management compare governance status across countries without flattening legal differences. A US evidence row may assign reason-code review to the US Compliance Lead. An EU evidence row may assign pre-deployment evidence completion to the EU AI Governance Lead. They share a reporting format, but the risk signal and owner are jurisdiction-bound.

## 11. Quantitative Component

The quantitative analysis is generated from the following artefacts:

- `Task3_Quantitative_Analysis_Notebook.ipynb` and `.html`
- `Task3_Synthetic_Credit_Data.csv`
- `Task3_US_Processed_Data.csv`
- `Task3_EU_Audit_Data.csv`
- `Task3_Output_US_Evidence.csv`
- `Task3_Output_EU_Evidence.csv`
- `Task3_Sensitivity_Results.csv`
- `Task3_Run_Metrics.json`

| Metric | Result | Interpretation |
|---|---:|---|
| US low-confidence reason flag rate | 25.9% | A sampled review queue is required before reasons are treated as consumer-facing. |
| US Very High vs Low postcode denial gap | 31.8% | Potential proxy discrimination / digital redlining signal for internal review. |
| US thin-file denial gap | 26.5% | Thin-file applicants receive materially different outcomes. |
| EU approval disparity ratio | 0.35 | Below 0.80 would trigger model governance review in this prototype. |
| EU FNR gap | 26.5% | Shows whether good borrowers are denied at unequal rates by audit group. |
| EU score PSI | 0.005 | Post-deployment drift signal under protected-group shift scenario. |
| EU pre-deployment completeness | 87.5% | Missing governance owner blocks EU deployment approval in the prototype. |

US results are intentionally framed as internal review evidence. A high postcode denial gap does not prove unlawful discrimination by itself, and a SHAP-style candidate does not become a legal adverse action reason. EU results are framed as lifecycle governance evidence: incomplete pre-deployment controls can block launch even before a performance failure appears.

## 12. Sensitivity Analysis

The sensitivity file varies approval thresholds and alert thresholds. It estimates how conclusions and human-review workload change when the model becomes stricter or when the firm lowers its alert threshold. This matters because a governance design that is too insensitive misses harm, while a design that is too sensitive can overwhelm operations and delay legitimate approvals.

In the tested scenario, estimated human-review workload remains close to 37% across the approval thresholds shown in the figure output. This should not be presented as a dramatic threshold effect. The conclusion is workload stability under the tested range: the review queue does not become a runaway manual-review burden, but it also does not disappear. This supports the design choice of risk-tiered oversight rather than broad manual blocking.

| Scenario question | What the sensitivity output tests |
|---|---|
| If approval threshold rises | Approval rates fall, denial concentration can grow and human-review workload changes. |
| If alert threshold tightens | More proxy-risk and bias signals become reviewable issues. |
| If protected-group DTI shifts | EU drift and group-performance signals reveal whether monitoring catches distribution change. |
| If workload grows | Management can choose Level 1 monitoring or Level 2 sampled review rather than immediate business blocking. |

## 13. Human Oversight Design

The human oversight design is deliberately not a full manual-review queue. Level 1 creates monitoring tickets, Level 2 uses sampled review, and only Level 3 / Level 4 affects deployment or emergency suspension. This preserves human judgement without paralysing instant decisioning.

| Level | Action | Typical trigger |
|---|---|---|
| Level 0 | No action | Data contract passes and metrics remain within normal monitoring range. |
| Level 1 | Monitoring ticket | Minor drift or weak signal; no business blocking. |
| Level 2 | Sampled review | Low-confidence US reasons or moderate EU performance gap; 1%-5% sample review. |
| Level 3 | Model governance review | High-risk EU evidence missing, severe disparity or material model change. |
| Level 4 | Emergency suspension | Sensitive fields leak into live model, jurisdiction configuration fails or severe systemic discrimination signal appears. |

This design operationalises the principle that judgement cannot be outsourced. The tool routes judgement to accountable owners instead of pretending that a dashboard can make legal or ethical decisions.

## 14. Self-Governance of the RegTech Tool

The tool itself can become a source of governance risk. It processes evidence, configuration and in the EU audit path potentially sensitive audit-only fields. For that reason, the tool should be governed as compliance infrastructure rather than treated as a neutral dashboard.

Key self-governance controls include:

- The tool does not make final credit decisions and does not automatically change model weights.
- The tool does not issue final legal opinions or regulatory certifications.
- EU audit-only sensitive data requires lawful basis, data minimisation, role-based access, retention limits and audit logs.
- Configuration changes require four-eyes approval and a rollback path.
- The tool has its own tool card because RegTech software can itself become a source of governance risk.

## 15. Failure Mode Analysis

The strongest failure modes are specific to RegTech, not only generic model risk. The table below names who is harmed, how the tool detects the failure, how the firm mitigates it and what residual risk remains.

| Failure mode | Who is harmed | Detection | Mitigation | Residual risk |
|---|---|---|---|---|
| Jurisdiction configuration drift | Applicants and compliance owners | Config version mismatch or protected field in wrong path | Four-eyes approval, audit log and rollback | A wrong but approved rule can still encode a poor policy choice. |
| US reason-code failure | Declined applicants | Low-confidence reason flag or REVIEW-PROXY reason | Sampled review and approved reason taxonomy | Post-hoc explanations can approximate but not perfectly reveal model logic. |
| US proxy blind spot | Protected communities | Postcode and thin-file concentration analysis | Privileged fair lending review | Without demographic labels, some disparities can be missed. |
| EU audit data governance failure | EU applicants | Audit log, access review and data contract tests | Segregated audit environment and retention limits | The audit environment itself increases privacy risk. |
| Human oversight overload | Applicants and operations teams | Sensitivity analysis on review workload | Risk-tiered review and threshold calibration | Lower thresholds may still slow instant decisioning. |

Jurisdiction configuration drift is the most RegTech-specific failure. A model can appear stable while the rule layer silently changes. For example, a bad configuration could allow an EU audit-only field into a downstream dataset or bypass a US hard-drop control. That is why configuration control is treated as part of the product, not an administrative afterthought.

## 16. Strategic Boundary Choices

- **No unified sensitive-data pool:** this reduces cross-jurisdiction contamination at the cost of weaker comparability and higher engineering cost.
- **No automatic final adverse action notice:** human review is preserved because SHAP-style attribution is not legally sufficient by itself.
- **No automatic model repair:** the tool surfaces evidence and escalation, but remediation stays inside model governance.
- **No legal conclusion:** the tool says what evidence exists and what action is required; it does not say legal or illegal.

These are not generic disclaimers. They are product boundary choices. The tool is useful precisely because it refuses to become a credit engine, a legal certification system or an automated bias-remediation system.

## 17. Acceptance Checks Built into the Submission

- `Task3_US_Processed_Data.csv` contains no `age`, `gender_audit`, `age_band`, `protected_group_flag` or `audit_group` fields.
- `Task3_EU_Audit_Data.csv` contains audit-only fields and is documented as separate from live credit decisioning.
- US and EU evidence outputs use the same schema but different `rule_version`, `risk_signal`, owner and required-action values.
- `Task3_Jurisdiction_Config.json` gives each rule an owner, version, legal basis, effective date, human-review trigger and rollback mechanism.
- The senior management deck and one-page summary explicitly state what the tool does not do.

## 18. Limitations and Future Improvements

- Synthetic data demonstrates mechanics but cannot estimate Revolut's real customer impact.
- The US proxy module is deliberately conservative and should be paired with privileged legal review.
- The EU audit design assumes a lawful basis and access control for audit-only sensitive fields; real deployment would need data-protection review.
- Future versions should connect to live model monitoring, issue trackers, legal-rule update workflows, immutable audit logging, production drift dashboards and additional jurisdiction packs such as the UK or Singapore.

## 19. References

CFPB (Consumer Financial Protection Bureau) (2022) *Consumer Financial Protection Circular 2022-03: Adverse action notification requirements in connection with credit decisions based on complex algorithms*. Washington, D.C.: Consumer Financial Protection Bureau. Available at: https://www.consumerfinance.gov/compliance/circulars/circular-2022-03-adverse-action-notification-requirements-in-connection-with-credit-decisions-based-on-complex-algorithms/ (Accessed: 22 May 2026).

CFPB (Consumer Financial Protection Bureau) (2023) *CFPB issues guidance on credit denials by lenders using artificial intelligence*. Washington, D.C.: Consumer Financial Protection Bureau. Available at: https://www.consumerfinance.gov/about-us/newsroom/cfpb-issues-guidance-on-credit-denials-by-lenders-using-artificial-intelligence/ (Accessed: 22 May 2026).

CFPB (Consumer Financial Protection Bureau) (2025) *Regulation B, 12 CFR Section 1002.9: Notifications*. Washington, D.C.: Consumer Financial Protection Bureau. Available at: https://www.consumerfinance.gov/rules-policy/regulations/1002/9/ (Accessed: 22 May 2026).

EU AI Act (2024a) *Article 10: Data and data governance*. Available at: https://www.euaiact.com/article/10 (Accessed: 22 May 2026).

EU AI Act (2024b) *Article 14: Human oversight*. Available at: https://artificialintelligenceact.eu/article/14/ (Accessed: 22 May 2026).

European Commission (2024) *AI Act: regulatory framework for artificial intelligence*. Brussels: European Commission. Available at: https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai (Accessed: 22 May 2026).

European Commission AI Act Service Desk (2024) *EU AI Act Annex III: High-risk AI systems*. Brussels: European Commission. Available at: https://ai-act-service-desk.ec.europa.eu/en/ai-act/annex-3 (Accessed: 22 May 2026).

Revolut (2026a) *About Revolut*. Available at: https://www.revolut.com/en-US/about-revolut/ (Accessed: 22 May 2026).

Revolut (2026b) *US secured credit card disclosure*. Available at: https://www.revolut.com/en-US/secured-creditcards/ (Accessed: 22 May 2026).
