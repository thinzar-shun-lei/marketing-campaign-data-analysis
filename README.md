# Marketing Campaign Analysis — Power BI

## 📌 Project Overview

This project analyzes **marketing campaign performance and customer behavior** using **Microsoft Power BI**. The analysis combines campaign, customer, event, product, and transaction data to evaluate marketing effectiveness throughout the customer journey.

The project focuses on understanding:

* Which campaigns and marketing channels generate the greatest business impact
* Which customer segments respond most effectively to marketing campaigns
* Where customers drop off during the purchase journey
* Which marketing channels perform best across key business metrics
* What actions can improve future marketing performance

The final Power BI dashboard provides stakeholders with an interactive view of **campaign performance, customer behavior, marketing channels, and product performance** to support data-driven marketing decisions.

---

## 🎯 Business Questions

The analysis was designed to answer five key business questions:

1. **Which marketing campaigns generated the greatest business impact?**
2. **Which customer segments respond best to our marketing campaigns?**
3. **Where are customers dropping off in the purchase journey?**
4. **Which marketing channels deliver the highest return?**
5. **What actions should we take to improve future marketing performance?**

---

## 🎯 Objectives

The project aims to answer the business questions by:

* Evaluating the performance and business impact of marketing campaigns
* Comparing actual campaign performance against expected uplift
* Identifying high-performing and underperforming campaigns
* Understanding customer purchasing and engagement behavior
* Identifying the most responsive customer segments
* Analyzing customer drop-off throughout the purchase journey
* Comparing marketing channels based on revenue, conversion, and refund performance
* Identifying high- and low-performing product categories
* Developing actionable recommendations to improve future marketing performance
* Building an interactive Power BI dashboard that enables stakeholders to explore marketing performance from different perspectives

---

# 🔍 Methodology

## 4.1 Data Connection, Cleaning & Transformation

The analysis uses multiple datasets representing different aspects of the marketing ecosystem.

| Dataset          | Description                                                                                            |
| ---------------- | ------------------------------------------------------------------------------------------------------ |
| **Campaigns**    | Campaign information, objectives, target segments, duration, and expected uplift                       |
| **Customers**    | Customer demographics, acquisition channels, and loyalty tiers                                         |
| **Events**       | Customer interactions, sessions, page categories, device types, traffic sources, and experiment groups |
| **Products**     | Product information and categories                                                                     |
| **Transactions** | Purchases, revenue, quantities, discounts, campaigns, and refunds                                      |

### Data Preparation

Key data preparation activities included:

* Reviewing data types and column structures
* Identifying missing and null values
* Checking inconsistent categorical values
* Reviewing invalid or unexpected identifiers
* Handling missing product and revenue information where appropriate
* Standardizing categorical fields
* Preparing a calendar table for time-based analysis

---

## 4.2 Data Model

A **hybrid dimensional model combining Star Schema and Snowflake Schema concepts** was used to structure the data and support efficient analysis.
<img width="1272" height="686" alt="Screenshot 2026-08-08 143158" src="https://github.com/user-attachments/assets/842530ab-d7e8-41fd-bcc9-d883af780306" />

The model connects campaign, customer, event, product, transaction, and date information to enable analysis across multiple dimensions of the customer journey.

---

## 4.3 Data Analysis & DAX Measures

DAX was used to create calculated measures and analytical metrics for the dashboard.

### Interesting DAX Measures

1. **View-to-Click Rate**

   * Measures the percentage of product views that resulted in clicks.
   * Used to identify early-stage customer engagement and potential bottlenecks in the purchase journey.
  
View-to-click rate = DIVIDE(
CALCULATE(DISTINCTCOUNT(events[session_id]), events[event_type] = "purchase"), 
CALCULATE(DISTINCTCOUNT(events[session_id]), events[event_type] = "view")
)

2. **Customer Categorization**

   * Categorizes customers based on purchasing behavior and revenue.
   * Helps identify different customer value and engagement groups.

Customer Categorization = 
SWITCH(TRUE(),
    'Customer Summary'[Repeat Purchase Time] <> 1, "Repeat Purchase Customers",
    'Customer Summary'[Total Revenue] < 0, "High Refund Customers",
    AND('Customer Summary'[Repeat Purchase Time] == 1,'Customer Summary'[Discount Applied] > 0), "One-time Discount Buyers",
    AND('Customer Summary'[View Counts] > 4000, 'Customer Summary'[Purchase Counts] < 2000), "Window Shoppers",
    AND('Customer Summary'[Avg Session Duration] < 130, 'Customer Summary'[Purchase Counts] > 2000), "Impulsive Buyers",
    AND('Customer Summary'[Repeat Purchase Time] == 1, 'Customer Summary'[Refund Times] = 1), "Single-Purchase Refunders")

Additional measures were developed to support analysis of:

* Revenue
* Conversion Rate
* Average Order Value (AOV)
* Repeat Purchase Rate
* Refund Rate
* Expected vs. Actual Campaign Performance
* Campaign Performance
* Customer and Product Performance

---

## 4.4 Data Visualization

Visualizations were selected based on four major analytical areas:

1. **Campaign Overall Effectiveness**
2. **Customer Behaviors**
3. **Marketing Channels**
4. **Product Performance**

The dashboard uses different visualization techniques to communicate business insights effectively.

### Example Visualizations

| Visualization            | Purpose                                                                             |
| ------------------------ | ----------------------------------------------------------------------------------- |
| **Combo Chart**          | Compares revenue and conversion rate across the five most recent campaigns          |
| **Bubble Chart**         | Analyzes the relationship between expected uplift and actual conversion rate        |
| **Stacked Column Chart** | Compares event-type contributions across A/B testing experiment groups              |
| **Funnel Chart**         | Identifies bottlenecks throughout the customer purchase journey                     |
| **Donut / Pie Charts**   | Analyzes customer segmentation by loyalty tier, device type, and acquisition method |

---

# 📊 Key Insights

### 1. Campaign Performance

Campaign performance was strongly associated with conversion rate. Higher-converting campaigns generally generated greater revenue, while **Campaigns 26 and 30 underperformed against their expected uplift**.

### 2. Campaign Objectives

**Reactivation campaigns** generated the highest revenue, while **Cross-sell campaigns** achieved the highest Average Order Value (AOV).

This indicates strong potential for both customer re-engagement and increasing basket value through complementary product recommendations.

### 3. Customer Segments

**Deal Seekers** responded most strongly to marketing campaigns and contributed the highest revenue.

In contrast, **Churn Risk customers** were less effectively engaged, indicating an opportunity for more targeted retention strategies.

### 4. Customer Retention

Customer retention remains a key challenge.

* Repeat Purchase Rate: **~24%**
* Most customers remained in the **Bronze loyalty tier**

This suggests opportunities to strengthen loyalty and encourage repeat purchases.

### 5. Customer Journey

The largest customer drop-off occurred early in the purchase journey.

The **View-to-Click Rate was approximately 18%**, with high bounce rates observed on **Product List** and **Product Description** pages.

This indicates that improvements to product presentation and calls-to-action could potentially increase customer engagement.

### 6. Marketing Channels

**Affiliate** was the strongest-performing marketing channel.

**Paid Search** generated high revenue but also recorded the highest refund rate, suggesting that revenue performance should be evaluated alongside customer quality and post-purchase outcomes.

**Email** was the weakest-performing channel based on the analyzed performance indicators.

### 7. Product Categories

**Electronics** and **Home** were the strongest-performing product categories, while **Grocery** underperformed.

**Sports** and **Beauty** experienced relatively high refund rates, highlighting potential opportunities to improve product targeting, descriptions, or customer expectations.

### 8. A/B Testing

The A/B test variants showed **very similar customer behavior**, suggesting that the current experiments did not produce meaningful improvements in the analyzed customer actions.

---

# 💡 Business Recommendations

### 1. Optimize Campaign Strategy

Investigate the factors behind the underperformance of **Campaigns 26 and 30** and identify which strategies contributed to the success of high-performing campaigns such as **Campaigns 9 and 31**.

### 2. Prioritize Customer Retention

Strengthen retention strategies through:

* Loyalty programs
* Personalized offers
* Targeted reactivation campaigns
* Special incentives for Churn Risk customers

### 3. Improve the Customer Journey

Improve product-listing and product-detail experiences by optimizing:

* Product images
* Product descriptions
* Pricing information
* Promotional content
* Calls-to-action

The goal is to improve the **View-to-Click Rate** and reduce early-stage customer drop-off.

### 4. Optimize Marketing Investment

Expand high-performing **Affiliate partnerships** and **Cross-sell campaigns**, while investigating opportunities to improve the effectiveness of **Email** and **Paid Search**.

### 5. Increase Customer Basket Value

Increase AOV through:

* Personalized product recommendations
* Product bundles
* Cross-selling
* Complementary-product promotions

### 6. Reduce Refund Rates

Investigate the causes of high refund rates by improving:

* Customer targeting
* Product information
* Product expectations
* Promotional accuracy
* Post-purchase customer experience

### 7. Strengthen A/B Testing

Design more meaningful A/B test variations and establish measurable success criteria to better evaluate whether changes produce improvements in customer behavior.

### 8. Establish Continuous KPI Monitoring

Continuously monitor key performance indicators such as:

* Revenue
* Conversion Rate
* Average Order Value (AOV)
* Repeat Purchase Rate
* Refund Rate

This can support ongoing, data-driven marketing decisions.

---

# ⚠️ Disclaimer: Dataset Limitations & Additional Data Requirements

This project is a **study/portfolio project based on a provided dataset** and does not represent real-time business data or the actual performance of a specific organization.

Therefore, the findings, insights, and recommendations are intended primarily for **analytical and learning purposes**.

### Customer Acquisition Cost (CAC)

CAC could not be reliably analyzed because the dataset does not contain sufficient information about **marketing spend or campaign costs**.

### Customer Lifetime Value (CLV)

CLV could not be fully evaluated because the available data does not provide sufficient information about:

* Customer-level long-term revenue
* Customer retention period
* Customer servicing costs
* Customer acquisition costs

### ROI & ROAS

**Return on Investment (ROI)** and **Return on Ad Spend (ROAS)** are also limited by the absence of reliable marketing expenditure data.

High revenue does not necessarily indicate high profitability if the associated customer acquisition or campaign costs are high.

### Additional Data Requirements

For a more comprehensive business analysis, the following data would be valuable:

* Campaign and advertising spend
* Customer acquisition costs
* Customer-level acquisition and servicing costs
* Long-term customer revenue
* Customer retention/churn history
* Marketing channel costs
* Profit or contribution margin
* Detailed campaign execution costs

These additional datasets would enable a more complete evaluation of **profitability, CAC, CLV, ROI, and ROAS**.

---
