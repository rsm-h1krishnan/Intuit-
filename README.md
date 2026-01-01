# Intuit QuickBooks Upgrade Targeting (Wave-2) — Predictive Modeling Case Study

This repo contains the final **project report only** (no code/data) due to school/confidentiality constraints.

## Overview
Intuit ran a direct-mail upgrade campaign to move small businesses to **QuickBooks v3.0**.  
Wave-1 went to a large customer list; Wave-2 should target **only the most likely responders** among customers who **did not respond in Wave-1**, with the goal of maximizing profit.

**Goal:** Predict upgrade likelihood and produce a Wave-2 targeting strategy that balances response probability vs. mailing cost.

## Business Context (What we’re optimizing)
- **Mailing cost:** $1.41 per customer
- **Margin per upgrade (excluding mailing cost):** $60
- **Wave-2 expected response drop:** assume Wave-2 response probability is **50% of predicted Wave-1 probability** (standard practice in the case)

We used a breakeven framework to decide who should be mailed in Wave-2.

## Data (high level)
The dataset represents small business customers who received the Wave-1 mailing, including:
- Customer/order history (e.g., number of orders, total spend, recency)
- Product ownership & upgrade history
- ZIP bin features
- Binary response label for Wave-1

> Note: The dataset is course-provided and not included here.

## Modeling Approach
### 1) Logistic Regression (baseline + feature selection)
We started with a full model and iteratively removed non-contributing variables. We also used:
- **LASSO** to validate feature importance
- **Permutation importance**
- **Correlation checks** to address multicollinearity

Final core predictors used:
- `zip_bins`, `numords`, `dollars`, `last`, `upgraded`, `owntaxprod`, `version1`

### 2) Neural Network (to capture non-linear patterns)
We tested multiple single hidden-layer configurations. Early experiments showed either no lift or overfitting.
Switching to:
- **Adam solver + ReLU activation**
and tuning hidden layer size led to a stable model. The best configuration used a hidden layer size of **(10,)**.

### 3) “Best of both” — discovering interactions
We used the neural network to surface interactions not captured by the base logistic model, then added these into logistic regression:
- `version1:last`
- `numords:version1`

After adding these terms, logistic regression performance became very close to the neural model, with the added benefit of interpretability.

## Targeting Rule (Profit-based)
We mailed customers when the adjusted probability exceeded the breakeven threshold.

Breakeven probability:
\[
p_{breakeven} = \frac{1.41}{60} \approx 0.0235
\]

Wave-2 adjustment:
- `p_wave2 = 0.5 × p_predicted`

Mail in Wave-2 if:
- `p_wave2 > p_breakeven`



### Final decision
We chose the **logistic regression model** for deployment because it delivered **higher total profit** and remained highly competitive after adding interaction terms—while staying simpler and more interpretable.

## What we learned
- Past purchase behavior and recency strongly relate to upgrade likelihood.
- Neural networks helped uncover interaction effects that improved a traditional model.
- Profit-based targeting (breakeven threshold + response drop adjustment) is essential for realistic campaign decisions.

## Contents of this repo
- `report/` — Final project report (PDF)

## Notes on confidentiality
- Code, data, and any course-only resources are intentionally excluded.
- This repo is meant to showcase the **business framing, modeling approach, and results**.




## License
For educational/portfolio use only. Please do not reuse course-provided materials in ways that violate your institution’s academic policies.
