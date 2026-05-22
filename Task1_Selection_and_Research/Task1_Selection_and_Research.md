**Task 1 - Selection and Research**

*Jurisdiction-Aware Credit Decision Governance Monitor*

|                     |                                                                                    |
|---------------------|------------------------------------------------------------------------------------|
| **Selected entity** | Revolut                                                                            |
| **Domain**          | AI-assisted credit decisioning / credit scoring fairness / AI governance           |
| **Jurisdictions**   | United States and European Union                                                   |
| **Format**          | Option C with a quantitative component and a lightweight evidence-output prototype |

# 1. Selection and Rationale

This project selects Revolut as the named regulated entity and focuses
on AI-assisted credit decisioning and credit scoring fairness across the
United States and the European Union. Revolut is a suitable case because
it presents itself as a global digital financial institution and has
public US credit product disclosures. The assignment treats the US use
case carefully as Revolut-operated or Revolut-partnered credit products,
rather than assuming Revolut is always the final legal creditor.

The choice is intentionally realistic but bounded. Revolut is a
digital-first financial services group with a public ambition to operate
globally. It has launched or supported credit-related products in
multiple markets, but the legal entity, issuer, partner-bank structure
and regulatory perimeter may differ by product and jurisdiction. That
makes Revolut useful for this assignment because the compliance function
must coordinate governance evidence even when product ownership and
legal responsibility are not identical across countries.

Revolut is also a better fit for this project than a traditional global
bank. A traditional bank may operate locally ring-fenced systems, local
data stores and separate model governance processes by national
subsidiary. A digital-first financial institution is more likely to
operate comparable product, customer onboarding and model-monitoring
workflows across markets, even when the legal creditor or partner-bank
arrangement differs. The project therefore does not assume that Revolut
uses one global credit model or one pooled customer dataset. It studies
a more realistic governance problem: how a cross-border digital
financial institution can maintain comparable credit decisioning
controls while allowing jurisdiction-specific data rights, evidence
requirements and escalation routes.

The selected domain is AI-assisted credit decisioning / credit scoring
fairness. This domain is appropriate for a RegTech assignment because it
combines model risk, consumer impact, explainability, fairness
monitoring and jurisdiction-specific compliance evidence. Credit
decisions affect access to financial services, and automated or
semi-automated decisioning can scale both useful consistency and harmful
error. A governance tool must therefore do more than report model
accuracy. It must show how evidence is produced, which data can be
accessed, which human owner is responsible and what happens when the
tool detects a weak explanation, a proxy discrimination signal or an
incomplete high-risk AI governance record.

# 2. Regulatory Divergence: US vs EU

The US and EU do not merely ask for the same model report in different
formats. The US side is anchored in adverse action explanation and fair
lending review. The EU side treats creditworthiness or credit scoring AI
as a high-risk use case and therefore asks for lifecycle governance,
data governance, technical documentation, human oversight,
record-keeping and post-deployment monitoring. That divergence drives
the tool architecture.

The political and regulatory difference is not simply technical. The US
framework places weight on individualised accountability after a credit
decision: if a person is denied credit or treated unfavourably, the
creditor must be able to identify the principal reasons in a specific
and usable form. The CFPB has made clear that use of complex algorithms
does not excuse failure to provide specific and accurate adverse action
reasons. The EU framework places greater weight on institutional
lifecycle governance: if an AI system is used for creditworthiness
assessment or credit scoring, the system falls into a high-risk
governance setting because the use case can affect access to important
economic services. These are not mutually exclusive values, but they
produce different product requirements.

A US module that only reports aggregate bias metrics would miss the
adverse-action problem. A rejected applicant needs a reason that can be
understood and challenged; a SHAP value or internal model contribution
is not enough on its own. Conversely, an EU module that only generates
individual reason codes would miss the lifecycle governance problem. A
high-risk AI system needs evidence of risk management, data governance,
human oversight, logging and monitoring before and after deployment.

The table below translates the regulatory divergence into concrete tool
design implications.

|                                 |                                                                                                                                |                                                                                                                            |                                                                                    |
|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **Theme**                       | **United States**                                                                                                              | **European Union**                                                                                                         | **Design implication**                                                             |
| **Primary regulatory question** | Can the creditor provide specific, accurate reasons for adverse action and detect fair lending risk?                           | Can the provider or deployer evidence high-risk AI governance before and after deployment?                                 | The tool needs different calculation modules, not just different report templates. |
| **Sensitive-data posture**      | US live path hard-drops direct protected attributes and relies on proxy-risk signals or separately approved privileged review. | EU audit path may use sensitive audit fields only in a segregated, lawful, access-controlled environment for bias testing. | Shared governance schema, not shared sensitive-data pipeline.                      |
| **Explanation posture**         | SHAP-style attribution is internal evidence only and must be mapped to approved reason codes.                                  | Explanation is part of broader high-risk AI transparency, documentation and oversight evidence.                            | The same model score can generate different compliance evidence.                   |
| **Lifecycle posture**           | Main tool output is an adverse action evidence package and fair lending review trigger.                                        | Main tool output is a pre-deployment evidence gate, audit bias testing, drift monitoring and human oversight workflow.     | Jurisdiction affects workflow timing, not only reporting language.                 |

# 3. Why This Needs a Jurisdiction-Aware Tool

A memo or spreadsheet can describe the regimes, but it cannot reliably
enforce data-path separation, version rule changes, produce consistent
evidence packages or escalate failures to the right owner. The prototype
therefore uses a jurisdiction_config layer, synthetic data and evidence
outputs to show how a compliance team would see different risk signals
under US and EU settings.

The main design risk is building a decorative jurisdiction selector. To
avoid that, the prototype makes the jurisdiction choice operational. US
data is physically stripped of audit-only protected fields before
analysis. EU audit data keeps sensitive audit fields only in a
controlled testing path. The US module produces reason-code and
proxy-risk evidence. The EU module produces high-risk AI governance,
bias testing and drift evidence. The output schema is shared, but the
calculations are not.

This is the central product thesis of the assignment: shared governance
schema, not shared sensitive-data pipeline. The tool shares evidence
fields such as jurisdiction, model version, rule version, risk signal,
owner, required action, deadline and audit log reference. It does not
share sensitive data access, computation modules or human review
triggers across jurisdictions. This matters because RegTech tools are
not neutral dashboards. They translate legislative and political choices
into data permissions, workflow timing and accountability structures.

# 4. Synthetic Data and Scope Boundary

The quantitative component uses synthetic data because real Revolut
customer credit data is not available. Synthetic data is suitable for
this assignment because the purpose is not to estimate Revolut's
real-world disparate impact; it is to demonstrate how a
jurisdiction-aware tool would route data, compute metrics, produce
evidence and trigger review. The figures should therefore be read as
method demonstration, not as empirical findings about Revolut or its
customers.

The scope boundary is deliberate. The project does not claim that
Revolut has one global model, one global credit policy or one global
data warehouse. It also does not claim that synthetic audit labels
represent real protected-class prevalence. Instead, it shows how a
governance monitor can enforce different data paths and evidence
obligations while remaining comparable at the management-reporting
level. This is why the prototype separates the US processed dataset from
the EU audit dataset and why the tool output uses a shared evidence
schema without pooling sensitive attributes.

# 5. References

- CFPB (Consumer Financial Protection Bureau), 2022. Consumer Financial
  Protection Circular 2022-03: Adverse action notification requirements
  in connection with credit decisions based on complex algorithms.
  Washington, D.C.: CFPB. Available at:
  <https://www.consumerfinance.gov/compliance/circulars/circular-2022-03-adverse-action-notification-requirements-in-connection-with-credit-decisions-based-on-complex-algorithms/>
  \[Accessed 22 May 2026\].

- CFPB (Consumer Financial Protection Bureau), 2023. CFPB Issues
  Guidance on Credit Denials by Lenders Using Artificial Intelligence.
  Washington, D.C.: CFPB. Available at:
  <https://www.consumerfinance.gov/about-us/newsroom/cfpb-issues-guidance-on-credit-denials-by-lenders-using-artificial-intelligence/>
  \[Accessed 22 May 2026\].

- CFPB (Consumer Financial Protection Bureau), 2025. Regulation B, 12
  CFR Section 1002.9, Notifications. Washington, D.C.: CFPB. Available
  at: <https://www.consumerfinance.gov/rules-policy/regulations/1002/9/>
  \[Accessed 22 May 2026\].

- EU AI Act, 2024. Article 10: Data and Data Governance. Available at:
  <https://www.euaiact.com/article/10> \[Accessed 22 May 2026\].

- EU AI Act, 2024. Article 14: Human Oversight. Available at:
  <https://artificialintelligenceact.eu/article/14/> \[Accessed 22 May
  2026\].

- European Commission, 2024. AI Act overview and risk-based framework.
  Brussels: European Commission. Available at:
  <https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai>
  \[Accessed 22 May 2026\].

- European Commission AI Act Service Desk, 2024. EU AI Act Annex III:
  High-risk AI systems. Brussels: European Commission. Available at:
  <https://ai-act-service-desk.ec.europa.eu/en/ai-act/annex-3>
  \[Accessed 22 May 2026\].

- Revolut, 2026a. About Revolut. London: Revolut. Available at:
  <https://www.revolut.com/en-US/about-revolut/> \[Accessed 22 May
  2026\].

- Revolut, 2026b. US Secured Credit Card disclosure. London: Revolut.
  Available at: <https://www.revolut.com/en-US/secured-creditcards/>
  \[Accessed 22 May 2026\].
