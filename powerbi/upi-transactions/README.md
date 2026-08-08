# UPI Transactions Dashboard

A Power BI report analyzing UPI (Unified Payments Interface) transaction activity, built around a synchronized 10-slicer filter panel and bookmark-driven chart switching instead of static side-by-side visuals.

## Report Structure

**2 pages, 26 visuals total**

### Page 1 — Transaction & Balance Trends
- **10-slicer filter panel** (top of page): Bank Name Sent, Bank Name Received, City, Device Type, Gender, Age Group, Merchant Name, Payment Method, Purpose, Transaction Type
- **Column chart** — Transaction Amount by Month (2024)
- **Line chart** — Transaction Amount by Month (2024)
- **Bookmark navigator** — toggles between the column and line views of the same measure, so the page swaps chart type on click rather than showing both permanently
- **Column chart** — Remaining Balance by Month (2024)
- **Line chart** — Remaining Balance by Month (2024)

### Page 2 — Transaction Detail Table
- Same 10-slicer filter panel, repeated and synced with Page 1's filter context
- **Pivot table** breaking down Sum(Amount) and Sum(Remaining Balance) by Transaction Date, City, and Currency

## Bookmark-Driven Navigation

4 bookmarks drive the interactive toggle UI on Page 1:
| Bookmark | Shows |
|---|---|
| Line Chart | Transaction Amount — line view |
| Column Chart | Transaction Amount — column view |
| Balance Line chart | Remaining Balance — line view |
| Balance Column Chart | Remaining Balance — column view |

This lets a user flip between chart types for the same metric without navigating pages or losing slicer selections.

## Data Model

Single fact table: **UPI Transaction**

| Field | Role |
|---|---|
| TransactionDate | Date dimension (monthly trend axis) |
| Amount | Measure — transaction value |
| RemainingBalance | Measure — account balance after transaction |
| Currency | Dimension |
| BankNameSent / BankNameReceived | Dimension (sender/receiver bank) |
| City | Dimension |
| DeviceType | Dimension |
| Gender | Dimension |
| Age Group | Dimension |
| MerchantName | Dimension |
| PaymentMethod | Dimension |
| Purpose | Dimension |
| TransactionType | Dimension |

## Tech Stack

- **Power BI Desktop** — data modeling, DAX aggregations, bookmark configuration
- Bookmark-based interactivity for chart-type switching
- 10-dimension slicer panel synced across both report pages

## Key Design Choice

Rather than cramming both a column and a line view onto the canvas, the report uses **bookmarks + a bookmark navigator** to let the same visual real estate serve two chart types — keeping the page uncluttered while still giving the user both perspectives on demand.
