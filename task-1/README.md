# Customer Churn: Data Quality & Exploratory Analysis

**Question:** Which customer groups should a (fictional) subscription team contact first to reduce avoidable churn?
**Data:** `data/customer_churn_raw.csv`: 15 synthetic customers, 11 columns (EdVyro).

## Start here
| File | What it is |
|---|---|
| `churn_data_quality_eda.html` | Rendered notebook (open in any browser) |
| `churn_data_quality_eda.ipynb` | Reproducible notebook (re-run top to bottom) |
| `data/customer_churn_clean.csv` | Clean, analysis-ready dataset (15 rows, 15 columns) |
| `data_dictionary.csv` | Every column: type, meaning, allowed values |
| `cleaning_log.csv` | Every change made and why |
| `figures/eda_overview.png` | Distribution & churn-rate charts |

## Data-quality summary
| Check | Result |
|---|---|
| Missing values | 0 in all 11 columns |
| Duplicate rows / duplicate IDs | 0 / 0 |
| Whitespace or casing inconsistencies | 0; category labels are consistent |
| Impossible values (age, tenure, charges, tickets) | 0 |
| Outliers (1.5 x IQR) | 0 flagged in any numeric column |
| `total_charges` = `monthly_charges` x `tenure_months` | Holds for all 15 rows |
| Price per plan consistent | Yes: Basic 49.99, Pro 79.99, Enterprise 149.99 |

**Result: the file was already clean, so no rows were removed or imputed.** Changes were limited to snake_case column names, a numeric `churn_flag`, and derived helper columns (`expected_total_charges`, `charge_gap`, `tenure_band`). Ten automated validation checks run in the notebook and fail loudly if any break.

**Assumptions**
- IQR outlier rules are a coarse screen at n = 15; flagged values would be judged by business logic, not auto-deleted.
- Currency assumed INR (per the EdVyro guide; the file has no unit).
- The guide's field names (`monthly_charge`, `churned`, contracts "monthly/quarterly/annual") differ from the file (`MonthlyCharges`, `Churn`, Month-to-Month/One Year/Two Year; no quarterly). I mapped them explicitly.

## Key findings (descriptive only)
- Overall churn: **7 of 15 (46.7%)**.
- **All 7 churners are Month-to-Month**; 0 of 8 One-Year/Two-Year customers churned.
- Churners: tenure 2-14 months, 3-6 tickets in 90 days, mean age 30. Retained: tenure 15-48 months, 0-2 tickets, mean age 47. No overlap on tenure or tickets.
- Plan and payment method show differences (Basic 71%, Enterprise 0%; UPI 75%, Bank Transfer 0%) but overlap heavily with contract type, so they are not independent drivers.
- Churned customers represent ~32% of monthly charges (INR 409.93 of 1,269.85).

## Recommendation
- **Audience:** Month-to-Month customers with 3+ tickets in the last 90 days and under ~15 months of tenure.
- **Decision:** Prioritise them for retention outreach (support follow-up, annual-plan offer).
- **Supporting metric:** 7/7 churn in this segment vs 0/8 outside it.
- **Uncertainty:** n = 15 and the segment overlaps almost perfectly with Month-to-Month; real-world rates will be lower. Correlation is not causation: high ticket counts may be a symptom, not a cause. Timing of tickets vs. churn is unknown.
- **Next measurement:** on a larger real sample, track 90-day churn for Month-to-Month customers by ticket count and tenure band, with a no-outreach holdout group to test whether contact actually reduces churn.

## Reproduce
`pip install pandas matplotlib jupyter` → run `churn_data_quality_eda.ipynb` from this folder.
