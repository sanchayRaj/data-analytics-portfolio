# Loan Default — Power BI Dashboard

**Heaviest DAX showcase project.** Dataflow-sourced loan portfolio analytics dashboard spanning 3 pages, with the deepest DAX measure count of any project in this portfolio — ~13 measures covering time intelligence, filtered/conditional aggregation, rate calculations, and category breakdowns.

## Overview

- **Data source:** SQL Server → Power BI Dataflow (Gen 1) → Power BI Desktop. Data was first loaded and shaped in a Dataflow before being consumed by the report, rather than connecting Power BI directly to SQL — a different ingestion pattern from the rest of this portfolio's projects.
- **Dataset:** Loan_default, 255,347 rows × 19 columns (LoanID, Age, Income, LoanAmount, CreditScore, MonthsEmployed, NumCreditLines, InterestRate, LoanTerm, DTIRatio, Education, EmploymentType, MaritalStatus, HasMortgage, HasDependents, LoanPurpose, HasCoSigner, Default, Loan Date)
- **Pages:** 3 — Loan Default Overview, Applicant Demographic & Financial Profile, Financial Risk Metrics
- **Refresh:** Incremental refresh configured (5-year retention window, 10-day refresh window, detect data changes enabled) — a production-scale consideration beyond a static one-off dashboard
- **Design note:** Deliberately no slicers on this report — each page is built to answer a specific question through its visuals directly, rather than relying on interactive filtering

## Calculated columns

- `Age_Groups` — bucketed age ranges
- `Credit Score Bins` — Very Low (≤400), Low (≤450), Medium (≤650), High (>650)
- `Income Bracket` — Low (<30,000), Medium (<60,000), High (≥60,000)

All three built using the `SWITCH(TRUE())` pattern.

## Pages

### 1. Loan Default Overview
- Loan Amount by Purpose, split by Age Group and by Loan Purpose (2 line charts)
- Default Rate by Employment Type (line chart)
- Average Income by Employment Type (line chart)
- Default Rate by Year (line chart, time intelligence)

### 2. Applicant Demographic & Financial Profile
- Loan Amount by Credit Score Bins (line chart)
- Average Loan Amount (High Credit) by Age Group × Marital Status (donut chart)
- Loans by Education Category (line chart)
- Total Loan Amount (Middle Age) by Mortgage/Dependents status (clustered column chart)
- Median Loan Amount by Credit Score Bins (line chart)

### 3. Financial Risk Metrics
- YOY Loan Amount Change (line chart, time intelligence)
- YOY Default Loans Change (line chart, time intelligence)
- YTD Loan Amount by Credit Score Bins × Marital Status (ribbon chart)
- **Decomposition Tree:** Loan Amount broken down by Income Bracket → Employment Type — lets a viewer interactively drill into what's driving loan amount, powered by Power BI's AI-assisted decomposition tree visual

## Key DAX measures

- **Time intelligence:** `YOY Default Loans Change`, `YOY on Loan Amount Change`, `YTD Loan Amount`
- **Filtered/conditional measures:** `Average Loan Amount (High Credit)`, `Total Loan (Middle Age)`
- **Rate calculations:** `Default Rate By Year`, `Default Rate By Employment Type`
- **Category aggregations:** `Median by credit score bins`, `Average income by Employment Type`, `Loan Amount by Credit Bins`, `Loans By Education Category`, `Loan Amount By Purpose`

## What this project demonstrates

- Dataflow (Gen 1) as a data ingestion layer between SQL Server and Power BI — a different pipeline pattern from directly connecting to a live source
- The deepest DAX footprint in this portfolio — CALCULATE, filter context, and time intelligence functions used across nearly every visual on all 3 pages
- Incremental refresh configuration — a real production consideration for large, growing datasets (255K+ rows), not something a typical portfolio project bothers to set up
- Use of Power BI's Decomposition Tree AI visual for interactive root-cause style drill-down, alongside standard chart types
- A deliberate design choice to build slicer-free, purpose-built pages rather than defaulting to a generic filterable dashboard

## Files in this folder

- `LoanDefault.pbix` — the Power BI report file
- `screenshots/` — report page images (add your own)
