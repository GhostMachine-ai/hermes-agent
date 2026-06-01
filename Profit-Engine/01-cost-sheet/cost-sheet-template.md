# Cost Sheet — Excel Template Schema

This file documents the expected columns for `cost-sheet.xlsx`.
Create the file manually in Excel or Google Sheets using this schema.

## Columns

| Column | Type | Description |
|--------|------|-------------|
| SKU | Text | Unique product identifier (matches `price-book.json`) |
| Product Name | Text | Customer-facing name |
| Unit | Text | e.g. per seat / per month / per project |
| COGS | Currency | Cost of Goods Sold (your direct cost) |
| List Price | Currency | Full retail / rack rate |
| Floor Price | Currency | Minimum sellable price (auto-calculated from margin-rules.md) |
| Notes | Text | Any pricing exceptions or supplier notes |

## Tabs

- **Products** — one row per SKU (schema above)
- **Bundles** — package deals with aggregate COGS and bundle price
- **History** — date-stamped price changes for audit trail

## Usage

The `/profit-engine:cost-quote` command reads from `price-book.json`.
Keep that file in sync with the Products tab whenever prices change.
