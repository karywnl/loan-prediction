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

| Feature | Effect on approval | Strength |
|---|---|---|
| Credit_History | good 80% vs bad 8% | 🟢 Dominant |
| Property_Area | Semiurban +11–15% over Urban/Rural (cause unexplained by this data) | 🟢 Strong |
| Education | Graduate +10% | 🟡 Mild |
| Married | Married +9% | 🟡 Mild |
| Gender | Male +3% | 🔴 Weak |
| Self_Employed | both groups ≈ 69% base rate | ⚫ None |
| Dependents | 0/1/2/3+ all ≈ base rate, non-monotonic | ⚫ None |
| Loan_Amount_Term | 83% are 360; off-360 rates are tiny-sample noise | ⚫ None (low variance) |

**Numeric** (median, approved Y vs rejected N):

| Feature | Approved (Y) | Rejected (N) | Strength |
|---|---|---|---|
| CoapplicantIncome | 1239 | 268 | 🟢 Real signal (second earner helps) |
| ApplicantIncome | 3812 | 3833 | ⚫ None alone |
| LoanAmount | 126 | 129 | 🔴 Weak |

**Engineered features** (tested in `preprocessing.ipynb`):

| Feature | Definition | Verdict |
|---|---|---|
| income_to_loan_ratio | (ApplicantIncome + CoapplicantIncome) / LoanAmount | ⚫ Dead — flat & non-monotonic across quartiles; Credit_History swamps affordability |

> Imbalanced target → accuracy alone misleads; "approve everyone" already scores ~69%.

---

## ⚙️ Setup

```bash
uv sync
```

> Data isn't included — download `train.csv` / `test.csv` from the Analytics
> Vidhya link above into `data/`.

`profiling.ipynb` — inspection & data audit · `eda.ipynb` — exploratory analysis ·
`preprocessing.ipynb` — train/validation split, imputation & feature engineering.
