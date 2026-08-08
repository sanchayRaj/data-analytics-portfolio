# UPI Transaction Overview

A Tableau workbook giving a quick multi-angle overview of UPI transaction activity — spend by payment method (drilling into merchant), transaction volume by customer age bracket, and geographic spend by city.

## Worksheets

### Amount By Payment Method
- **Hierarchical column shelf:** Payment Method → Merchant Name (drill-down from method into individual merchants)
- **Color:** Payment Method
- **Label:** Sum of Amount
- Lets you see total spend per payment method, then expand into which merchants drove it

### Transaction By Age Group
- Uses a **calculated field** to bucket customers into three age groups:
  ```
  IF [CustomerAge] <= 25 THEN 'Age Group 1'
  ELSEIF [CustomerAge] <= 35 THEN 'Age Group 2'
  ELSE 'Age Group 3'
  END
  ```
- **Metric:** Count of Transaction ID per age group

### Transaction by Amount City
- **Map visual** using Tableau's generated Latitude/Longitude for `City`
- **Color & label:** City
- **Label:** Sum of Amount
- Geographic view of where transaction value is concentrated

## Data Fields

`Amount`, `PaymentMethod`, `MerchantName`, `City`, `CustomerAge`, `CustomerAccountNumber`, `Currency`, `DeviceType`, `TransactionID` — plus the derived `Age Group` calculated field.

## Design Notes

This workbook is intentionally lean — three focused worksheets rather than one dense dashboard, each isolating a single angle (payment method, demographic, geography) so each can also be dropped into a larger dashboard individually.

## Tech Stack

- **Tableau Desktop** — calculated fields, geographic mapping (auto-generated lat/long), hierarchical drill-down shelf
