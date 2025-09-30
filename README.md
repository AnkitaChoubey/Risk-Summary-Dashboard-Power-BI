# Risk Summary Dashboard

A clean, interactive dashboard to track and analyze project risks and opportunities by owner, severity, likelihood, status and weighted risk score.


## Table of contents
- [Project overview](#project-overview)  
- [Goals and audience](#goals-and-audience)  
- [Key metrics & KPIs](#key-metrics--kpis)  
- [Dashboard pages & interactions](#dashboard-pages--interactions)  
- [Data model & sources](#data-model--sources)  
- [How to run / reproduce locally](#how-to-run--reproduce-locally)  
- [Folder structure](#folder-structure)

## Project overview
This repository contains everything needed to reproduce the "Risk Summary" dashboard: the Power BI report file (.pbix), sample datasets, ETL/preprocessing scripts, and documentation. The dashboard surfaces counts of open risks, aggregated severity & likelihood, owner-level rankings, stacked risk-level charts by likelihood, weighted risk scores, and a detailed table for operational use.

## Dashboard Preview
 <img width="1198" height="697" alt="Dashboard Image" src="https://github.com/user-attachments/assets/ad868086-5be4-44de-acfc-c3f0e85d1843" />



## Goals and audience
- Provide executives and project managers a quick summary of active risks.
- Enable risk owners to drill into their assigned items and monitor mitigation status.
- Support prioritization using weighted risk scores (e.g., severity × likelihood).

Audience: PMO, Risk Managers, Project Leads.


## Key metrics & KPIs
- *Total Open Risks* — count of IsOpen == True (shown: 500)
- *Sum of Severity* — total severity/impact
- *Sum of Likelihood* — aggregated likelihood
- *Count of risks per owner* (bar chart)
- *Weighted risk score* — sum of (Severity × Likelihood) per owner
- *Risk level composition* — proportion of High/Medium/Low risks by Likelihood
- *Status breakdown* — Open / In Progress / Closed (pie/donut)
- *Full Risk Details* — table for filtering and export

---

## Dashboard pages & interactions
- *Filter pane*: Owner, Status, Likelihood to slice everything.
- *Top KPIs*: Big numeric tiles for Open count, severity and likelihood totals.
- *Owner ranking*: Horizontal bars for count of risks and weighted score.
- *Stacked bars*: Risk level (High/Medium/Low) by Likelihood (1–5).
- *Table*: Searchable/exportable risk details with Mitigation Plan and Status.
- Export to CSV / Print from Power BI.

---

## Data model & sources
Primary table risks with these suggested columns:
- RiskID (int)
- RiskDescription (text)
- Owner (text)
- Severity (int) — e.g., 1–5 or 1–10
- Likelihood (int) — e.g., 1–5
- Status (text) — Open, In Progress, Closed
- IsOpen (bool) — derived (Status != 'Closed')
- MitigationPlan (text)
- CreatedDate, UpdatedDate
- RiskCategory (text) — Critical / Low / Moderate

Example data sources:
- CSV / Excel export from risk register
- Database: SQL Server / PostgreSQL table risks
- API from risk management tools

---

## How to run / reproduce locally

### Option A — Open Power BI (recommended)
1. Install Power BI Desktop.
2. Open ./powerbi/Risk-Summary.pbix.
3. If using the included sample CSV, Power BI will load it automatically. If you use your own data, update the data source in Power BI (Home > Transform data > Data source settings).

## Suggested Power BI measures (DAX)

Is Open Count = CALCULATE (COUNT('risks'[RiskID]), 'risks'[IsOpen] = 1)

Sum Severity = SUM ('risks'[Severity])

Sum Likelihood = SUM ('risks'[Likelihood])

Risk Score = SUMX ('risks', 'risks'[Severity] * 'risks'[Likelihood])

## Connect With Me

If you liked this project or want to collaborate, connect with me on:

 [LinkedIn]( https://www.linkedin.com/in/ankita-c-4a1581212) | [GitHub](https://github.com/AnkitaChoubey/AnkitaChoubey)
