# E-Commerce Sales & Customer Behaviour Analysis

## 1. Problem Statement

E-commerce transaction data may contain missing values, inconsistent categories, invalid dates, duplicate records and extreme values. These issues can affect the reliability of business analysis. This project uses Python to clean the dataset, perform exploratory data analysis (EDA), identify sales and profitability patterns, and provide practical business recommendations.

## 2. Dataset Overview

The project uses `ecommerce_dirty_dataset.csv`, which initially contained 100,500 rows and 16 columns. After the documented cleaning steps and duplicate removal, the dataset contained 99,518 rows and 16 columns.

| Column Group | Columns | Purpose |
|---|---|---|
| Order details | `Order_ID`, `Order_Date`, `Ship_Date` | Track orders and shipping dates. |
| Customer and location | `Customer_ID`, `Customer_Segment`, `Region`, `State` | Analyse customer segments and geographic performance. |
| Product details | `Product_Category`, `Sub_Category`, `Product_Name` | Compare product and category performance. |
| Financial details | `Sales`, `Quantity`, `Discount`, `Profit`, `Shipping_Cost` | Analyse sales, discounts, profit and shipping costs. |
| Payment | `Payment_Mode` | Review payment methods. |

## 3. Data Cleaning and Transformation

1. **Data Type Conversion:** Converted `Order_Date` and `Ship_Date` to datetime format and `Sales` and `Profit` to numeric format for accurate analysis.

2. **Duplicate Removal:** Used `df.drop_duplicates()` to remove exact duplicate records and prevent duplicate data from affecting results.

3. **Handling Inconsistent Categories:** Used `str.strip()` and `str.title()` to remove unwanted spaces and standardise product category names.

4. **Handling Invalid Dates:** Identified and removed records where `Ship_Date` was earlier than `Order_Date`, as these violate the expected shipping sequence.

5. **Handling Negative Sales:** Excluded records with negative `Sales` values based on the cleaning rules used in this project.

6. **Handling Missing Customer Segment Values:** Replaced missing `Customer_Segment` values with `Unknown` to retain records without assigning an unsupported category.

7. **Handling Missing Profit Values:** Left missing `Profit` values unchanged. Mean or median imputation was avoided because it could introduce unsupported financial estimates and potentially create inconsistent relationships between `Sales` and `Profit`.

8. **Handling Missing Shipping Cost Values:** Filled missing `Shipping_Cost` values with the median to retain records while limiting the influence of extreme values.

9. **Handling Shipping Cost Outliers:** Applied the Interquartile Range (IQR) method to calculate the upper limit and capped extreme `Shipping_Cost` values.

10. **Handling Profit Outliers:** Identified extreme `Profit` values using the IQR method, removed records where `Profit` equalled `500,000`, and capped the remaining upper outliers.

## 4. Feature Engineering

Created date-based features from the order and shipping dates to support time-based and operational analysis.

- **Order_Year:** Extracted the year from `Order_Date` to compare annual sales performance.
- **Order_Month:** Extracted the month from `Order_Date` to analyse monthly sales trends.
- **Order_Quarter:** Extracted the quarter from `Order_Date` to compare quarterly business performance.
- **Shipping_Days:** Calculated the difference between `Ship_Date` and `Order_Date` in days to analyse shipping duration.

## 5. Exploratory Data Analysis (EDA) and Key Insights

### 5.1 Univariate Analysis

Reviewed the distributions of `Sales`, `Profit`, `Discount` and `Shipping_Cost` using descriptive statistics, histograms and KDE curves to understand spread, skewness and potential outliers.

### 5.2 Bivariate Analysis

Used scatter plots and correlation analysis to examine numerical relationships.

- **Sales and Profit:** Strong positive correlation of `0.89`.
- **Shipping_Cost and Profit:** Almost no linear correlation.

### 5.3 Categorical Analysis

Compared sales and profit by region, product category and customer segment.

- **Regional Performance:** The North region recorded the highest sales.
- **Product Performance:** Electronics generated the highest sales and total profit among product categories.

### 5.4 Discount and Profitability Analysis

Average profit declined from approximately `11,564` at `0%` discount to `7,184` at `50%` discount, suggesting that higher discounts may reduce profitability.

### 5.5 Customer Analysis

Compared customer sales contribution and average order value.

- **Highest Average Order Value:** The Corporate segment recorded the highest average order value, at approximately `52,158`.

## 6. Recommendations

1. **Promote Electronics:** Focus on Electronics promotions to increase sales and profit.

2. **Control Discounts:** Compare profit at different discount levels before offering large discounts.

3. **Reduce Shipping Costs:** Identify expensive shipments and negotiate better rates with delivery partners.

4. **Improve Data Quality:** Verify missing profit values and unusual financial records using original transaction data.
