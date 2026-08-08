# Banking Analysis — SQL + AI-Integrated Power BI Project

An end-to-end banking analytics report built on a synthetic dataset with intentionally dirty data, cleaned entirely in SQL Server through production-style views, then layered with AI-generated narrative insights — the only project in the portfolio with a dedicated AI-integration layer on top of the SQL/BI stack.

## Data Pipeline

- **Synthetic source data:** ~2,500 customers, ~10,000 transactions, deliberately dirtied with mixed casing, mixed date formats, currency stored as text, duplicate rows, and orphaned `CustomerID`s
- **Load:** SQL Server Import and Export Wizard, into pre-created `NVARCHAR`-typed staging tables (chosen specifically to preserve the dirty data rather than have it silently coerced on import)
- **Cleaning layer — two production-style SQL views:**
  - `vw_CustomersClean` — deduplicated via `ROW_NUMBER()`, standardized via `CASE`-based logic
  - `vw_TransactionsClean` — multi-format date parsing via `TRY_CONVERT` across different style codes, currency parsing via `REPLACE` + `CAST`

## Data Model

- 3 tables, including a `DateTable` built with `CALENDAR()` spanning both `AccountOpenDate` and `TransactionDate` ranges
- **Active relationship** to `TransactionDate`; **inactive relationship** to `AccountOpenDate`, activated inside the YoY New Customer Growth measure via `USERELATIONSHIP()`

## Report Structure

**2 pages, 19 visuals total**

### Page 1 — Customer Account & Overview
- **Card** — Total Customers
- **Card** — Total Balance
- **Card** — Avg Credit Score
- **Donut chart** — Customer Count by Account Type
- **Line chart** — New Customers and YoY New Customer Growth % by Year
- **AI Generated Insight text box:** *"The bank serves 2,500 customers holding a combined balance of ₹620.31M, with an average credit score of 575 — indicating a customer base skewing toward the lower-middle credit tier..."* — plus a synthetic-data disclaimer note

### Page 2 — Transaction & Cash Flow Analysis
- **Card** — Total Transactions
- **Card** — Total Txn Amount
- **Card** — Avg Txn Value
- **Card** — Success Rate
- **Donut chart** — Total Transactions by Transaction Status
- **Clustered column chart** — Total Txn Amount by Channel
- **Line chart** — Net Cash Flow by Year
- **AI Generated Insight text box:** *"Across 10,000 transactions totaling ₹993.32M, only 33.7% completed successfully — with Pending (33.5%) and Failed (32.8%) transactions together accounting for nearly two-thirds of all activity..."*

## AI Integration Layer

Structured SQL summary queries were run against the clean views and the results sent to an LLM to generate analyst-style narrative text — not decorative copy, but insight grounded directly in the query output (customer tier skew, account-type distribution, transaction success-rate anomaly). The output was placed into dedicated "AI Generated Insight" text box visuals on both pages, with an explicit synthetic-data disclaimer on Page 1.

## DAX Highlights

- `USERELATIONSHIP()` to activate the inactive `AccountOpenDate` relationship specifically for the YoY New Customer Growth measure
- Debugged a DAX row-context conflict caused by a calculated column sharing a name with a measure (`New Customers`) — resolved by removing the redundant column
- Currency (₹) formatting applied to monetary measures, percentage formatting applied to rate measures

## Tech Stack

- **SQL Server** — dirty-data staging, cleaning views, multi-format date/currency parsing
- **Power BI Desktop** — data modeling, DAX, USERELATIONSHIP time intelligence
- **LLM-generated narrative insights**, grounded in structured SQL query output

## Why This Project Stands Out

Every other project in the portfolio is SQL-cleaned and Power BI-visualized; this one adds a third layer — AI-generated narrative analysis grounded in the query output — making it the clearest demonstration of SQL + BI + AI working together rather than as three separate skills.
