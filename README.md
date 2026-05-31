# Electronic Sales Analytics — Loyalty, Upselling & Demographics

Statistical analysis of **19,999 electronics-retail transactions** (Sep 2023 – Sep 2024) covering customer loyalty, add-on upselling, and demographic spending behaviour. Built with Python (`pandas`, `scipy`, `statsmodels`, `seaborn`) and cross-checked in SPSS.

The work is deliberately **honest about null results**: two of the three questions return no effect, and one analysis *overturns* an intuitive claim. Reporting that — rather than over-fitting a narrative — is the point.

---

## Headline finding — the "headphone paradox"

Add-on spend is driven by **product type**, not price or loyalty status. Headphones, despite being a low-priced device, pull the **highest** average add-on spend (\$82.64); smartphones, the highest-volume category, pull the **lowest** (\$55.37). One-way ANOVA: **F = 84.7, p < .001**.

![Add-on analysis](figures/rq2_addons.png)

The right panel matters: loyalty members do **not** spend more on add-ons (\$62.32 vs \$62.23, p = .92). A common assumption — that the loyalty card lifts upsell — does not hold in this data.

---

## The three questions

| # | Question | Method | Result |
|---|----------|--------|--------|
| **RQ1** | What drives loyalty-programme membership? | t-test, χ², logistic regression | **True null** — pseudo-R² ≈ 0; membership is unrelated to ratings, cancellations, or demographics. |
| **RQ2** | Which products drive add-on upselling? | One-way ANOVA + Tukey HSD | **Significant** — product type sets the add-on ceiling (headphone paradox). |
| **RQ3** | Do age & gender shape spend / shipping? | t-test, cross-tab, heatmap | **Weak** — gender p = .45; shipping mix near-flat across generations. |

### RQ1 — loyalty is a snapshot null, but movement exists over time
The cross-sectional tests find nothing, which is the *correct* answer for a synthetically generated loyalty flag. The more interesting structure only appears once rows are treated as **transactions, not customers** (12,135 unique customers, some with up to 8 purchases): **963 customers cancelled** their membership and **930 signed up** across their own purchase histories — the churn signal a flat snapshot cannot see.

![Loyalty analysis](figures/rq1_loyalty.png)

### RQ3 — uniform premium pricing
High-commitment categories (smartphones, smartwatches) command premium prices evenly across every generation; no actionable demographic segmentation surfaces here.

![Demographics analysis](figures/rq3_demographics.png)

---

## What this project demonstrates

- **Statistical discipline** — choosing the right test per question (parametric t-test, χ² independence, ANOVA with post-hoc Tukey, logistic regression with pseudo-R² and fit diagnostics).
- **Knowing when to accept a null** — and explaining *why* it arises (synthetic, independently generated fields) instead of p-hacking.
- **Spotting the unit-of-analysis trap** — transactions vs. customers — and engineering RFM + loyalty-movement features the raw cross-section hides.
- **Correcting an intuitive-but-false claim** with a direct test.

---

## Repository structure

```
electronics-sales-analytics/
├── notebooks/
│   └── electronics_sales_analysis.ipynb   # full, executed analysis (renders on GitHub)
├── data/
│   ├── electronic_sales_data.xlsx          # source data (synthetic, Faker-generated)
│   └── data_dictionary.md
├── figures/                                # exported charts
├── report/
│   └── assignment_brief.pdf
├── requirements.txt
└── README.md
```

## Reproduce

```bash
pip install -r requirements.txt
jupyter notebook notebooks/electronics_sales_analysis.ipynb   # Run All
```

## Data
Adapted from *Customer Purchase Behavior – Electronic Sales Data* on Kaggle. The dataset is **synthetic** (generated with the Faker library); it contains no real personal data and is used here for methodological demonstration only.
