# Rainfall Analysis — Power BI Dashboard

Agricultural climate analytics dashboard built on a full cloud data pipeline — AWS S3 → Snowflake → Power BI — with 4 pages breaking down rainfall, temperature, humidity, and crop yield across crops, seasons, locations, and years.

## Overview

- **Data pipeline:** AWS S3 bucket → Snowflake (storage integration + stage + `COPY INTO`) → Power BI Desktop
- **Table:** AGRICULTURE
- **Pages:** 4 — Rainfall Analysis, Temperature Analysis, Humidity Analysis, Yield Analysis
- **Filter:** A single Season slicer, synced across all 4 pages — change it once, every page updates together

## Pages

Each page follows the same consistent structure, letting a viewer compare the same metric across four different dimensions:

| Page | Metric | Breakdown charts |
|---|---|---|
| **Rainfall Analysis** | RAINFALL | by Crops, by Season, by Location (bar charts) + by Year (line chart) |
| **Temperature Analysis** | TEMPERATURE | by Crops, by Season, by Location (bar charts) + by Year (line chart) |
| **Humidity Analysis** | HUMIDITY | by Crops, by Season, by Location (bar charts) + by Year (line chart) |
| **Yield Analysis** | YEILDS | by Crops, by Season, by Location (bar charts) + by Year (line chart) |

## Notable fixes made during the build

- **Year field summarization:** Power BI defaulted the Year column to Sum aggregation on first load (which is meaningless for a year value) — corrected to "Don't summarize."
- **Chart type correction:** Year-based visuals were initially bar charts, converted to line charts to properly show trend over time rather than implying discrete unrelated categories.

## What this project demonstrates

- A full end-to-end cloud data pipeline: raw files in S3, loaded into Snowflake via a storage integration and stage, then consumed by Power BI — not just a direct file-to-report connection
- A consistent multi-page report structure (same visual layout pattern repeated across 4 metrics) — shows deliberate design thinking rather than one-off page-by-page decisions
- Cross-page slicer synchronization for a coherent multi-page filtering experience
- Practical debugging of default Power BI behaviors (auto-summarization, wrong default chart type) that aren't obvious to someone new to the tool

## Files in this folder

- `RainfallAnalysis.pbix` — the Power BI report file
- `screenshots/` — report page images (add your own)
