# AzureDatabase — Men's T-Shirt/Shirt Brand Analysis

A 2-page Power BI report built on a scraped men's apparel dataset, cleaned and served from **Azure SQL Database**, with a custom-themed layout and two custom visuals (Multi Info Cards, Scrolling Text) for a more polished, non-default look.

## Report Structure

**2 pages, 7 visuals total**

### Page 1 — Brands
- **Slicer** — Brand (landing page filter, feeds selection into Page 2)

### Page 2 — Brand Details
- **Pie chart** — Profit % by Brand
- **Scrolling Text visual** (custom) — Brand ticker, used as a polish/attention element
- **Area chart** — Profit % trend by Brand
- **Donut chart** — Title (product count) by Brand
- **Ribbon chart** — Sales Price by Brand (rank-over-category visual)
- **Bar chart** — Discount Percentage by Brand

## Custom Visuals

| Visual | Purpose |
|---|---|
| **Multi Info Cards** | Imported custom visual for compact multi-metric cards |
| **Scrolling Text (Scroller)** | Imported custom visual — animated brand name ticker on the detail page |

## Data Pipeline & Cleaning

- **Source:** scraped men's T-shirt/shirt e-commerce dataset (1,445 rows), loaded into **Azure SQL Database**
- **Connection fix:** resolved a Named Pipes vs. TCP protocol issue in SSMS by connecting via the fully qualified `.database.windows.net` server name
- **Cleaning done in Azure SQL:** stripped ₹ currency symbols, parsed comma-formatted numbers, converted string `"NA"` placeholders to real NULLs, removed junk rows and duplicates

## DAX Measures

- **Discount Percentage** — `DIVIDE()`-based measure comparing list price to sale price. Required the third `DIVIDE` argument to be a constant (`0`/`BLANK()`) rather than a column reference — a common DIVIDE syntax trap.
- **Profit %** — synthetic measure using `RANDBETWEEN()`, since the source dataset had no cost/COGS field to calculate real margin from. Documented as synthetic, not a real profitability figure.

## Publishing

Published twice as a distribution exercise:
- To the standard **Power BI Service** workspace
- As a **Power BI App** in a separate workspace, to practice the full packaging/distribution lifecycle

## Tech Stack

- **Azure SQL Database** — cloud data source, SSMS-based cleaning
- **Power BI Desktop** — data modeling, DAX, custom visual integration
- 2 imported custom visuals for a distinct, non-default report look
