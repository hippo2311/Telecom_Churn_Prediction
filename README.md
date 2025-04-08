# Telco Customer Churn Prediction

This report analyzes a telecommunications dataset for **churn prediction**, focusing on exploratory data analysis, data preprocessing, and evaluation of several machine learning models. The goal is to **understand** why customers discontinue services and how to **mitigate** churn through strategic interventions.

---

## Table of Contents

1. [Project Overview](#project-overview)  
2. [Objectives](#objectives)  
3. [Data Description](#data-description)  
4. [Data Cleaning & Preprocessing](#data-cleaning--preprocessing)  
5. [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)  
6. [Model Training & Evaluation](#model-training--evaluation)  
   - [Decision Tree](#decision-tree)  
   - [Random Forest](#random-forest)  
   - [Logistic Regression](#logistic-regression)  
   - [SVM](#svm)  
7. [Key Findings & Insights](#key-findings--insights)  
8. [Recommendations](#recommendations)  
9. [Conclusion](#conclusion)  

---

## 1. Project Overview

**Customer churn** is a major concern for telecom providers. Customers frequently switch to competitors in a market with numerous service options. By identifying at-risk customers ahead of time, companies can target retention efforts more efficiently. This project demonstrates how to **explore the Telco dataset**, **visualize churn patterns**, and **build multiple machine learning models** to predict churn.

---

## 2. Objectives

1. **Quantify** the proportion of churn vs. non-churn customers.  
2. **Identify** demographic or behavioral factors that drive churn (e.g., contract type, monthly charges).  
3. **Evaluate** and **compare** different models (Decision Tree, Random Forest, Logistic Regression, SVM) based on accuracy and other classification metrics.  
4. **Provide actionable insights** to reduce churn and improve customer retention.

---

## 3. Data Description

- **Rows**: Each row represents a single telecom customer.  
- **Columns**:  
  - **Demographics**: Gender, Senior Citizen status, Partner, Dependents  
  - **Subscription Info**: InternetService, PhoneService, OnlineSecurity, etc.  
  - **Billing & Contract**: Contract type, PaymentMethod, MonthlyCharges, TotalCharges  
  - **Target**: Churn (Yes/No)  
- **Size**: ~7,043 entries initially, reduced to ~7,032 after removing invalid rows.  

Examples of key columns:

| Feature           | Description                                     |
|-------------------|-------------------------------------------------|
| gender            | Customer’s gender (Male/Female)                 |
| SeniorCitizen     | Whether the customer is a senior (1) or not (0) |
| Contract          | Contract type (Month-to-month, One year, etc.)  |
| MonthlyCharges    | Monthly billing amount                          |
| Churn             | Target variable (Yes/No)                        |

---

## 4. Data Cleaning & Preprocessing

1. **Missing Values**:  
   - 11 rows had missing `TotalCharges` with `tenure` = 0. These were **removed** because they constitute a small portion (< 0.2%) of the data.  

2. **Irrelevant Columns**:  
   - `customerID` was dropped, since it does not help with prediction.  

3. **Encoding**:  
   - Converted categorical features (e.g., `gender`, `InternetService`) into numeric codes (Label Encoding).  

4. **Train–Test Split**:  
   - Data split into **80% training** and **20% testing** to ensure an **unbiased** performance measure.

---

## 5. Exploratory Data Analysis (EDA)

### Churn Distribution
- **Churn Rate**: ~26.5% of customers left (1,869 out of 7,032), while ~73.5% stayed.

### Demographic Insights
- **Gender**: Similar churn rates; not a strong differentiator.  
- **Senior Citizens**: Though a smaller group, they exhibit a **higher churn** rate.

### Service & Contract Variables
- **Contract Type**: Month-to-month contract customers are **most likely** to churn (~75% of all churners).  
- **Payment Method**: Customers paying via **Electronic Check** have higher churn than those using automatic bank or credit card payments.  
- **Online Security & Tech Support**: Lack of these services strongly correlates with churn.

### Charges & Tenure
- **Monthly Charges**: Higher monthly bills associate with **higher churn**.  
- **Tenure**: Short-tenure (new) customers tend to churn more frequently.

---

## 6. Model Training & Evaluation

Four classification models were trained and evaluated using **accuracy**, **confusion matrix**, and **classification report**:

### Decision Tree
- **Max Depth**: 5  
- **Accuracy**: ~78.8%  
- Pros: High interpretability (easy to see how splits occur).  
- Cons: May overfit without parameter tuning; moderate recall for churn class.

### Random Forest
- **n_estimators**: 100  
- **Accuracy**: ~79.2%  
- Pros: Generally robust to overfitting; improved recall over single tree.  
- Cons: Less interpretable than a single decision tree.

### Logistic Regression
- **max_iter**: 1000  
- **Accuracy**: ~78.6%  
- Pros: Straightforward baseline, interpretable coefficients.  
- Cons: May miss complex, non-linear patterns.

### SVM (RBF Kernel)
- **Accuracy**: ~73.4%  
- Pros: Can capture more complex boundaries with the RBF kernel.  
- Cons: Performance in this dataset is lower; might improve with further hyperparameter tuning.

---

## 7. Key Findings & Insights

1. **Month-to-Month Contracts**: Strongly linked to churn due to easy cancellation.  
2. **High Monthly Charges**: Customers with bigger bills appear cost-sensitive and more inclined to leave.  
3. **Lack of Add-On Services**: Not subscribing to online security or tech support leads to higher churn rates.  
4. **Payment Method**: “Electronic check” is a common factor among those who churn.  
5. **Short Tenure**: New customers (tenure < 12 months) are more vulnerable to switching providers.

---

## 8. Recommendations

1. **Encourage Long-Term Contracts**  
   - Offer discounts or promotions for annual/biannual plans to reduce the month-to-month churn risk.

2. **Tiered Pricing / Loyalty Benefits**  
   - Address high monthly charges by introducing **loyalty bonuses** or **tiered pricing** that lowers costs over time.

3. **Service Bundles**  
   - Bundle crucial services like Online Security and Tech Support to enhance perceived value and retain subscribers.

4. **Payment Method Optimization**  
   - Incentivize customers to move from **electronic check** to **automatic** or credit card payments, which often correlate with lower churn.

5. **Target Early-Tenure Clients**  
   - Engage new customers with onboarding programs or rewards to increase satisfaction and reduce early churn.

---

## 9. Conclusion

**Telco Customer Churn Prediction** demonstrates that churn is multi-faceted, involving contract details, billing amounts, and additional services. Data-driven insights indicate that offering **longer contracts**, **valuable add-ons**, and **cost-effective strategies** can meaningfully reduce churn. While all tested models (Decision Tree, Random Forest, Logistic Regression, SVM) produced modestly similar accuracies (~78–79%), **Random Forest** slightly outperformed others.

### Future Steps
1. **Advanced Tuning**: Use GridSearchCV or RandomSearchCV for each model to maximize performance.  
2. **Ensemble Methods**: Explore XGBoost or LightGBM to potentially boost accuracy beyond ~80%.  
3. **Expanded Features**: Incorporate further customer data (support call details, demographic expansions) for richer modeling.

**Ultimately,** addressing these churn drivers with targeted retention strategies and refined data science solutions will enable telecom companies to **improve customer loyalty** and **optimize revenue**.
