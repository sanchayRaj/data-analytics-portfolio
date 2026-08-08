# Housing Market Dashboard

A 3-page Power BI report analyzing residential housing sales data — pricing trends, regional performance, and property-type breakdowns — sourced from Google BigQuery, with a Key Influencers AI visual used to surface what actually drives purchase price.

## Report Structure

**3 pages, 20 visuals total**

### Page 1 — House Market Overview
- **Line chart** — YoY Growth in Sales, by Sales Type
- **Scatter chart** — Offer Price vs. Purchase Price (pricing gap / negotiation spread)
- **Card** — Units Sold in Latest Year & Quarter
- **Card** — Last Sales
- **Bar chart** — Median Sales Price Change by Region

### Page 2 — Sales Performance
- **Donut chart** — Average Price per SQM by Region
- **Bar chart** — Sales by Region
- **Bar chart** — Offer Price to Price-per-SQM ratio, by Sales Type
- **Key Influencers AI visual** — explains Purchase Price using Age as an influencing factor (Power BI's built-in AI visual, not a custom-built model)
- **Table** — Date, Total YTD Sales, and Purchase Price detail

### Page 3 — House Type
- **Combo chart (line + clustered column)** — SQM and Price-per-SQM by House Type
- **3 slicers** — City, Region, Area
- **Clustered bar chart** — Offer Price vs. Purchase Price by House Type
- **Clustered bar chart** — Annual Inflation Rate %, Yield on Mortgage Credit Bonds %, and Nominal Interest Rate % by House Type (macroeconomic overlay on housing figures)

## Data Model

Source: **Google BigQuery**

Key fields used across the report: `sales_type`, `region`, `city`, `area`, `house_type`, `date`, `Offer Price`, `purchase_price`, `sqm`, `sqm_price`, plus macroeconomic fields (`dk_ann_infl_rate%`, `yield_on_mortgage_credit_bonds%`, `nom_interest_rate%`) and derived measures (`YOY_GROWTH_SALES`, `Median Sales Price Change`, `AVG Price per SQM`, `TOTALYTD SALES`).

## Tech Stack

- **Google BigQuery** — cloud data source
- **Power BI Desktop** — data modeling and DAX measures (YoY growth, TOTALYTD)
- **Key Influencers visual** — Power BI's built-in AI visual for driver analysis on Purchase Price
- Multi-page layout: overview → regional performance → property-type deep dive

## Key Design Choice

The macroeconomic overlay on Page 3 (inflation rate, mortgage bond yield, interest rate — all sliced by house type) ties housing price movement back to broader economic conditions rather than treating the dataset as sales figures in isolation.
