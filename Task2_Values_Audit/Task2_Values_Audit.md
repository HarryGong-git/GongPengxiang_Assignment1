Task 2 - Values Audit

Jurisdiction-Aware Credit Decision Governance Monitor | EvidenceBridge RegTech

**Purpose.** This values audit states the operating values and trade-offs behind the proposed RegTech tool before the technical design is judged. The tool serves a paying institutional client, but its failures would be felt first by credit applicants.

## 1. Company Mission and Operating Reality

EvidenceBridge RegTech is a hypothetical 15-person B2B compliance analytics startup. Its mission is to help financial institutions convert model-risk and regulatory obligations into testable evidence without pretending that software can settle legal judgement. The company is good at model monitoring, explanation workflows, data-contract controls, rule versioning and regulatory evidence design. It is early-stage, revenue-constrained and must sell to clients with clear budget and accountability: Chief Compliance Officers, model risk teams, AI governance leads and internal audit functions at regulated digital financial institutions.

The company is not a consumer-rights platform and not a regulator. That is an uncomfortable but important starting point. EvidenceBridge wants a narrow enterprise product that can be sold to firms operating across the US and EU. The commercial case is that a cross-border fintech such as Revolut needs consistent governance evidence even when the legal creditor, partner-bank structure, data rights and regulatory obligations differ by product and jurisdiction. The product therefore helps a CCO answer a board-level question: which rule version, data path, evidence package, owner and escalation trail supports this credit decision workflow?

EvidenceBridge's values are operational honesty, jurisdictional humility and accountable automation. Operational honesty means the tool must show gaps, missing owners, low-confidence explanations and weak evidence even when that is commercially uncomfortable. Jurisdictional humility means the product does not flatten different political choices into one global compliance score. Accountable automation means the tool helps humans focus their judgement, but does not outsource judgement to a dashboard.

## 2. Whose Perspective Does the Tool Serve?

The tool primarily serves Revolut's CCO, model risk and AI governance teams. This is a deliberate choice because they are the immediate buyer, they hold internal accountability and they have a workflow pain point: they must coordinate evidence across jurisdictions without paralysing digital credit operations. The tool also indirectly serves consumers and regulators by making risk evidence harder to ignore. It does not serve consumers directly: it does not provide a dispute portal, does not send notices to applicants and does not decide whether a legal breach occurred.

The stakeholder conflict is real rather than rhetorical:

- **CCO / model risk team:** wants reliable evidence, clear owners and defensible governance, but may prefer fewer alerts and lower review workload. The design response is owner-specific evidence packages and risk-tiered escalation.

- **Business unit:** wants fast credit decisions and high conversion. The design response is a Level 0-4 oversight ladder so that only severe failures block deployment.

- **Regulators:** want traceability, specificity and human accountability. The design response is rule versioning, data-path controls, common evidence fields and audit logs.

- **Consumers:** want fair access and understandable adverse outcomes, but they are not the buyer. The design response is reason-code quality checks, proxy-risk monitoring and human review for low-confidence cases.

- **EvidenceBridge:** wants adoption, scalability and limited liability. The design response is explicit limitations, a tool card and no claim of legal certification.

The company's choice is to serve the paying compliance function while refusing to provide a silent-ignore path for material risk. The tool can be overridden, because judgement cannot be outsourced, but high-risk overrides require an owner, rationale, timestamp, evidence reference and audit log. This is not presented as a risk-detection feature; it is a responsibility-governance feature. The risk-detection features are the proxy-risk, reason-quality, drift, bias-testing and configuration-drift modules described below.

## 3. Is the Tool Measuring Genuine Risk or Documenting Compliance?

The tool has both documentary and risk-detection functions, but it should not confuse them. Compliance documentation includes evidence packages, audit logs, override records, model cards and rule-version histories. Those are necessary, but they can still coexist with a harmful model. Genuine risk detection asks whether model outputs are becoming unstable, whether a postcode or thin-file variable is concentrating denials, whether declined applicants receive low-confidence reason codes, whether EU bias-testing evidence shows group-level performance gaps, and whether a jurisdiction configuration has drifted from approved policy.

The most important design choice is not the override log. It is the combination of the US proxy-risk and reason-code-quality module with the EU controlled audit bias-testing and drift module. In the US live path, direct protected attributes are hard-dropped before the tool receives data. That reduces sensitive-data contamination risk but also weakens direct disparity testing. To compensate, the tool monitors proxy signals such as postcode risk band, thin-file status and income-instability concentration. These signals do not prove unlawful discrimination; they direct fair-lending review to the parts of the pipeline most likely to hide proxy effects.

In the EU path, the tool does not put sensitive fields into live credit decisioning. Instead, where a lawful basis and data-protection review are available, audit-only fields are processed in a segregated environment for bias testing. That produces governance evidence on approval disparity, false negative gaps, false positive gaps, data drift and pre-deployment completeness. The value is not that the software declares the system legal. The value is that it creates a structured evidence trail showing where human judgement must engage before deployment and during monitoring.

A deliberately excluded feature is automatic generation of final legal adverse action notices. The tool produces candidate reason codes and evidence packages, but final notices require human review because SHAP-style attribution is not legally sufficient by itself. Another deliberately excluded feature is automatic model repair. The tool may recommend investigation or remediation, but it does not rebalance training data, change model weights or approve deployment. That boundary is costly because detection can be faster than remediation, but it preserves model governance and auditability.

## 4. Who Bears the Cost if the Tool Gets It Wrong?

The cost of error is not distributed evenly. False negatives in compliance monitoring usually harm consumers first because unfair outcomes remain hidden. False positives can harm consumers and the business by delaying legitimate approvals. Jurisdictional misconfiguration can harm everyone: applicants receive worse outcomes, Revolut and partner banks face governance risk, regulators lose trust in automated evidence, and EvidenceBridge may lose the account because its tool became part of the failure.

The most serious risk is not only that a model fails. It is that the governance tool gives a false sense of control. A clean evidence package can become dangerous if the rule version is wrong, the data path has leaked audit-only fields, or the reason-code mapping is overconfident. For that reason the tool must be governed as compliance infrastructure, not treated as a neutral dashboard.

The main failure scenarios are specific:

- **US reason-code mapping error:** an applicant receives a vague or inaccurate denial reason because attribution is overconfident or mapped to the wrong reason code. The consumer is harmed first; Revolut, the partner bank and legal team face downstream risk. Mitigation is a low-confidence flag, approved reason taxonomy, sampled review and no automatic final notice.

- **US proxy discrimination blind spot:** a postcode, thin-file or income-instability variable functions as a protected-class proxy but is not detected because direct labels are unavailable in the live path. The affected community bears the main cost. Mitigation is proxy-risk monitoring and separately approved privileged fair-lending review, but some disparities can still be missed.

- **EU audit data governance failure:** audit-only sensitive data leaks into a live model, is accessed by unauthorised users or is retained longer than necessary. EU applicants and Revolut's data governance function are harmed. Mitigation is a segregated audit environment, access control, logging, retention limits and data contract tests.

- **Jurisdiction configuration drift:** a rule change disables the EU evidence gate or bypasses the US hard-drop control while the tool still produces apparently clean outputs. Revolut compliance owners, applicants and EvidenceBridge are exposed. Mitigation is four-eyes approval, rule-version checks, rollback and configuration validation.

- **Over-sensitive escalation threshold:** too many applications are routed to review and instant decisioning slows down. Legitimate applicants and product operations bear the cost. Mitigation is risk-tiered Level 0-4 oversight and sensitivity testing of review workload.

## 5. Values Position

EvidenceBridge's position is not morally perfect, but it is explicit. The product serves an institutional buyer and is designed for adoption by compliance and model-risk teams. It does not claim to equalise access to credit or replace public enforcement. Its value is narrower: it makes cross-jurisdiction credit model governance more testable, more owned and more honest about uncertainty.

The tool therefore measures genuine risk where it can, documents governance where it must, and names the boundary between the two. It is strongest when it surfaces uncomfortable signals that a spreadsheet or memo would bury: low-confidence reasons, proxy-risk concentrations, incomplete EU pre-deployment evidence, audit-data governance weaknesses and jurisdiction configuration drift. It is weakest if management treats its evidence package as proof of fairness. That residual risk is why the design preserves human judgement, legal review and explicit limitations.
