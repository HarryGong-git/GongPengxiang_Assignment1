Name: Pengxiang Gong
Matriculation ID: G2505431H
Email: GONG0093@e.ntu.edu.sg

# Jurisdiction-Aware Credit Decision Governance Monitor

Selected entity: Revolut
Domain: AI-assisted credit decisioning / credit scoring fairness / AI governance
Jurisdictions: United States and European Union
Assignment format: Option C - Analytical Design with Quantitative Component

## Project thesis

The tool uses a shared governance schema, not a shared sensitive-data pipeline.
In the US, it focuses on adverse action reason quality, proxy discrimination risk
and fair lending review. In the EU, it assumes creditworthiness AI is a high-risk
AI use case and focuses on controlled bias testing, pre-deployment governance
evidence and post-deployment monitoring.

## Data disclaimer

All application data used in this project is synthetic. The figures are designed
to demonstrate the governance workflow and should not be interpreted as
empirical findings about Revolut or its customers.

## How to review the quantitative analysis

1. Open `task3/notebook/Task3_Quantitative_Analysis_Notebook.ipynb`.
2. Run all cells from the `task3/notebook/` folder.
3. The notebook reads data from `../data/` and generated outputs from `../outputs/`.
4. Open `task3/notebook/Task3_Quantitative_Analysis_Notebook.html` for a static rendered version.

## Figures

Generated figures are stored in `task3/figures/`:

- `approval_rate_by_group.png`
- `reason_code_distribution.png`
- `sensitivity_workload.png`
- `evidence_architecture.png`

## PDF companion files

Each PDF remains in its original location. Next to each PDF, there is a same-name
folder containing a `.docx` and `.md` companion version extracted from the PDF.

Examples:

- `Task1_Selection_and_Research.pdf`
- `Task1_Selection_and_Research/Task1_Selection_and_Research.docx`
- `Task1_Selection_and_Research/Task1_Selection_and_Research.md`
- `task3/outputs/Task3_Tool_Design_Report.pdf`
- `task3/outputs/Task3_Tool_Design_Report/Task3_Tool_Design_Report.docx`
- `task3/outputs/Task3_Tool_Design_Report/Task3_Tool_Design_Report.md`

The same companion pattern is used for Task 2, the one-page summary, regulatory
mapping table, tool card, senior management presentation, and detailed senior
management presentation.

Companion folders:

- `Task1_Selection_and_Research/`
- `Task2_Values_Audit/`
- `task3/outputs/Task3_Tool_Design_Report/`
- `task3/outputs/Task3_One_Page_Summary/`
- `task3/outputs/Task3_Senior_Management_Presentation/`
- `task3/outputs/Task3_Senior_Management_Presentation_Detailed/`
- `task3/outputs/Task3_Regulatory_Mapping_Table/`
- `task3/outputs/Task3_Model_Card_or_Tool_Card/`

## File list

- `README.md`
- `Task1_Selection_and_Research.pdf`
- `Task1_Selection_and_Research/Task1_Selection_and_Research.docx`
- `Task1_Selection_and_Research/Task1_Selection_and_Research.md`
- `Task2_Values_Audit.pdf`
- `Task2_Values_Audit/Task2_Values_Audit.docx`
- `Task2_Values_Audit/Task2_Values_Audit.md`
- `task3/notebook/Task3_Quantitative_Analysis_Notebook.ipynb`
- `task3/notebook/Task3_Quantitative_Analysis_Notebook.html`
- `task3/data/Task3_Synthetic_Credit_Data.csv`
- `task3/data/Task3_US_Processed_Data.csv`
- `task3/data/Task3_EU_Audit_Data.csv`
- `task3/figures/approval_rate_by_group.png`
- `task3/figures/reason_code_distribution.png`
- `task3/figures/sensitivity_workload.png`
- `task3/figures/evidence_architecture.png`
- `task3/outputs/Task3_Tool_Design_Report.pdf`
- `task3/outputs/Task3_One_Page_Summary.pdf`
- `task3/outputs/Task3_Senior_Management_Presentation.pdf`
- `task3/outputs/Task3_Senior_Management_Presentation_Detailed.pptx`
- `task3/outputs/Task3_Senior_Management_Presentation_Detailed.pdf`
- `task3/outputs/Task3_Jurisdiction_Config.json`
- `task3/outputs/Task3_Regulatory_Mapping_Table.pdf`
- `task3/outputs/Task3_Regulatory_Mapping_Table.csv`
- `task3/outputs/Task3_Model_Card_or_Tool_Card.pdf`
- `task3/outputs/Task3_Output_US_Evidence.csv`
- `task3/outputs/Task3_Output_EU_Evidence.csv`
- `task3/outputs/Task3_Sensitivity_Results.csv`
- `task3/outputs/Task3_EU_PreDeployment_Checklist.csv`
- `task3/outputs/Task3_US_Reason_Code_Summary.csv`
- `task3/outputs/Task3_Run_Metrics.json`
