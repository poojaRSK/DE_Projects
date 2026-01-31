# AI-Driven Customer Churn Prediction & Decision Support System

## 1. Business Problem

Customer churn is a critical challenge for subscription-based businesses, directly impacting revenue and customer lifetime value. Traditional rule-based approaches detect churn too late, fail to capture complex customer behavior, and provide no actionable guidance on how to retain customers.

This project addresses that gap by building an **end-to-end, AI-driven churn prediction and decision-support system** that not only identifies customers at risk of churning but also explains *why* they are at risk and *what actions* the business should take.

---

## 2. Objective

The primary objectives of this project are to:

* Predict customer churn probability
* Segment customers into risk categories (Low / Medium / High)
* Generate actionable retention strategies
* Enable proactive, data-driven decision-making

The solution shifts churn management from **reactive reporting** to **proactive intervention**.

---

## 3. Architecture Overview

The solution is implemented on the **Databricks Lakehouse Platform** using the **Medallion Architecture**.

### High-Level Flow

CSV Source → Bronze → Silver → Gold → ML Model → Risk Segmentation → Retention Actions → Dashboards

### Key Technologies

* Databricks (PySpark, SQL)
* Delta Lake
* MLflow
* Unity Catalog
* Databricks Jobs & Dashboards

---

## 4. Data Architecture (Medallion Design)

### 4.1 Bronze Layer – Raw Ingestion

**Purpose:** Preserve raw data exactly as received.

* No transformations applied
* Schema inference only
* Ensures auditability and reprocessing

**Example Table:** `bronze.customer_churn`

### 4.2 Silver Layer – Cleaned & Standardized

**Purpose:** Improve data quality and consistency.

* Handle missing values and duplicates
* Standardize categorical values
* Convert churn label to numeric

**Example Table:** `silver.customer_churn_clean`

### 4.3 Gold Layer – Feature-Ready & Analytics

**Purpose:** Business-ready and ML-ready data.

* Engineered features
* Model predictions
* Risk segmentation
* Retention recommendations

**Example Tables:**

* `gold.customer_churn_features`
* `gold.customer_churn_predictions`

---

## 5. Feature Engineering

Instead of using raw columns, business-driven features were engineered to improve interpretability and model performance.

### Key Features

* **tenure_bucket:** Customer lifecycle segmentation
* **avg_monthly_charge:** Normalized billing behavior
* **contract_type_encoded:** Commitment strength
* **total_services_count:** Customer engagement / stickiness score

These features align ML outputs with real business understanding and actions.

---

## 6. Machine Learning Approach

### Problem Type

Binary Classification (Churn vs No Churn)

### Model Used

**Logistic Regression (Spark ML)**

### Why Logistic Regression?

* Interpretable coefficients
* Lightweight and scalable
* Suitable for structured data
* Easy to explain to business stakeholders

### Limitations

* Assumes linear relationships
* Cannot capture deep non-linear patterns

---

## 7. Training, Evaluation & Governance

### Training Setup

* Train/Test Split: 80/20

### Evaluation Metrics

* ROC-AUC (Primary)
* Precision & Recall
* Confusion Matrix

**Example Result:** ROC-AUC = 0.82

### MLflow Integration

MLflow is used to track:

* Model parameters
* Evaluation metrics
* Feature list
* Trained model artifacts

This ensures reproducibility, experiment comparison, and enterprise-grade governance.

---

## 8. AI Innovation: From Prediction to Decision Support

### Step 1: Churn Probability

The model outputs a churn probability between 0 and 1, representing the likelihood of churn for each customer.

### Step 2: Risk Segmentation

Probabilities are converted into business-friendly segments:

* < 0.30 → Low Risk
* 0.30–0.60 → Medium Risk
* > 0.60 → High Risk

### Step 3: Retention Action Generation

Risk segments are enriched with customer context (tenure, contract, service usage) to generate concrete actions:

* High Risk + short tenure → Loyalty discount & contract upgrade
* High Risk + low services → Cross-sell add-ons
* Medium Risk → Engagement email
* Low Risk → No action required

This transforms the model into a **decision-support system**, not just a prediction engine.

---

## 9. Final Decision-Ready Output

| customer_id | churn_prob | risk_segment | recommended_action       |
| ----------- | ---------- | ------------ | ------------------------ |
| 4582        | 0.78       | High Risk    | Offer loyalty discount   |
| 9123        | 0.42       | Medium Risk  | Promote bundled services |
| 3345        | 0.12       | Low Risk     | No action required       |

Each row directly answers: **“What should the business do for this customer?”**

---

## 10. Business Impact & Practical Use

### Who Benefits

* **Retention Teams:** Prioritized customer lists
* **Marketing Teams:** Targeted campaigns instead of blanket discounts
* **Leadership:** Visibility into revenue at risk
* **Data Teams:** Reproducible and governed ML pipeline

### Key Insights

* Month-to-month customers with high charges churn the most
* Long-tenured customers with contracts churn the least
* Add-on services significantly reduce churn

---

**“This project transforms churn prediction into a scalable, governed, and actionable decision-support system that enables businesses to reduce customer attrition proactively.”**
