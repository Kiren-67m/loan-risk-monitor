# Loan Portfolio Risk Monitor

> **AITCC 2026 Banking Analytics Challenge — 2nd Place**  
> Competition work extended into a portfolio monitoring prototype.

**[Live Portfolio Site](https://Kiren-67m.github.io/loan-risk-monitor)** · [LinkedIn](https://www.linkedin.com/in/qiming-liu-845ba92a0/)

---

## What This Is

This project started as a timed competition entry at **AITCC 2026** (America's Innovate IT Collegiate Conference) — predict loan defaults from messy, multi-table banking data under time pressure. We placed **2nd in the Analyze IT Challenge**.

Post-competition, I extended it into a **portfolio monitoring prototype** connecting prediction outputs, monthly KPI snapshots, risk segmentation and AI-generated reports.

---

## Core Analytical Insight

Payment behavior features engineered from raw monthly records show stronger associations with default in this competition dataset than the credit metrics below:

| Feature | Correlation with Default |
|---|---|
| On-Time Rate | **r = -0.76** |
| Cumulative Delinquent Days | **r = +0.70** |
| Credit Score | r = 0.001 |
| Annual Income | r = -0.005 |

> *"A borrower's credit profile tells you who they are on paper. Their payment behavior tells you what they actually do."*

---

## System Architecture

```
Raw Data (3 tables)
    ↓
Feature Engineering          Loan.ipynb
    ↓
Dual-Target Modeling         AUC 0.9629 · R² 0.7867 · F1 0.9089
    ↓
Monthly KPI Snapshots        Copilot_Phase0.ipynb
    ↓
Risk Segmentation            Copilot_Phase2.ipynb
    ↓
Tableau Dashboard            Interactive portfolio monitor
    ↓
AI Risk Reports              Copilot_Phase3.ipynb → Claude API
    ↓
Portfolio Website            index.html
```

---

## Repository Structure

```
├── Loan.ipynb                            # Competition notebook: EDA → modeling
├── Copilot_Phase0.ipynb                  # Monthly KPI snapshot pipeline
├── Copilot_Phase2.ipynb                  # Risk segmentation & early warning
├── Copilot_Phase3.ipynb                  # Claude API report generator
├── index.html                            # Portfolio website (single-page)
│
├── submission.csv                        # Competition predictions
├── sample_starter.py                     # Original competition starter code
├── benchmark.txt                         # Competition evaluation metrics
│
├── portfolio_monthly_kpi.csv             # 7 rows: monthly portfolio KPIs
├── portfolio_monthly_kpi_by_segment.csv  # Segment breakdown by loan type & state
├── risk_profile.csv                      # 4 rows: per risk-band summary
├── priority_loans.csv                    # Top-50 intervention priority loans
│
├── ai_insights/                          # Claude-generated monthly risk reports
│   ├── month_1_2023-01_risk_report.txt
│   ├── month_2_2023-02_risk_report.txt
│   ├── month_3_2023-03_risk_report.txt  ← Peak risk month
│   ├── month_4_2023-04_risk_report.txt
│   └── month_5_2023-05_risk_report.txt
│
└── eda_outputs/                          # EDA charts and figures
```

> Original competition inputs are not bundled. Full modeling requires `borrowers.csv`, `loans.csv`, `payment_history.csv`, `train.csv`, `eval.csv` and `answer_key.csv` in the repository root. The committed outputs and notebook results can be inspected without these files.

---

## Model Performance

| Model | Val AUC | Val RMSE | Val R² |
|---|---|---|---|
| Logistic + Linear (baseline) | **0.9650** | 116.4 | 0.6163 |
| Random Forest | 0.9633 | **87.6** | **0.7825** |

**Final evaluation:** AUC 0.9629 · R² 0.7867 · F1 0.9089

---

## Risk Segmentation Results

| Band | Loans | % Portfolio | Avg Proba | On-Time Rate |
|---|---|---|---|---|
| Low | 146,879 | 80.0% | 0.026 | 1.000 |
| Medium | 8,438 | 4.6% | 0.150 | 1.000 |
| High | 694 | 0.4% | 0.395 | 1.000 |
| **Critical** | **27,585** | **15.0%** | **0.998** | **0.519** |

The exploratory scoring output is concentrated in the Low and Critical bands. Because these scores include training rows, this pattern should not be interpreted as evidence of reliable separation on new loans.

---

## Key Finding: Month 2 Cliff

```
Month 1:  3,229 loans first went delinquent  (baseline)
Month 2: 12,454 loans first went delinquent  ← largest single-month jump (46%)
Month 3:  9,202 loans first went delinquent  (peak cumulative risk)
```

Month 2 has the largest count of first delinquency events in this retrospective summary. This is a candidate period for investigation; establishing an actionable early-warning window requires features available before delinquency and time-based validation.

---

## Running the Notebooks

```bash
pip install -r requirements.txt
jupyter lab
```

**Execution order:**
1. `Loan.ipynb` — competition modeling pipeline (requires raw data CSVs)
2. `Copilot_Phase0.ipynb` — generates monthly KPI CSVs
3. `Copilot_Phase2.ipynb` — generates risk profile and priority loans
4. `Copilot_Phase3.ipynb` — requires an `ANTHROPIC_API_KEY` environment variable and makes external API calls

**API key:** Set `ANTHROPIC_API_KEY` in your local environment before launching Jupyter. Do not write a real key into a notebook. Phase 3 sends analytical context to the Anthropic API and incurs usage charges; it is optional. The existing reports can be read without an API call.

---

## Scope and evaluation limits

- The performance figures above are recorded competition results from `Loan.ipynb`; they have not been reproduced from a fresh checkout here because the raw competition inputs are absent. `benchmark.txt` is the supplied challenge baseline, not the final model's score.
- Feature engineering aggregates supplied payment history, and model selection uses a random validation split. This does not establish point-in-time forecasting performance or remove the need to check temporal leakage and preprocessing leakage before operational use.
- Phase 2 fits a separate random forest and scores the full portfolio, including training rows. Its risk bands and watchlists are exploratory outputs, not held-out model evaluation.
- Monthly reports use generated analytical context and require human review. A production early-warning claim would need as-of feature cutoffs, time-based validation, calibration and monitoring.

## Tech Stack

Python · pandas · scikit-learn · statsmodels · XGBoost · matplotlib · Anthropic Claude API · Tableau · Jupyter Notebook

---

**Qiming Liu** · [LinkedIn](https://www.linkedin.com/in/qiming-liu-845ba92a0/)  
Built as a portfolio project from AITCC 2026 Banking Analytics Challenge · **2nd Place**
