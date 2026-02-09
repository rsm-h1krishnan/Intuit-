# Intuit QuickBooks Upgrade Targeting (Wave-2) — Predictive Modeling Case Study

# **Project Overview**

This case study focuses on optimizing a direct-mail marketing campaign for **Intuit QuickBooks**. After an initial Wave-1 mailing to over 800,000 small businesses, the goal was to develop a sophisticated targeting strategy for **Wave-2**. The objective was to identify which non-responders from the first wave were most likely to upgrade to QuickBooks Version 3.0, maximizing total campaign profit while accounting for a projected 50% drop in response rates for the second wave.

***Business Logic & Strategy***

To ensure the campaign was data-driven and ROI-focused, I utilized a **breakeven probability framework**:

• **Cost Dynamics:** Each mail piece cost **$1.41**, with a net revenue of **$60** per successful upgrade.

• **Breakeven Threshold:** Targeting was only performed if a customer's predicted probability of responding exceeded **0.0235** ($P_{breakeven} = 1.41 / 60$).

• **Wave-2 Adjustment:** Applied a conservative 50% "drop-off" multiplier to Wave-1 predicted probabilities to reflect realistic second-wave behavior.

***Analytical Methodology***

I developed and compared two primary modeling architectures to find the optimal balance between predictive power and business interpretability:

• **Logistic Regression (Baseline & Refinement):** Started with a comprehensive feature set and used **LASSO regression** and **Permutation Importance** to isolate the most impactful predictors, such as purchase recency (`last`), version history (`version1`), and past order volume (`numords`).

• **Neural Networks (Pattern Discovery):** Employed a Neural Network with an **Adam solver** and **ReLU activation** (10 nodes in a single hidden layer) to capture complex, non-linear relationships.

• **Feature Engineering & Interaction:** Used the Neural Network to "discover" hidden interactions—specifically between software version and purchase recency (`version1:last`) and order frequency (`numords:version1`). These were then integrated back into the Logistic Regression model to enhance its performance.

***Key Results & Impact***

• **Optimal Model:** Selected the **Interaction-Adjusted Logistic Regression** for final deployment due to its superior total profit and high interpretability.

• **Profitability:** The model successfully identified a high-value segment, leading to an estimated **$550,094 in total profit**.

• **Efficiency:** Achieved a **192.33% Return on Marketing Expenditure (ROME)**, ensuring that marketing spend was concentrated only on the most promising leads.

***Technical Skills Demonstrated***

• **Predictive Modeling:** Logistic Regression, Neural Networks (MLP), LASSO Regularization.
• **Model Evaluation:** Gains/Lift Charts, AUC, ROME, and Profit-based Thresholding.
• **Tools:** Python (pandas, sklearn, statsmodels, pyrsm).

This repo contains the final **project report only** (no code/data) due to school/confidentiality constraints.

