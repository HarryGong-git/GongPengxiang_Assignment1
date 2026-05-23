# MH6822 Regulatory Technology — Assignment 1

Name: Gong Pengxiang  
Matriculation ID: G2505431H  
Email: GONG0093@e.ntu.edu.sg  

## Project Title

**Jurisdiction-Aware Credit Decision Governance Monitor**

## Assignment Overview

This submission designs a jurisdiction-aware RegTech governance monitor for **Revolut's AI-assisted credit decisioning / credit scoring fairness** across the **United States** and the **European Union**.

The project follows **Option C — Analytical Design with Quantitative Component**.

The core product thesis is:

> **Shared governance schema, not shared sensitive-data pipeline.**

The tool uses a shared evidence schema, rule-versioning logic and escalation workflow, while keeping US and EU data access, computation modules and review triggers jurisdiction-bound.

## Selected Entity, Domain and Jurisdictions

- **Selected regulated entity:** Revolut
- **Domain:** AI-assisted credit decisioning / credit scoring fairness / AI governance
- **Jurisdictions compared:** United States and European Union
- **Format option:** Option C — Analytical Design with Quantitative Component

## Data Generation Collaboration

Data generation collaboration: **None. Synthetic data was generated individually for this submission.**

All application data used in this project is synthetic. The figures and metrics are designed to demonstrate the governance workflow and should not be interpreted as empirical findings about Revolut or its customers.

## Folder Structure

```text
PengxiangGong_Assignment1/
├── README.md
│
├── Task1_Selection_and_Research/
│   ├── Task1_Selection_and_Research.pdf
│   ├── Task1_Selection_and_Research.docx
│   └── Task1_Selection_and_Research.md
│
├── Task2_Values_Audit/
│   ├── Task2_Values_Audit.pdf
│   ├── Task2_Values_Audit.docx
│   └── Task2_Values_Audit.md
│
└── task3/
    ├── data/
    │   ├── Task3_Synthetic_Credit_Data.csv
    │   ├── Task3_US_Processed_Data.csv
    │   └── Task3_EU_Audit_Data.csv
    │
    ├── notebook/
    │   ├── Task3_Quantitative_Analysis_Notebook.ipynb
    │   └── Task3_Quantitative_Analysis_Notebook.html
    │
    ├── figures/
    │   ├── approval_rate_by_group.png
    │   ├── reason_code_distribution.png
    │   ├── sensitivity_review_workload_stable.png
    │   └── evidence_architecture.png
    │
    ├── config/
    │   └── Task3_Jurisdiction_Config.json
    │
    ├── evidence_outputs/
    │   ├── Task3_Output_US_Evidence.csv
    │   ├── Task3_Output_EU_Evidence.csv
    │   ├── Task3_Sensitivity_Results.csv
    │   ├── Task3_US_Reason_Code_Summary.csv
    │   ├── Task3_EU_PreDeployment_Checklist.csv
    │   └── Task3_Run_Metrics.json
    │
    └── deliverables/
        ├── Task3_Tool_Design_Report/
        │   ├── Task3_Tool_Design_Report.pdf
        │   ├── Task3_Tool_Design_Report.docx
        │   └── Task3_Tool_Design_Report.md
        │
        ├── Task3_One_Page_Summary/
        │   ├── Task3_One_Page_Summary.pdf
        │   ├── Task3_One_Page_Summary.docx
        │   └── Task3_One_Page_Summary.md
        │
        ├── Task3_Senior_Management_Presentation/
        │   ├── Task3_Senior_Management_detailed_slides.pptx
        │   ├── RegTech_Presentation_GongPengxiang.pptx
        │   ├── RegTech_Presentation_GongPengxiang.pdf
        │   └── Presentation_video.mp4
        │
        ├── Task3_Regulatory_Mapping_Table/
        │   ├── Task3_Regulatory_Mapping_Table.pdf
        │   ├── Task3_Regulatory_Mapping_Table.md
        │   └── Task3_Regulatory_Mapping_Table.csv
        │
        └── Task3_Model_Card_or_Tool_Card/
            ├── Task3_Model_Card_or_Tool_Card.pdf
            └── Task3_Model_Card_or_Tool_Card.md
```

## How to Review the Submission

### Task 1

Open:

```text
Task1_Selection_and_Research/Task1_Selection_and_Research.pdf
```

This file explains the selected entity, selected domain, US/EU jurisdictional comparison and references.

### Task 2

Open:

```text
Task2_Values_Audit/Task2_Values_Audit.pdf
```

This file answers the four values-audit questions required by the assignment.

### Task 3 Main Deliverables

Open the following files:

```text
task3/deliverables/Task3_Tool_Design_Report/Task3_Tool_Design_Report.pdf
task3/deliverables/Task3_One_Page_Summary/Task3_One_Page_Summary.pdf
task3/deliverables/Task3_Senior_Management_Presentation/Task3_Senior_Management_Presentation.pdf
task3/deliverables/Task3_Regulatory_Mapping_Table/Task3_Regulatory_Mapping_Table.pdf
task3/deliverables/Task3_Model_Card_or_Tool_Card/Task3_Model_Card_or_Tool_Card.pdf
```

The `.docx`, `.md` and/or `.csv` companion files are included where available for editability, transparency and traceability.

## How to Review the Quantitative Analysis

Open and run:

```text
task3/notebook/Task3_Quantitative_Analysis_Notebook.ipynb
```

The notebook reads input data from:

```text
task3/data/
```

and uses or generates evidence outputs under:

```text
task3/evidence_outputs/
```

A static rendered version is also provided:

```text
task3/notebook/Task3_Quantitative_Analysis_Notebook.html
```

## Data Files

The synthetic data files are located under:

```text
task3/data/
```

Files:

- `Task3_Synthetic_Credit_Data.csv`
- `Task3_US_Processed_Data.csv`
- `Task3_EU_Audit_Data.csv`

The synthetic dataset contains **1,400 synthetic applications**:

- **700 US processed records**
- **700 EU audit records**

The US processed dataset hard-drops direct protected / audit-only fields, including:

- `age`
- `gender_audit`
- `age_band`
- `protected_group_flag`
- `audit_group`

The EU audit dataset retains audit-only fields only for controlled bias testing in a segregated audit path.

## Evidence Outputs

The evidence outputs are located under:

```text
task3/evidence_outputs/
```

Files:

- `Task3_Output_US_Evidence.csv`
- `Task3_Output_EU_Evidence.csv`
- `Task3_Sensitivity_Results.csv`
- `Task3_US_Reason_Code_Summary.csv`
- `Task3_EU_PreDeployment_Checklist.csv`
- `Task3_Run_Metrics.json`

The US and EU evidence files use a shared evidence schema while producing jurisdiction-bound risk signals and owners.

## Jurisdiction Configuration

The jurisdiction configuration file is located at:

```text
task3/config/Task3_Jurisdiction_Config.json
```

It stores rule IDs, jurisdiction, legal / policy basis, data-access posture, computation modules, required outputs, human-review triggers, owners, versions, effective dates, approval status and rollback mechanisms.

## Figures

Reusable figures are stored under:

```text
task3/figures/
```

These figures support the notebook, report and senior-management presentation.

## Important Scope Boundaries

This project does **not** claim that:

- Revolut uses one global credit model.
- Revolut uses one pooled global sensitive-data pipeline.
- The synthetic metrics represent real Revolut customer outcomes.
- SHAP-style attribution is legally sufficient for adverse action notices.
- The tool certifies legal compliance or EU AI Act conformity.
- The tool makes final credit decisions.
- The tool automatically repairs model bias.

The tool supports evidence generation, jurisdiction-bound monitoring, risk-tiered escalation and management review.
