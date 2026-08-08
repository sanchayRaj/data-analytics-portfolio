# Production Dashboard

An Excel dashboard analyzing manufacturing production data — units produced, cost, and workforce breakdowns — built entirely with pivot tables, linked pivot charts, and slicers (no Power Query/DAX layer; pure native Excel).

## Workbook Structure

**6 sheets:** Pivot 1, Pivot 2, Pivot 3, Pivot 4, Sheet4, Production Dataset (raw data)

## Pivot Tables & Charts

| Pivot Table | Linked Chart | Chart Title |
|---|---|---|
| PivotTable1 | Bar chart (3D) | Total Product Cost By Product Type |
| PivotTable1 | Bar chart (3D) | Number of Tasks by Manager |
| PivotTable1 | Line chart (3D) | Total Units Produced By Year/Month |
| PivotTable2 | Pie chart (3D) | Average Production Cost Per Unit By Product Type |

*(Charts 1–4 are mirrored on a second pivot sheet, giving 8 chart objects total across the workbook — 4 unique views, each placed twice.)*

## Slicers

4 slicers filter across the linked pivot tables:
- Production Date
- Region
- Gender
- Age Groups

## Data Model

Single source table: **Production Dataset** (120 rows)

| Field | Type |
|---|---|
| ProductionID | Key |
| ProductionDate | Date dimension |
| Region | Dimension |
| Manager | Dimension |
| ProductType | Dimension |
| UnitsProduced | Measure |
| TotalCost | Measure |
| Gender | Dimension |
| True Age | Measure |
| Age Groups | Dimension (bucketed) |
| Production Cost Per Unit | Calculated measure |

## Tech Stack

- **Excel** — native PivotTables, PivotCharts, and slicers
- No Power Query or DAX — all aggregation handled through pivot table grouping

## Known Issue / Cleanup Note

All 4 charts are currently rendered in **3D** (3D bar, 3D line, 3D pie). 3D charts are generally discouraged in BI/data-viz best practice — they distort value perception (especially pie and bar) and add no analytical value. **Flagged for conversion to standard 2D charts** before this is showcased as a portfolio piece.
