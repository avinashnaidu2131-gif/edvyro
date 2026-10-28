# Customer Churn KPI Dashboard

Interactive dashboard for the 15-customer synthetic churn dataset (cleaned and validated in Task 1).

**Open it:** open `index.html` in any browser. It is one self-contained file with no external libraries. If hosted with GitHub Pages (Settings → Pages → deploy from `main`), it becomes a live link.

## KPIs
- **Churn rate** = churned ÷ customers in the filter
- **Retention rate** = 1 − churn rate
- **Monthly revenue at risk** = sum of monthly charges of churned customers (also shown as % of all monthly charges)
- **Tenure** = average months, for all / churned / retained customers

## Filters
Contract type, tenure band (0–6, 7–12, 13–24, 25+ months), payment method. Every KPI, chart and written insight updates with them.

## Charts (each has a written insight beside it)
Churn rate by contract · churn rate by payment method · customers by tenure band · support tickets · monthly revenue at risk by plan

## Accessibility
Colour-blind-safe blue/orange palette (Okabe–Ito); churned bars also carry a hatch pattern and every bar has a text label, so meaning never relies on colour alone. Keyboard-focusable filters, ARIA labels, light and dark mode.

## Caveats
Only 15 customers, so one person moves a rate by about 7 points. Findings are descriptive, not causal. Contract, tenure and tickets overlap heavily. Currency assumed INR.

Data: `data/customer_churn_clean.csv`
