# 🏦 Loan Eligibility Prediction

Practice problem from **Analytics Vidhya** —
[Loan Prediction](https://www.analyticsvidhya.com/datahack/contest/practice-problem-loan-prediction-iii/).

Predict whether a home-loan application gets approved (`Loan_Status` = Y/N) from
applicant details, for Dream Housing Finance.

**Binary classification** · Fintech · Metric: **Accuracy** (target imbalanced ~69/31).
Train: 614 rows · Test: 367 rows.

---

## 🔍 EDA Findings

**Categorical** (approval-rate gap vs target):
- **Credit_History** — good 80% vs bad 8% → *dominant predictor*
- **Property_Area** — Semiurban +11–15% over Urban/Rural → strong, cause unexplained by this data
- Education (+10%), Married (+9%) → mild · Gender (+3%) → weak
- Self_Employed → no signal (both groups at the ~69% base rate)

**Numeric** (median, approved vs rejected):
- **CoapplicantIncome** 1239 vs 268 → real signal (a second earner helps)
- ApplicantIncome 3812 vs 3833, LoanAmount 126 vs 129 → weak / none alone

> Insight: raw income is weak, but an **income-to-loan ratio** may carry signal.

> Imbalanced target → accuracy alone misleads; "approve everyone" already scores ~69%.

---

## ⚙️ Setup

```bash
uv sync
```

> Data isn't included — download `train.csv` / `test.csv` from the Analytics
> Vidhya link above into `data/`.

`profiling.ipynb` — inspection & data audit · `eda.ipynb` — exploratory analysis.
