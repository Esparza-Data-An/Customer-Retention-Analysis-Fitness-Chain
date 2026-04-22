# Customer Churn Prediction & Segmentation — Model Fitness

## Overview
Model Fitness, a gym chain, seeks to reduce customer churn by understanding 
which clients are likely to leave and why. This project builds a churn 
prediction model and segments customers into behavioral profiles to support 
data-driven retention strategies.

## Note on Language
The Jupyter notebook and internal comments are currently in Spanish.
An English version is in progress.

## Objectives
- Predict the probability of churn for each customer in the following month.
- Identify the most influential features driving cancellations.
- Segment customers into clusters and describe their key characteristics.
- Deliver actionable, cluster-specific retention recommendations.

## Dataset
Provided by TripleTen. Contains anonymized customer data from a gym chain,
including demographic information, contract details, visit frequency, and 
additional service consumption. Target variable: `Churn` (1 = left, 0 = stayed).

**Key features:** `Lifetime`, `Contract_period`, `Month_to_end_contract`,
`Avg_class_frequency_current_month`, `Near_Location`, `Group_visits`,
`Avg_additional_charges_total`

## Tools & Libraries
Python · Pandas · Scikit-learn · SciPy · Seaborn · Matplotlib

## Methodology

### 1. Exploratory Data Analysis (EDA)
- No missing values or duplicates found.
- Compared mean feature values between churned and retained customers.
- Identified multicollinearity: `Contract_period` / `Month_to_end_contract` 
  (r ≈ 0.97) and `Avg_class_frequency` variables (r ≈ 0.95).
- Strongest negative correlations with churn: `Lifetime` (-0.44), 
  `Avg_class_frequency_current_month` (-0.41), `Age` (-0.40).

### 2. Churn Prediction Models
Trained and compared two binary classification models:

| Model | Accuracy | Precision | Recall |
|---|---|---|---|
| Logistic Regression | 92% | 86% | 83% |
| Random Forest | 92% | Slightly lower | Slightly lower |

Logistic Regression selected as the preferred model based on superior 
precision and recall for identifying at-risk customers.

### 3. Customer Segmentation (K-Means, n=5)
- Data standardized prior to clustering.
- Dendrogram used to estimate optimal cluster count.
- Two high-risk clusters identified (churn rates ~44–51%):
  - **Cluster 2:** No customers live near a facility; low class frequency 
    and low community engagement.
  - **Cluster 3:** Youngest group, shortest tenure, lowest class attendance 
    and additional spending.
- Low-risk clusters (churn < 7%): characterized by high class frequency, 
  longer contracts, and stronger social engagement.

## Key Findings
- Customers who churn tend to be younger, have short contracts, low class 
  attendance, and weak social ties to the gym community.
- Geographic distance from facilities is a critical churn factor independent 
  of contract length.
- Customers without a registered phone number show intermediate churn risk.

## Retention Recommendations
- **Cluster 2:** Promote group classes and referral programs; explore 
  distance-based discounts to incentivize attendance.
- **Cluster 3:** Incentivize longer contracts from sign-up; offer discounts 
  on additional services to increase engagement.
- **Cluster 1:** Collect missing contact information; encourage higher class 
  frequency through targeted communication.
- **Acquisition:** Segment new customer promotions by geographic proximity 
  to facilities.

## Project Structure
```
├── datasets/
│   └── gym_churn_us.csv     # Dataset
├── notebook.ipynb       # Full analysis and modeling
└── README.md
