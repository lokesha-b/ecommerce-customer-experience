# Capstone Assignment 16.1: Finalized Problem Statement

## Ecommerce Revenue, Retention, and Customer Experience Optimization

## 1. Research Question

How can an ecommerce marketplace use historical order, customer, product, payment, delivery, seller, geography, and review data to identify the drivers of revenue and customer satisfaction, segment customers by value and behavior, and predict poor customer outcomes so the business can improve retention, prioritize interventions, and increase long-term revenue?

## 2. Dataset Selection

**Dataset:** Brazilian E-Commerce Public Dataset by Olist  
**Source:** Kaggle, `olistbr/brazilian-ecommerce`  
**Size:** about 100,000 orders, 9 interrelated CSV files, 2016-2018

This dataset was selected because it supports a realistic ecommerce analytics project with connected tables for orders, customers, products, sellers, payments, reviews, and geolocation.

## 3. Original Problem Statement Coverage

The original idea proposed four ecommerce goals: reduce churn, improve segmentation, optimize pricing, and increase conversion. The Olist dataset supports the business intent, but some original data requirements are not available in this public dataset. The refined scope below keeps the project realistic and defensible.

| Original Requirement | Olist Coverage | Final Capstone Treatment |
|---|---|---|
| Customer demographics: age, gender, income | Not available | Excluded; use customer location instead |
| Customer location | Available | Use city/state and geolocation |
| Browsing history, sessions, clicks, device usage | Not available | Excluded; no session logs |
| Email, app, and social engagement metrics | Not available | Future CRM/marketing-data extension |
| Purchase history, order values, frequency, categories | Available | Core analysis and feature engineering |
| Customer lifetime data | Partially available | Use first/last purchase, RFM, total spend, AOV |
| Product SKUs, categories, dimensions | Available | Use product IDs, category, weight, dimensions |
| Inventory, product images, descriptions | Not available | Excluded |
| Historical prices and discounts | Partially available | Use observed item prices; no promotion flags |
| Competitor prices and real-time tracking | Not available | Future external-data extension |
| Market trends, benchmarks, and competitor promotions | Not available | Future external-data extension |
| Ratings and reviews | Available | Use review score as satisfaction signal |
| Seasonality | Available | Analyze monthly order and revenue patterns |
| Cart events, search queries, abandoned carts | Not available | Excluded |
| Conversion events | Partially available | Use completed purchases and repeat purchase as proxy |

## 4. Refined Business Problems

| Original Goal | Refined Capstone Version |
|---|---|
| Customer churn prediction | Analyze one-time vs repeat purchase behavior using RFM features |
| Customer segmentation | Segment customers using recency, frequency, monetary value, geography, order value, and satisfaction |
| Dynamic pricing | Explore category-level price, demand, seasonality, and revenue patterns; true dynamic pricing needs competitor and inventory data |
| Conversion optimization | Use repeat purchase after the first order as a conversion-like proxy; true conversion modeling needs browsing and cart data |

## 5. Original Technique Coverage

| Original Technique | Final Treatment |
|---|---|
| Random Forest / XGBoost for churn prediction | Candidate models for one-time vs repeat-customer prediction |
| K-Means + hierarchical clustering for segmentation | RFM segmentation first; K-Means or hierarchical clustering can be added later |
| ARIMA/SARIMA for demand or pricing time series | Candidate methods for category-level demand forecasting |
| Gradient boosting regression for price optimization | Candidate model for demand/revenue modeling; true price optimization needs richer pricing, promotion, inventory, and competitor data |
| Logistic regression / neural networks for conversion | Candidate models for repeat-purchase likelihood; true session conversion needs browsing and cart data |

## 6. Expected Techniques

- Exploratory data analysis: missing values, revenue trends, customer geography, product categories, delivery timing, review scores.
- RFM feature engineering: recency, frequency, monetary value, average order value, repeat-customer indicator.
- Customer segmentation: rule-based RFM segmentation first, with K-Means as a later modeling extension.
- Classification modeling: logistic regression, random forest, or gradient boosting for low satisfaction risk and/or repeat-purchase likelihood.
- Pricing and demand analysis: category-level price-demand exploration and monthly demand trends.
- Model evaluation: accuracy, precision, recall, F1-score, ROC-AUC, confusion matrix, and business interpretability.

## 7. Expected Results

The expected output is a clean, order-level analytical dataset, EDA findings that explain revenue and satisfaction patterns, customer segments that can guide marketing strategy, and a feasible modeling path for predicting low review risk or repeat-purchase likelihood.

Expected business insights include:

- Which states and product categories generate the most revenue.
- Whether late delivery is associated with low customer review scores.
- Which customer groups are high value, recently active, at risk, or low engagement.
- Which order and delivery features may predict poor customer satisfaction.
- Which additional data would be required for true dynamic pricing or real-time conversion optimization.

## 8. Why This Question Is Important

If this question is not answered, the business may continue treating all customers, regions, and product categories the same. That can waste marketing budget, miss high-value customers, overlook delivery problems that damage customer trust, and leave revenue opportunities hidden in the data.

The value of this project is that it translates ecommerce data into actions that non-technical business teams can understand: where to focus retention campaigns, which customer segments need attention, which categories drive revenue, and which operational issues are most likely to hurt customer satisfaction.

## 9. Project Phases

| Phase | Deliverable | Current Status |
|---|---|---|
| Phase 1 | Data loading, cleaning, EDA, visualizations | Covered in `Olist_EDA_Analysis.ipynb` and `Capstone-Project.md` |
| Phase 2 | Feature engineering and model development | Planned next |
| Phase 3 | Pipeline, dashboard, deployment | Future work |
| Phase 4 | Business impact, A/B testing, ROI | Future work after model deployment |

## 10. Expected Business Impact

The original target impacts remain useful benchmarks, but they should not be presented as proven outcomes until future modeling and experiments are completed:

| Outcome | Future Target |
|---|---|
| Reduce churn / one-time customer behavior | 15-20% decrease through targeted retention |
| Improve repeat purchase behavior | 10-15% increase through personalized campaigns |
| Improve revenue from pricing/category strategy | 5-10% uplift after testing |
| Improve customer lifetime value | Higher average value across priority customer segments |

*Prepared for: Capstone Assignment 16.1, Finalizing Your Problem Statement*
