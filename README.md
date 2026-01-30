# Customer Churn Prediction & Retention Intelligence

**Built on Databricks Lakehouse**

### 1. Business Problem
Customer churn is a critical challenge for subscription-based businesses, directly impacting revenue and customer lifetime value. Traditional rule-based approaches (e.g., “low usage customers will churn”) fail to capture complex interactions between customer behavior, billing patterns, and service usage.

# The goal of this project is to:
* Predict the probability of customer churn
* Segment customers by churn risk
* Translate predictions into **actionable retention strategies**

# Why AI?
* Churn drivers are multi-dimensional and non-linear
* Machine learning can learn hidden patterns that static rules cannot
* Probabilistic outputs enable prioritization and decision-making


### 2. Architecture Overview
This project is implemented using the **Databricks Lakehouse architecture** with an end-to-end AI workflow.

# High-Level Flow
CSV Source
   ↓
Bronze Layer (Raw Data)
   ↓
Silver Layer (Cleaned & Standardized)
   ↓
Gold Layer (Feature-Ready & Business Tables)
   ↓
ML Model (Churn Probability)
   ↓
Risk Segmentation & Decision Rules
   ↓
Dashboards & Insights


# Key Technologies
* Databricks (PySpark, SQL)
* Delta Lake
* MLflow
* Unity Catalog
* Databricks Jobs & Dashboards


### 3. Medallion Architecture Explanation

# Bronze Layer – Raw Ingestion
* Stores data exactly as received
* No transformations except schema inference
* Ensures data traceability and auditability
**Example Table**
 -bronze.customer_churn

# Silver Layer – Data Cleaning & Standardization
* Missing and invalid data handling
* Standardizes categorical values (e.g., “No internet service” → “Not Applicable”)
* Converts target variable (`Churn`) to numeric
**Example Table**
 -silver.customer_churn_clean
 
# Gold Layer – Business & ML Ready
* Contains engineered features and analytics-ready columns
* Serves as the single source of truth for ML, dashboards, and insights
**Example Tables**
-gold.customer_churn_features
-gold.customer_churn_predictions`

### 4. Machine Learning Approach

# Problem Type
-Binary Classification (Churn vs No Churn)
# Model Used
-Logistic Regression
# Reason for Model Choice
* Interpretable coefficients
* Lightweight and efficient
* Suitable for structured business data
* Easy to explain to non-technical stakeholders

## Feature Engineering Highlights
* tenure_bucket – customer lifecycle segmentation
* avg_monthly_charge – normalized billing behavior
* contract_type_encoded – commitment strength
* total_services_count – customer engagement score

### 5. Results & Insights

# Key Business Insights
* Month-to-month customers have the highest churn risk
* Customers with longer tenure and annual contracts churn less
* Customers with more add-on services show lower churn probability

# Risk Segmentation
| Churn Probability | Risk Segment |
| ----------------- | ------------ |
| < 0.30            | Low Risk     |
| 0.30 – 0.60       | Medium Risk  |
| > 0.60            | High Risk    |



### 6. Decision Support & Business Impact

Instead of stopping at prediction, the system generates **retention actions**:

| Risk Profile                  | Recommended Action                  |
| ----------------------------- | ----------------------------------- |
| High risk + short tenure      | Loyalty discount & contract upgrade |
| High risk + low service usage | Cross-sell add-on services          |
| Medium risk                   | Engagement email                    |
| Low risk                      | No action required                  |

# Impact
* Enables targeted retention campaigns
* Optimizes marketing spend
* Converts AI outputs into operational decisions


### 7. Dashboards & KPIs

Key KPIs visualized using Databricks SQL dashboards:

* % of High-Risk Customers
* Revenue at Risk
* Recommended Actions Distribution
* Churn Risk by Contract Type
* Top 20 High-Risk Customerss

These dashboards allow stakeholders to monitor churn risk and prioritize interventions.

## 8. Limitations

* Model is trained on historical data and may not capture sudden market changes
* Logistic Regression assumes linear relationships
* Dataset size and feature scope may limit predictive power
* No real-time streaming integration in current version

## 9. Future Improvements

* Experiment with tree-based models (Random Forest, XGBoost)
* Add SHAP or feature importance for deeper explainability
* Introduce real-time scoring using streaming data
* Automate retraining using Databricks Jobs
* Integrate outputs with CRM or marketing automation tools

## 10. Reproducibility & Governance

* All data stored as Delta tables with ACID guarantees
* Tracked using MLflow
* Unity Catalog used for access control and governance
* End-to-end workflow orchestrated using Databricks Jobs


>>>>>>>>> This project demonstrates how Databricks can be used to build an end-to-end AI-powered churn intelligence system that transforms predictions into actionable business decisions.

