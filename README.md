# Ecommerce Revenue, Retention, and Customer Experience Optimization

## Executive Summary

This capstone project analyzes the Brazilian Olist ecommerce dataset to understand the drivers of revenue, retention, delivery performance, and customer satisfaction. The initial EDA shows that revenue is concentrated by customer geography and product category, repeat purchase behavior is low, and late delivery is strongly associated with poor review scores.

The Module 20 notebook also includes machine learning models to predict low customer satisfaction risk, defined as review score 1 or 2. The baseline logistic regression model achieved a ROC-AUC of **0.753**. Random forest improved the default low-review F1-score to **0.44**, and histogram gradient boosting produced the best ranking performance with a ROC-AUC of **0.761**. After threshold tuning, histogram gradient boosting achieved the strongest low-review F1-score of **0.48**.

## Rationale

Ecommerce businesses cannot improve customer experience or revenue by treating every customer and order the same. A business needs to know which customers are valuable, which orders are most likely to create poor experiences, which categories and regions drive revenue, and which operational issues hurt satisfaction.

If this question is unanswered, the business may waste marketing spend, overlook delivery problems, miss retention opportunities, and fail to prioritize the product categories or regions that matter most.

## Research Question

How can an ecommerce marketplace use historical order, customer, product, payment, delivery, geography, and review data to identify the drivers of revenue and customer satisfaction, segment customers by value and behavior, and predict poor customer outcomes so the business can improve retention, prioritize interventions, and increase long-term revenue?

## Data Sources

The project uses the **Brazilian E-Commerce Public Dataset by Olist**.

- Original source: <https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce>
- Local data folder included in this repository: [`data/`](data/)

The dataset includes approximately 100,000 ecommerce orders from Brazil between 2016 and 2018, with related tables for customers, orders, order items, payments, products, sellers, geolocation, and reviews.

The raw CSV files are included so another reviewer can clone the repository and rerun the notebook without manually downloading the dataset.

## How to Run

1. Clone the repository.
2. Install dependencies:

```bash
python3 -m pip install -r requirements.txt
```

3. Open the main notebook:

```bash
jupyter notebook Olist_EDA_Initial_Report.ipynb
```

4. Run all cells. The notebook reads from `data/` and writes visual outputs to `outputs/`.

## Methodology

The analysis follows these steps:

1. Load the relational Olist CSV files.
2. Clean the data by checking missing values, duplicates, invalid dates, and incomplete records.
3. Engineer order-level features, including revenue, freight cost, item count, payment behavior, delivery time, late delivery flag, product category, customer geography, and low-review target.
4. Engineer customer-level RFM features, including recency, frequency, monetary value, average order value, and repeat-customer indicator.
5. Perform EDA with visualizations for revenue trends, product categories, customer states, review scores, delivery performance, and outliers.
6. Create RFM-based customer segments.
7. Build and compare logistic regression, random forest, and histogram gradient boosting models to predict low customer satisfaction risk.
8. Tune the classification threshold for the best-ranking model.

## Rubric Coverage

The Module 20 submission requirements are covered as follows:

| Requirement | Coverage |
|---|---|
| README with findings and notebook link | This README includes summary findings and links to the notebooks |
| Notebook headings and formatting | `Olist_EDA_Initial_Report.ipynb` is organized with section headings and explanatory text |
| Code quality | Libraries are imported clearly, variables are named descriptively, and pandas pipelines are used for joins, aggregation, and feature engineering |
| Visualizations | The notebook includes categorical, continuous, bivariate, outlier, segmentation, and model-evaluation plots |
| Data cleaning | Missing values, duplicate rows, date parsing, delivered-order filtering, and modeling rows are reviewed |
| Feature engineering | Delivery days, late delivery, approval hours, month/day features, product volume, low-review target, freight burden, and RFM features are created |
| Outlier analysis | IQR-based outlier review and boxplots are included |
| Baseline model | Logistic regression classification model is included with ROC-AUC, precision, recall, F1-score, accuracy, ROC curve, and confusion matrix |
| Additional model comparison | Random forest and histogram gradient boosting models are compared against the baseline |
| Model selection | Final model choice is based on ROC-AUC, low-review precision, recall, F1-score, and threshold tuning |

## Results

### Key EDA Findings

- The dataset covers orders from **2016-09-04 to 2018-10-17**.
- The dataset contains **99,441 total orders** and **96,478 delivered orders**.
- Delivered item revenue is approximately **$13.2M**.
- Average delivered order value is approximately **$137.04**, while median delivered order value is approximately **$86.57**, suggesting a right-skewed revenue distribution.
- Repeat customer behavior is low: only about **3.0%** of delivered-order customers purchased more than once.
- Late delivery rate is approximately **8.1%**.
- Low review rate, defined as review score 1 or 2, is approximately **12.8%**.
- Average review score for on-time or early orders is approximately **4.29**.
- Average review score for late orders is approximately **2.57**.

### Business Interpretation

Late delivery appears to be one of the strongest operational risk factors for poor customer satisfaction. This means delivery performance is not only a logistics issue; it is also a customer retention and brand trust issue.

Revenue is also concentrated by geography and product category. This suggests that marketing, retention, and operational improvements should be targeted rather than applied equally across all customers and orders.

Additional observations from the expanded EDA:

- Some product categories have higher low-review rates, which may indicate quality, delivery, seller, or expectation-management issues.
- Freight burden varies across orders. Orders where freight cost is high relative to item value may create a weaker customer value perception.
- Payment method and installment behavior provide extra context for customer purchasing patterns and should be considered as modeling features.
- The correlation review shows that no single numeric feature fully explains review score, which supports using a multivariable baseline model.
- Outliers are present in order value, freight value, and delivery time. These are meaningful ecommerce anomalies and should be reviewed carefully rather than automatically removed.

### Baseline Model

The baseline model predicts whether an order will receive a low review score.

- Model: Logistic Regression
- Target: Low review risk, review score <= 2
- Primary metric: ROC-AUC
- Baseline ROC-AUC: **0.753**
- Low-review precision: **0.35**
- Low-review recall: **0.55**
- Low-review F1-score: **0.43**
- Overall accuracy: **0.81**

ROC-AUC was selected because the target is imbalanced and the business needs to rank orders by risk. Recall is also important because missing a poor customer experience may mean losing a customer or receiving a damaging review.

The baseline model is useful but not final. It provides a comparison point for future models such as random forest and gradient boosting.

### Model Comparison and Final Selection

I compared **Logistic Regression**, **Random Forest**, and **Histogram Gradient Boosting** models to see which model works best for predicting low customer satisfaction risk.

| Model | ROC-AUC | Accuracy | Low-review Precision | Low-review Recall | Low-review F1 |
|---|---:|---:|---:|---:|---:|
| Logistic Regression Baseline | 0.753 | 0.81 | 0.35 | 0.55 | 0.43 |
| Random Forest | 0.756 | 0.82 | 0.37 | 0.55 | 0.44 |
| Histogram Gradient Boosting | 0.761 | 0.90 | 0.73 | 0.30 | 0.42 |

The histogram gradient boosting model had the strongest ROC-AUC, meaning it was the best model for ranking orders by risk. However, at the default 0.50 threshold, it had lower recall than logistic regression and random forest. After threshold tuning, histogram gradient boosting performed best at a **0.25 threshold**, with:

- Low-review precision: **0.53**
- Low-review recall: **0.44**
- Low-review F1-score: **0.48**

For this capstone, the selected model is **Histogram Gradient Boosting with a tuned threshold of 0.25**. This is the best choice because it has the strongest overall ranking ability and the best balanced low-review F1-score after threshold tuning.

## Visual Outputs

Generated charts are saved in [`outputs/`](outputs/), including:

- Monthly revenue trend
- Top product categories by revenue
- Top customer states by revenue
- Delivery lateness and review score relationship
- Product categories with highest low-review risk
- Payment type and low-review relationship
- Freight burden and low-review relationship
- Numeric correlation heatmap
- Outlier boxplots
- RFM customer segments
- Baseline model ROC curve and confusion matrix
- Boosting model comparison chart
- Multi-model comparison chart
- Threshold tuning chart

## Next Steps

1. Refine the selected histogram gradient boosting model with cross-validation and hyperparameter tuning.
2. Tune model thresholds further based on business priorities, especially whether recall or precision is more important.
3. Add feature importance analysis to explain the model to non-technical stakeholders.
4. Build a final customer satisfaction risk scoring workflow.
5. Develop business recommendations for delivery prioritization, retention campaigns, and category strategy.

## Project Outline

- [Final problem statement](Problem_Statement_Final.md)
- [Module 20 EDA and model comparison notebook](Olist_EDA_Initial_Report.ipynb)
- [Generated visual outputs](outputs/)

## Repository Submission Files

Recommended files/folders for this GitHub submission:

```text
README.md
.gitignore
requirements.txt
Problem_Statement_Final.md
Olist_EDA_Initial_Report.ipynb
data/
outputs/
```

Do not commit generated local cache files:

```text
.ipynb_checkpoints/
.matplotlib-cache/
.DS_Store
```

## Contact and Further Information

This repository is prepared for the required capstone submission: **Assignment 20.1 Initial Report and Exploratory Data Analysis (EDA)**.
