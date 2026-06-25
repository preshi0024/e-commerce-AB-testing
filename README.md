# A/B Testing Analysis: E-Commerce Conversion Optimization

## Overview

This project analyzes a multi-table synthetic e-commerce dataset to evaluate whether two experimental variants (Variant_A and Variant_B) significantly improved purchase conversion rates compared to a Control group. The analysis covers over 2 million user sessions across 100,000 customers.

## Business Question

Does exposure to Variant_A or Variant_B significantly increase purchase conversion rate compared to Control — and is the effect consistent across customer segments?

## Dataset

**Source:** [Marketing & E-Commerce Analytics Dataset](https://www.kaggle.com/datasets/geethsagarb/marketing-e-commerce-analytics-dataset) by GeethaSagarBonthu on Kaggle (synthetic, CC0 Public Domain)

Five linked tables:
| File | Description |
|---|---|
| `campaigns.csv` | Campaign objective, duration, target segment, expected uplift |
| `customers.csv` | Demographics, signup date, loyalty tier, acquisition channel |
| `events.csv` | 1.9M+ session-level events (view, click, add_to_cart, purchase, bounce) with experiment group assignment |
| `products.csv` | Product catalog |
| `transactions.csv` | Purchase transactions with revenue and refund flags |

> **Note:** Dataset files are not included in this repo. Download from the Kaggle link above and place CSVs in the same directory as the notebook before running.

## Methodology

1. **Data Loading & EDA** — Loaded five CSV files, checked shapes, nulls, and column structures
2. **Conversion Definition** — Conversion = reaching a `purchase` event within a session
3. **Statistical Testing** — Two-proportion Z-tests (Control vs. Variant_A, Control vs. Variant_B) using `statsmodels`
4. **Confidence Intervals** — Wilson method for per-group rates; Wald method for the difference between groups
5. **Segment Validation** — Conversion rate breakdown by loyalty tier and device type to confirm effect consistency
6. **Funnel Analysis** — view → add_to_cart → purchase drop-off comparison across groups
7. **Data Limitation Noted** — 99,963 of 100,000 customers appeared in multiple experiment groups, indicating session-level (not customer-level) randomization; documented as a data quality observation

## Key Results

| Group | Conversion Rate | 95% CI |
|---|---|---|
| Control | 4.74% | 4.71% – 4.78% |
| Variant_A | 5.24% | 5.17% – 5.31% |
| Variant_B | 6.30% | 6.23% – 6.38% |

- **Variant_B drove a statistically significant 32.9% relative lift** over Control (Z = 38.71, p < 0.001)
- The 95% CI on the difference [1.48%, 1.64%] excludes zero — the effect is real and precisely estimated
- Variant_A also significantly outperformed Control (Z = 12.70, p < 0.001), with a smaller effect size
- At Control's traffic scale, rolling out Variant_B projects ~**18,700 additional conversions**
- Segment analysis confirmed the Variant_B lift was **consistent across all loyalty tiers and device types**

## Visualizations

- Conversion rate bar chart with 95% confidence intervals
- Loyalty tier × experiment group heatmap
- Conversion funnel line chart (view → add_to_cart → purchase)
- Device type segment breakdown

## Tech Stack

`Python` · `pandas` · `numpy` · `scipy` · `statsmodels` · `matplotlib` · `seaborn` · `Jupyter Notebook`

## Author

**Preshika Shanmugavel**  
MS Information Technology & Management (Data Science & Applied AI) — Illinois Institute of Technology  
[Portfolio](https://preshi0024.github.io) · [LinkedIn](https://www.linkedin.com/in/preshikashanmugavel)
