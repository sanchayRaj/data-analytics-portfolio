# Renewable Energy Usage — Tableau Dashboard

**Tier 1 project.** Energy consumption analytics dashboard built on a full cloud data pipeline — AWS S3 → Snowflake → Tableau — published live to Tableau Cloud.

## Overview

- **Data pipeline:** AWS S3 bucket (`tableau.project10`) → Snowflake storage integration (`Tableau_Integration`) + stage (`tableau_stage`) → `COPY INTO` a raw table → transformed via SQL into a final `energy_consumption` table
- **Connection:** Snowflake (`TABLEAU.ENERGY_CONSUMPTION`, warehouse `COMPUTE_WH`, schema `TABLEAU_DATA`) — connected live, then converted to an Extract before publishing
- **Tool:** Tableau Desktop, published to Tableau Cloud
- **Dataset:** Renewable_Energy_Usage_Sampled.csv, 1,000 rows × 12 columns

## Data transformation

Applied income-tier-based multipliers to `Monthly_Usage_kWh` and `Cost_Savings_USD` in SQL before the data reached Tableau — modeling the real-world pattern that higher-income segments tend to show more energy usage but proportionally less cost savings.

## Dashboard structure

**"Energy Consumption Dashboard"** — a single combined dashboard built from 6 worksheets:

| Worksheet | Metric | Breakdown |
|---|---|---|
| CSU by Country | Cost Savings (USD) | by Country |
| CSU by Region | Cost Savings (USD) | by Region |
| CSU by Energy Source | Cost Savings (USD) | by Energy Source |
| KWH Hour by Country | Monthly Usage (kWh) | by Country |
| KWH by Energy Source | Monthly Usage (kWh) | by Energy Source |
| Monthly Usage KWH by Region | Monthly Usage (kWh) | by Region |

**Design note:** Deliberately no slicer/filter control on this dashboard — each worksheet already answers a distinct question through a different breakdown dimension (Country / Region / Energy Source), unlike a cross-filtering dashboard where a single control narrows multiple charts at once. This was a considered design choice, not an oversight.

## What this project demonstrates

- A complete cloud pipeline from raw file storage through a cloud data warehouse into a BI tool: S3 → Snowflake (storage integration, stage, `COPY INTO`) → Tableau
- SQL-side data transformation (income-tier multiplier logic) applied before the data ever reaches the visualization layer
- Live-to-Extract conversion — connecting Tableau live to Snowflake first, then converting to an Extract for publishing (Tableau Public/Cloud doesn't support persistent live database connections)
- Combining 6 individual worksheets into a single cohesive dashboard
- A deliberate no-filter design choice, reasoned against the alternative (cross-filtering) rather than defaulting to it

## Files in this folder

- `RenewableEnergyUsage.twbx` — the Tableau packaged workbook
- `screenshots/` — dashboard images (add your own)
