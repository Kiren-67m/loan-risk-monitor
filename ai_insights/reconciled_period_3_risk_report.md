# Loan portfolio risk brief

**Payment period 3 · Representative due-date month March 2023 · AITCC competition data**

Period 3 showed the weakest payment performance among the first five observed periods. The average cumulative on-time rate fell from **95.04% to 94.51%**. Among loans with comparable payment histories, **15,579 of 163,405 (9.53%)** had a drop of more than 10 percentage points in their own cumulative on-time rate, up from **12,071 of 171,022 (7.06%)** in period 2.

| Metric | Period 2 | Period 3 |
| --- | ---: | ---: |
| Loans with a payment record | 179,739 | 167,587 |
| Loans with known current payment status | 175,309 | 163,506 |
| Average cumulative on-time rate | 95.04% | 94.51% |
| Loans ever recorded delinquent through the period | 15,583 of 179,619 (8.68%) | 20,303 of 167,584 (12.12%) |
| Loans with a deteriorating on-time rate | 12,071 of 171,022 (7.06%) | 15,579 of 163,405 (9.53%) |

Credit lines and home equity loans accounted for **17,326 of 20,303** loans with recorded delinquency through period 3. Their rates were similar at **12.12%** and **12.13%**, respectively. Those two segments are a practical starting point for reviewing the increase by volume. Check the **4,081** period 3 payment records with unknown current status separately before interpreting current payment performance.

The observed population fell by **12,152** loans between periods 2 and 3. Each row compares the population observed in that period. A matched cohort would be needed to measure how the same loans changed. The average on-time rate is the mean of each eligible loan’s cumulative rate. Each loan contributes one observation per period. The denominator for deterioration requires a known current status and a comparable preceding-period rate.

The period 3 source count of **167,587** matches the corrected portfolio and both segment totals. The earlier unchecked joins produced **170,919** rows for that period. The figures above come from Phase 0, using the original competition CSVs and aggregate outputs only.

[Monthly KPI rows](../portfolio_monthly_kpi.csv) · [Loan-type breakdown](../portfolio_monthly_kpi_by_segment.csv) · [Join reconciliation](../portfolio_kpi_reconciliation.csv) · [Calculation notebook](../Copilot_Phase0.ipynb)
