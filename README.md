# SBA-Loan-Default-Prediction
The **2024 CSU Systemwide Business Analytics Competition** focuses on leveraging the SBA National Dataset, originally published by Li, Mickel, and Taylor (2018). This dataset provides historical data from the U.S. Small Business Administration (SBA) to analyze and predict the probability of loan default.
Participants are tasked with building Predictive models to classify whether a loan will be paid in full (P I F) or charged off (CHGOFF). 

<p align="center">
  <img src="https://github.com/sindhu28ss/SBA-Loan-Default-Prediction/blob/main/Images/Picture1.png" width="500">
</p>

The problem also incorporates real-world constraints such as:
- **Imbalanced Classes:** A higher proportion of loans are classified as “P I F” compared to CHGOFF.
- **Cost-Sensitive Decisions:** Misclassifying a high-risk loan as low-risk incurs a much greater cost than the benefit of correctly identifying a low-risk loan.

## Problem
- **Loan Defaults:** Difficulty in predicting loan defaults that impacts profitability.
- **Threshold Challenge:** Finding the right cut-off for loan approavals by the bank to balance risk and profit.

## Solution
**1.	Classify Loan Applications:** as higher risk (CHGOFF) or lower risk (P I F).

**2.	Incorporate Cost Sensitivity:** Account for the significant financial cost of misclassifying high-risk loans.

**3.	Optimize Profitability:** Use the provided cost matrix to determine the optimal threshold for loan approvals to maximize net profits.

**4.	Provide Business Insights:** Help banks make data-driven decisions on loan approvals.

## Data Overview
- The SBA National Dataset - https://drive.google.com/file/d/1LGKdxoDwP_jypAnB_o7HKJheoXpTS9qv/view comprises 899,164 rows and 27 columns.
- Target Variable (MIS_Status): Indicates whether a loan was Paid in Full (P I F) or Charged Off (CHGOFF).
- Predictor Variables: A mix of numerical and categorical features, including loan terms, business characteristics, and loan performance metrics.

## Methodology
Several predictive models were employed to classify SBA loan applications as "higher risk" or "lower risk" for loan approval. 

### Modeling Techniques Used:
- **k-Nearest Neighbors (kNN)**: A non-parametric method used for both classification and regression.
- **Classification Trees and Ensemble Methods**: This includes single decision trees, bagging, boosting, and random forests to improve prediction accuracy.
- **Logistic Regression Models**: Utilizing regularization methods such as Lasso, Ridge, and ElasticNet to prevent overfitting and enhance model generalization.
- **Neural Networks**: Employed to capture complex nonlinear relationships within the data.
- **Discriminant Analysis**: A statistical technique to predict a categorical dependent variable by analyzing linear combinations of predictor variables.

### Cost Matrix:
The net profit impact based on actual loan outcomes compared to predictions made by the models is illustrated in the table below:

| Actual  | Predicted         | Net Profit                           |
|---------|-------------------|--------------------------------------|
| P I F   | P I F (grant loan)| 5% of DisbursementGross             |
| CHGOFF  | P I F (grant loan)| -5 * 5% of DisbursementGross (loss) |
| P I F   | Default (deny loan)| $0 (no profit/loss)                 |
| CHGOFF  | Default (deny loan)| $0 (no profit/loss)                 |

**Threshold Determination:** The optimal threshold was selected by maximizing the F1-Score using the Precision-Recall Curve.

### Model Performance Evaluation:

The evaluation of the predictive models was based on several key metrics: Accuracy, Specificity, Sensitivity, F1-Score, ROC-AUC, and Total Net Profit. Here's how each model performed:

| Model                   | Threshold | Accuracy | Specificity | Sensitivity | F1-Score | ROC-AUC | Total Net Profit ($)  |
|-------------------------|-----------|----------|-------------|-------------|----------|---------|-----------------------|
| KNN                     | 0.4       | 0.9916   | 0.9932      | 0.9838      | 0.9761   | 0.9914  | 1,586,088,755.55      |
| **Random Forest**       | **0.4704**| **0.9937**| **0.9933**  | **0.9955**  | **0.9823**| **0.998** | **1,589,844,341.60** |
| Base Logistic Regression| 0.3708   | 0.9922   | 0.9935      | 0.9863      | 0.9781   | 0.995   | 1,579,861,133.90      |
| Neural Networks (Base)  | 0.1802   | 0.9933   | 0.9934      | 0.9929      | 0.9812   | 0.9979  | 1,586,310,134.45      |
| Discriminant Analysis   | 0.2404   | 0.9806   | 0.9893      | 0.9398      | 0.9444   | 0.9821  | 1,558,540,857.85      |

### Best Performing Model:
The **Random Forest model** emerged as the best performer across all considered metrics
- **Profit**: Generates the highest net profit at approximately **$1.59 billion**.
- **Sensitivity**: Exceptional at identifying true positives with a sensitivity of **0.9955**.
- **Accuracy**: Maintains a high accuracy rate of **0.9937**, ensuring reliable predictions.

## Profit Optimization by Random Forest Model

The Random Forest model was strategically used to prioritize loan applications, ranking them from least risky to most risky based on the estimated probabilities. This approach was pivotal in maximizing financial outcomes.

<p align="left">
  <img src="https://github.com/sindhu28ss/SBA-Loan-Default-Prediction/blob/main/Images/final-gains%20chart.png" width="270">
  <img src="https://github.com/sindhu28ss/SBA-Loan-Default-Prediction/blob/main/Images/final-lift%20chart.png" width="300">
</p>

### Key Results:
- **Maximum Net Profit Achieved**: $1.59 billion was realized by approving 147,072 loans.
- **Optimal Probability Threshold**: A cut-off of 0.3804 was identified as ideal for future loan approvals. This threshold was selected based on its capacity to maximize net profit while balancing the risk of default.

## Final Recommendations

- **Approve Loans Strategically**: Prioritize approvals by starting with the least risky applicants, based on predicted probabilities from the **Random Forest** model.
- **Maximize Profitability**: Limit approvals to the first **147,072** loans to optimize profit margins.
- **Set Optimal Threshold**: Use a probability threshold of **0.3804** for future loan approvals to balance risk and maximize returns.



