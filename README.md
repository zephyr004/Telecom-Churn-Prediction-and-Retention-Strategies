# Telecom Churn Prediction & Customer Retention Strategy

An end-to-end machine learning pipeline that predicts customer churn for telecom operators and translates predictions into a prioritized, actionable retention strategy.

## Problem Statement

Telecom operators in India face a **2–3% monthly churn rate**, translating to **20,000–30,000 lost customers per month** and an estimated **₹6–9 Cr in monthly revenue loss** (for a 1M-subscriber base at ₹300 ARPU). Replacing a churned customer costs **5–7x more** than retaining one, making early, targeted intervention critical.

This project builds a system that identifies which customers are likely to churn *before* they leave — and ranks them by risk and value, so retention teams know exactly who to prioritize.

## Why This Is Hard

- **Timing:** Churn decisions build up over months; by cancellation, the window to intervene has closed.
- **Visibility:** Churners look identical to loyal customers on the surface — the signal is buried in usage, complaint, and tenure patterns.
- **Prioritization:** Retention teams can't contact everyone; they need a ranked, high-value/high-risk list.

## Approach

The pipeline follows five stages:

1. **Data Collection** — Merged and validated data from 4 source systems into a single reliable dataset.
2. **Data Cleaning & Feature Engineering** — Transformed raw fields into features that capture business meaning, not just raw usage.
3. **Model Training** — Trained multiple algorithms, compared them honestly, and selected the best based on retention-relevant metrics.
4. **Prediction & Risk Scoring** — Assigned every customer a churn probability and risk tier.
5. **Business Intelligence** — Delivered a Power BI dashboard for non-technical managers to act on the results.

## Dataset

- 500 synthetic customer records, generated with churn behavior grounded in real business logic.
- **Why synthetic?** Initial testing on 10 real records produced perfect but misleading scores — the model was memorizing, not learning. Realistic, larger synthetic data proved more valuable than a small real sample for learning genuine patterns.

## Feature Engineering

Key engineered features:

| Feature | What It Captures |
|---|---|
| **ARPU** (Average Revenue Per User) | Revenue generated per month of the customer relationship — distinguishes a ₹500/month customer of 2 months from one of 36 months. |
| **Complaint Open Ratio** | Distinguishes 3 resolved complaints from 3 unresolved ones — same count, very different risk. |

ARPU emerged as the single strongest churn predictor.

## Modeling

Three classifiers were trained and honestly compared:
- Logistic Regression
- Decision Tree
- Random Forest

**Evaluation approach:**
- **5-Fold Cross-Validation** — removes luck/variance from a single train-test split.
- **GridSearchCV** — systematically tested 18 hyperparameter combinations (90 model fits total).
- **Primary metrics:** F1 score and AUC, chosen to balance precision and recall over raw accuracy.

## Results

**Top churn drivers (by feature importance):**

| Rank | Feature | Importance | Insight |
|---|---|---|---|
| 1 | ARPU | 0.694 | Low-revenue customers on basic plans churn most — less value, lower switching cost. |
| 2 | Tenure | 0.562 | First 12 months is the highest-risk window. |
| 3 | Month-to-Month Contract | 0.424 | No contractual friction to leaving; annual contracts show near-zero churn. |
| 4 | Complaints Total | 0.284 | Complaint volume correlates with churn, especially when unresolved. |

**Risk tiers:** Low (<0.4) · Medium (0.4–0.65) · High (>0.65 — immediate retention priority)

**Model performance:**
- **93% precision**
- **82% recall** (churners correctly caught)

**Business impact:** Scaled to 1M subscribers, a 20% improvement in retention from the recommended interventions is projected to save approximately **₹5 crore per month**.

## Recommendations

1. **Launch a First-Year Onboarding Program** — structured touchpoints at months 1, 3, and 6 to engage new users during the highest-risk tenure window.
2. **Target Low-ARPU Customers** — plan upgrades and data add-ons to increase customer value, addressing the top churn driver directly.
3. **Enforce a 48-Hour Complaint SLA** — faster resolution to prevent complaint-driven attrition.
4. **Incentivize Annual Contracts** — discounts/bonuses to convert month-to-month users, effectively eliminating contractual churn risk.

## Dashboard

An interactive **Power BI dashboard** lets non-technical managers filter churn risk by region and plan type, and immediately see who to call and why.

## Tech Stack

- **Python** — Pandas, Scikit-learn
- **Modeling** — Logistic Regression, Decision Tree, Random Forest, GridSearchCV
- **Visualization / BI** — Power BI

---

*This project was completed as part of the "Advanced AI/ML in Telecom Systems" training program at Nokia.*
