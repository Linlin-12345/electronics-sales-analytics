# Data dictionary — electronic_sales_data.xlsx

19,999 transaction rows · 12,135 unique customers · Sep 2023 – Sep 2024.
Source: *Customer Purchase Behavior – Electronic Sales Data* (Kaggle). Synthetic (Faker-generated); no real PII.

| Column | Type | Notes |
|---|---|---|
| Customer ID | int | Repeats — one customer can have up to 8 transactions |
| Age | int | Customer age in years |
| Gender | str | Male / Female |
| Loyalty Member | str | Yes / No — **can change across a customer's transactions** (signup / churn) |
| Product Type | str | Smartphone, Laptop, Tablet, Smartwatch, Headphones |
| SKU | str | Product code |
| Rating | int | 1–5 stars (no nulls) |
| Order Status | str | Completed / Cancelled |
| Payment Method | str | Credit Card, Paypal, Cash, etc. |
| Total Price | float | Transaction total |
| Unit Price | float | Price per unit |
| Quantity | int | Units purchased |
| Purchase Date | date | YYYY-MM-DD |
| Shipping Type | str | Standard, Express, Overnight, Same Day, Expedited |
| Add-ons Purchased | str | Comma-separated add-on items (nullable) |
| Add-on Total | float | Total add-on spend |

## Engineered features (in the notebook)
- `loyalty_num`, `is_cancelled` — binary encodings
- `generation` — Gen Z / Millennial / Gen X / Boomer age bands
- `addon_ratio` = Add-on Total ÷ Unit Price
- Customer-level **RFM**: frequency, recency_days, monetary
- **Loyalty movement**: signed up / cancelled / no change across a customer's own history
