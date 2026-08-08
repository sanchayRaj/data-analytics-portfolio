# Student Depression & Lifestyle Factors

A Tableau workbook exploring how everyday student lifestyle factors — academic pressure, financial stress, sleep, study hours, and study satisfaction — distribute across the student population, cleaned in SQL Server and published to Tableau Public.

## Data Source & Cleaning

- Cleaned in **SQL Server**, then loaded into Tableau via a **Tableau Desktop extract** (`.hyper` file, not a live connection) — chosen for performance and to make the published workbook self-contained
- Published to **Tableau Public**

## Worksheets

Each worksheet plots one lifestyle/academic factor against **student count**, using distinct mark types to differentiate the views at a glance:

| Worksheet | Factor (X-axis) | Metric | Mark Type |
|---|---|---|---|
| AP & SC | Academic Pressure | Student Count | Square |
| FS & SC | Financial Stress | Student Count | Circle |
| SD & SC | Sleep Duration | Student Count | Circle (with trend line) |
| SH & SC | Study Hours | Student Count | Area |
| SS & SC | Study Satisfaction | Student Count | Automatic (bar) |

*("SC" = Student Count throughout — each sheet is a distribution of how many students fall at each level of that factor.)*

## Fields Used

- `Academic_Pressure`, `Financial_Stress`, `Sleep_Duration`, `Study_Hours`, `Study_Satisfaction` — the core lifestyle/academic variables
- `Age_Group` — demographic breakdown
- `Dietary_Habits` — lifestyle variable
- `Family_History_of_Mental_Illness` (boolean), `Have_you_ever_had_suicidal_thoughts` (boolean) — background/context fields in the source dataset
- `Index_Column` — used purely as a count key to derive student counts per group

## Design Notes

- Each worksheet uses a distinct color and mark shape (green squares, pink circles, gold circles with a trend line, purple area, red bars) so the five views read as a coherent but individually distinguishable set when placed together
- The Sleep Duration view includes a trend line overlay to highlight the shape of the distribution rather than just raw counts

## Tech Stack

- **SQL Server** — source data cleaning
- **Tableau Desktop** — extract-based workbook, published to **Tableau Public**

## Note on Dataset

This uses a public student mental-health/lifestyle dataset for portfolio and analytical-technique demonstration purposes (distribution analysis, extract-based publishing, multi-mark-type worksheet design) — it is not a clinical or diagnostic tool.
