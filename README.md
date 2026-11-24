# Cloud_Infrastructure_Cost_Prediction
# ☁️ Intelligent Cloud Infrastructure Cost Prediction & Resource Optimization System

## 📌 Project Overview

Cloud infrastructure costs can increase rapidly due to resource utilization, server configurations, network traffic, storage consumption, and pricing models.

This project uses Machine Learning to predict monthly cloud infrastructure expenses across multi-cloud environments (AWS, Azure, and GCP). It also explores cost optimization strategies through resource utilization analysis, scenario simulation, and FinOps recommendations.

**Project Domain:** Cloud Computing | DevOps | FinOps | Machine Learning

**Problem Type:** Supervised Machine Learning – Regression

**Target Variable:** `Monthly_Cost_USD`

## 🎯 Project Objectives

- Predict monthly cloud infrastructure expenditure.
- Identify the major factors influencing cloud costs.
- Analyze relationships between resource utilization and infrastructure expenses.
- Compare different regression algorithms.
- Perform what-if scenario analysis for resource growth.
- Identify potential savings through right-sizing and Reserved Instances.
- Provide actionable cloud cost optimization recommendations.

## 🛠️ Technologies & Tools

| Category | Tools |
|---|---|
| Programming | Python |
| Data Manipulation | Pandas, NumPy |
| Data Visualization | Matplotlib, Seaborn |
| Machine Learning | Scikit-learn |
| Development Environment | Jupyter Notebook |
| Version Control | Git, GitHub |

## 📊 Dataset Overview

The project uses a synthetic cloud infrastructure dataset containing **102,000 records and 24 columns**.

The dataset represents infrastructure distributed across AWS, Azure, and GCP.

### Feature Categories

**1. Infrastructure Identification**
- Server_ID
- Cloud_Provider
- Region
- Instance_Type
- Environment
- Application_Type

**2. Resource Utilization**
- CPU_Usage_Percent
- Memory_Usage_Percent
- Storage_GB
- Network_Traffic_GB
- Running_Hours
- VM_Count
- Database_Queries
- Active_Users
- Peak_CPU_Usage
- Peak_Memory_Usage

**3. Billing & Pricing**
- CPU_Hour_Rate
- Memory_Hour_Rate
- Storage_GB_Rate
- Network_GB_Rate
- Region_Pricing_Factor
- Discount_Percentage
- Reserved_Instance_Flag

**4. Target Variable**
- Monthly_Cost_USD

## 🧹 Data Cleaning & Preprocessing

The initial dataset inspection identified several data quality issues:

- Numeric columns stored as object data types.
- Missing values in resource utilization and billing columns.
- Duplicate records.
- Negative and unrealistic resource values.
- Extreme monthly cost outliers.
- Inconsistent environment labels.

### Cleaning Activities

- Converted relevant columns into appropriate numeric data types.
- Removed duplicate records.
- Removed records with missing target values.
- Handled missing feature values using median imputation.
- Identified and addressed invalid resource values.
- Standardized inconsistent categorical labels.

**Final cleaned dataset:** 99,675 records.

## 📈 Exploratory Data Analysis (EDA)

EDA was performed to understand resource utilization patterns, cloud infrastructure costs, and potential cost drivers.

Key observations:

- Median monthly infrastructure cost: **$257.19**
- Mean monthly infrastructure cost: **$695.17** before outlier removal.
- Median CPU utilization: **57.20%**
- Median memory utilization: **56.37%**
- Median storage consumption: **383.96 GB**
- Median network traffic: **1,201.94 GB**
- Median running hours: **671 hours/month**

The monthly cost distribution was heavily right-skewed due to high-cost infrastructure records and extreme outliers.

## ⚙️ Feature Engineering

Additional features were developed to represent cloud billing and infrastructure behavior more effectively.

Key feature engineering activities:

- Combining VM_Count and Running_Hours to represent total compute hours.
- Creating utilization-based features using CPU and memory consumption.
- Incorporating CPU and memory pricing rates.
- Accounting for regional pricing factors and discounts.
- Encoding categorical variables such as Cloud_Provider, Instance_Type, Environment, and Application_Type.
- Applying polynomial transformations to capture nonlinear relationships.

## 🤖 Machine Learning Experiments

All models were evaluated using an **80/20 Train-Test Split**.

### Experiment 1: Simple Linear Regression

**Feature Used:** CPU_Usage_Percent only.

| Metric | Result |
|---|---:|
| MAE | $739.15 |
| RMSE | $2,916.63 |
| R² Score | -0.0224 |

**Observation:** CPU utilization alone is insufficient to accurately estimate infrastructure expenses because it does not capture server size, VM count, running hours, storage, network traffic, and pricing discounts.

### Experiment 2: Multiple Linear Regression

**Features Used:** CPU, Memory, Storage, Network Traffic, Running Hours, and additional pricing/VM features where included.

| Metric | Result |
|---|---:|
| MAE | $285.16 |
| RMSE | $444.09 |
| R² Score | 0.2297 |

**Observation:** Combining multiple infrastructure features improved prediction performance compared with using CPU utilization alone.

### Experiment 3: Polynomial Regression

**Transformation:** Polynomial Features (Degree 2).

| Metric | Result |
|---|---:|
| MAE | $29.01 |
| RMSE | $47.42 |
| R² Score | 0.9912 |

**Observation:** Polynomial Regression captured nonlinear relationships and interaction effects more effectively than standard linear regression.

### Experiment 4: Final Model Comparison

| Model | MAE ($) | RMSE ($) | R² Score |
|---|---:|---:|---:|
| Simple Linear Regression | 739.15 | 2,916.63 | -0.0224 |
| Multiple Linear Regression | 285.16 | 444.09 | 0.2297 |
| Polynomial Regression | 29.01 | 47.42 | 0.9912 |

**Final Tuned Model:** Ridge Polynomial Regression

**Reported R² Score:** 0.9913

The final tuned model is reported separately from the initial three-model comparison. Its performance should be validated on an untouched test set to confirm generalization.

## 💰 FinOps Cost Prediction & Scenario Analysis

The final model was used to estimate infrastructure expenditure and evaluate potential cost optimization scenarios.

### 1. Monthly Cost Prediction

| Metric | Result |
|---|---:|
| Evaluated Servers | 20,400 |
| Predicted Monthly Expenditure | $8,848,482.88 |
| Average Cost per Server | $433.75 |

### 2. Resource Growth Analysis

| Resource Growth | Additional Monthly Cost | Bill Increase |
|---|---:|---:|
| +10% | $385,713.98 | 4.36% |
| +20% | $767,514.73 | 8.67% |
| +25% | $958,415.11 | 10.83% |
| +50% | $1,823,835.65 | 20.61% |

The estimates demonstrate how increasing CPU, memory, and storage consumption can raise monthly cloud expenditure. High resource utilization can also trigger nonlinear burst and autoscaling penalties.

### 3. Cost Optimization & Savings

The proposed optimization strategy combines:

- Right-sizing underutilized virtual machines.
- Applying Reserved Instance pricing to eligible Production servers.
- Reducing idle Development and Testing server running hours.

**Reported optimization results:**

| Metric | Estimated Savings |
|---|---:|
| Monthly Savings | $1,059,492.19 |
| Annual Savings | $12,713,906.28 |
| Monthly Bill Reduction | 12.0% |

These figures represent scenario-analysis estimates rather than guaranteed savings.

## 📊 Model Visualization & Diagnostics

The project includes visual analysis such as:

- Actual vs. Predicted Monthly Cost.
- Residual Distribution.
- Residuals vs. Predicted Values.
- Model Performance Comparison.
- Feature Coefficient Analysis.

These visualizations help assess prediction performance, residual behavior, and the relative influence of model features.

## 💡 Key Business Insights & Recommendations

1. **Monitor resource utilization:** Maintain average CPU and memory utilization between 40% and 65% as a proposed operating target.
2. **Right-size infrastructure:** Reduce unnecessary computing capacity in underutilized virtual machines.
3. **Optimize pricing:** Use Reserved Instances for stable Production workloads.
4. **Schedule non-production workloads:** Shut down Development and Testing servers outside business hours.
5. **Monitor network consumption:** Track network egress as an important infrastructure cost component.
6. **Improve FinOps visibility:** Standardize environment labels and continuously monitor resource-level expenditure.

## 📁 Project Structure

```text
03_Cloud_Infrastructure_Cost_Prediction/
│
├── README.md
├── Cloud_Cost_Prediction.ipynb
├── Project_Report.docx
│
├── models/
│   └── (Saved Machine Learning Models)
│
└── visualizations/
    └── (EDA and Model Evaluation Charts)
```

## 🚀 Project Outcomes

- Built a regression-based cloud infrastructure cost prediction workflow.
- Compared Simple, Multiple, and Polynomial Regression models.
- Developed a final tuned Ridge Polynomial model.
- Analyzed cloud infrastructure cost drivers.
- Performed resource growth and optimization scenario analysis.
- Estimated potential monthly and annual cloud cost savings.
- Translated machine learning results into actionable FinOps recommendations.

## ⚠️ Disclaimer

This project uses synthetic cloud infrastructure data and simulated pricing relationships for educational and portfolio purposes. Cost estimates and savings scenarios are model-based estimates, not actual AWS, Azure, or GCP billing quotations.

Model performance metrics should be interpreted in the context of the dataset and validated for data leakage and overfitting before real-world deployment.

## 👨‍💻 Author

**Kishore Kumar**

B.Tech – Information Technology

Interested in Data Analytics, Machine Learning, Cloud Computing, and AI-driven business solutions.
