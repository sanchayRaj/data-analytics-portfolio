# Prism Insurance — Power BI Dashboard

**Flagship project.** SQL-sourced insurance analytics dashboard with a custom dark theme, KPI cards, ribbon/bar/line/donut visuals, a pivot table breakdown, and a dedicated customer feedback page powered by a sentiment analysis pipeline.

## Overview

- **Data source:** SQL Server (InsuranceData + Feedbacks tables)
- **Tool:** Power BI Desktop, published to Power BI Service
- **Theme:** Innovate (dark theme — #3a3a3a background, white foreground)
- **Pages:** 3 — Dashboard, Raw, Feedback

## Pages

### 1. Dashboard
The main analytical view. Includes:
- **KPI cards:** Total Premium Amount, Total Coverage Amount, Total Claim Amount
- **Slicers:** Policy Number, Claim Number, Customer ID, Gender — lets a viewer drill into any individual policy or segment
- **Ribbon chart:** Claim Status distribution over time/rank
- **Bar chart:** Premium Amount by Policy Type
- **Line chart:** Claim Amount by Age Group
- **Donut chart:** Active vs. Inactive policy split
- **Pivot table:** Coverage Amount broken down by Policy Type × Claim Status — cross-tab view for detailed comparison

### 2. Raw
A full flat table of the underlying InsuranceData (Policy Number, Customer ID, Claim Number, Age, Gender, Coverage/Premium/Claim Amounts, Policy Start/End Dates, Policy Type, Claim Status, Claim Date, Age Group, Active/Inactive) with a navigation button back to the Dashboard — included so a reviewer can see the exact source-level data behind every visual.

### 3. Feedback
The sentiment analysis layer:
- **Word Cloud** (custom visual) built from customer feedback text
- **Bar chart:** feedback categorized as Good vs. Improvement
- **Table:** individual feedback entries paired with Customer Name and a sentiment score

## What this project demonstrates

- Connecting Power BI directly to a SQL Server data source across two related tables (transactional insurance data + a separate feedback table)
- Custom dark-theme report design applied consistently across all 3 pages
- Practical use of slicers as a drill-down mechanism (Policy/Claim/Customer/Gender) rather than just decorative filters
- A pivot table for cross-tab analysis alongside standard chart visuals — shows comfort with both visual and tabular BI patterns
- **Sentiment analysis workaround:** Power BI's built-in AI Insights visual requires a paid license. Instead of skipping the sentiment layer, feedback text was scored externally (Python + TextBlob) and the resulting sentiment score was brought into the model as a `Score sentiment` column — solving a real tooling constraint rather than a textbook "ideal-conditions" build
- A custom Word Cloud visual, plus an imported Inforiver Charts custom visual package, showing comfort going beyond Power BI's default visual set
- Publishing to Power BI Service (live report, not just a local .pbix)

## Files in this folder

- `PrismInsurance.pbix` — the Power BI report file
- `screenshots/` — report page images (add your own)
