# retail-supply-chain-analytics
End-to-end retail supply chain analytics project using SQL (50 queries), Power BI interactive dashboards, and Excel Pivot Tables for sales, profitability, and Pareto (80/20) analysis.
## Project Overview
This project analyzes sales performance using Excel, SQL Server, and Power BI to identify revenue, profitability, product, regional, salesperson, customer, and discount-related trends.
## Tools

• Excel <br>
• SQL Server / SSMS <br>
• Power BI <br>
• PowerPoint <br>
## Business Problem
The objective of this project is to evaluate retail sales performance and identify the key factors influencing revenue and profitability. The analysis focuses on sales trends over time, product and regional performance, salesperson performance, customer segments, and the relationship between discounts and profitability. 

The project aims to answer key business questions such as:  <br>

• How are sales and profitability performing overall and over time?  <br>
• Which products, categories, and regions contribute most to sales and profit?  <br>
• How does salesperson performance vary across the business?  <br>
• How do discount levels affect profitability?  <br>
• Which customers and customer segments generate the most value?  <br>
• Which products contribute most to total sales, and what does the Pareto (80/20) analysis reveal?  <br>
## Dataset
### Data source 
This project utilizes the [Retail Supply Chain Sales Dataset](https://www.kaggle.com/datasets/shandeep777/retail-supply-chain-sales-dataset?utm_source=chatgpt.com).
### Dataset Size
• Row Count: 9,994 rows <br>
• Column Count: 23 columns
### Data Grain
One row represents one order line item.
### Key Identifiers
• Row ID — unique identifier for each row/order line. <br>
• Order ID — identifies the order and can appear multiple times because an order may contain multiple line items.
### Main Data Fields
The dataset contains the following information: <br>
• Order information — Row ID, Order ID, Order Date, Ship Date, Ship Mode <br>
• Customer information — Customer ID, Customer Name, Segment <br>
• Geographic information — Country, City, State, Postal Code, Region <br>
• Sales information — Retail Sales People, Product ID, Category, Sub-Category, Product Name <br>
• Transaction status — Returned <br>
• Financial metrics — Sales, Discount, Profit <br>
• Volume — Quantity <br>.
### Data Dictionary
For detailed data definitions, view the [Data Dictionary (Word Document)](Data_Dictionary.docx).
## Data Quality Assessment & Cleaning

Prior to conducting dynamic Pivot Table analysis in Excel and executing analytical SQL queries, a systematic **Data Quality Assessment (DQA)** was executed to validate the dataset across the core dimensions of data governance and data cleanliness.

---

### 1. Data Quality Dimensions Audit

The dataset was thoroughly evaluated against the 6 primary data quality dimensions:

* **Completeness:** Audited key fields (`Sales`, `Profit`, `Order Date`, `Customer ID`) for null, blank, or missing values to prevent missing-data bias in financial aggregations.
* **Accuracy:** Verified numerical ranges—ensured no unrealistic pricing, verified `Quantity` values are positive integers, and validated that `Discount` remains bounded between 0.00 and 1.00 (0%–100%).
* **Consistency:** Audited text fields (`Region`, `Category`, `Country`) to eliminate typos, trailing whitespaces, or duplicate representations caused by case-sensitivity. Confirmed `Returned` values follow a uniform binary format ('Not' / 'Returned').
* **Validity:** Validated data formats across all columns—specifically identified and corrected data type mismatches (e.g., fields stored as text instead of numeric/date format).
* **Uniqueness:** Audited transaction logs for duplicate Order IDs and identical transaction rows to avoid artificial revenue inflation.
* **Integrity:** Cross-checked relational dependencies and temporal logic between fields (e.g., `Ship Date` vs. `Order Date`).

---

### 2. Business Logic & Operational Validation

Beyond basic data hygiene, specific commercial business rules were tested:

* **Temporal Rules:** Verified that `Ship Date >= Order Date` across all historical rows to guarantee logical supply chain fulfillment order.
* **Commercial Consistency:** Validated math relationships between `Quantity`, `Sales`, and `Unit Price` to ensure accurate line-item pricing.
* **Profit Margin & Discount Dynamics:** Cross-examined high-discount records against net margin levels to flag margin degradation and negative-profit transactions (`Profit < 0`).
* **Geographical Mapping:** Audited `Postal Code` entries for anomalies and format consistency against corresponding regions.

---

### 3. Key Excel Data Cleaning & Formatting Actions

* **Data Type Standardization:** Reclassified columns to their correct physical data types in Excel. Notably converted the `Quantity` field from raw `General` text format to standard numeric format to enable proper aggregation, filtering, and mathematical calculations in Pivot Tables.
* **Return Status Handling & Sales Filtering:** Observed that returned orders (`Returned = 'Yes'`) retained their original sales values to indicate historical transaction amount rather than net kept sales. To prevent artificial revenue inflation and ensure accurate performance metrics, all subsequent Excel Pivot Table calculations and SQL models strictly filtered for non-returned orders (`Returned = 'Not'`).
## Excel Pivot Table Analysis

The analytical workflow in Excel was structured across dedicated interactive Pivot Table sheets to dissect supply chain performance from multiple operational angles:

* **Overall Performance:** Evaluated macro-level metrics including Total Revenue, Net Profit, Total Orders, and Average Order Value (AOV) excluding returned transactions.
  
  ![Overall Performance](Excel_screenshots_overall_performance.png)

* **Time Series Analysis:** Analyzed monthly performance dynamics including Total Sales, Month-over-Month (MoM) Sales Growth %, Total Quantity, Distinct Order Count, and Total Profit to identify seasonal peaks (e.g., November as the best month, February as the lowest month).
  
  ![Time Analysis](Excel_screenshots_time_analysis.png)

* **Product Performance:** Structured a detailed hierarchical Pivot Table breakdown across main categories and sub-categories, evaluating Total Sales, Quantity Sold, and Net Profit to identify high-margin products alongside loss-making sub-categories (e.g., Tables and Bookcases).
  
  ![Product Performance](Excel_screenshots_product_performance.png)

* **Regional Dynamics:** Created a multi-level geographic Pivot Table analyzing volume, total revenue, and net profit across Region and State levels to pinpoint top-performing markets (e.g., California) versus unprofitable states (e.g., Arizona, Colorado).
  
  ![Regional Performance](Excel_screenshots_regional_performance.png)

* **Salesperson Performance:** Evaluated individual sales representative performance by aggregating order volume (Distinct Count of Order ID), total revenue generation, and net profit margins to identify top revenue and profit contributors (e.g., Anna Andreadi and Chuck Magee).
  
  ![Salesperson Performance](Excel_screenshots_salesperson_performance.png)

* **Discount & Profitability:** Cross-examined dynamic discount tiers against overall sales and net profit margins, revealing that discount rates exceeding 20% lead to severe profit erosion and negative profitability (e.g., reaching up to -182% margin at 80% discount).
  
  ![Discount and Profitability](Excel_screenshots_discount_profitability.png)

📂 **File Path:** [`Excel/Retail-Supply-Chain-Sales-Dataset(ANALYSIS).xlsx`](Excel/Retail-Supply-Chain-Sales-Dataset(ANALYSIS).xlsx)




# Retail Supply Chain Analytics

End-to-end retail supply chain analytics project using Excel, SQL Server, Power BI, and PowerPoint to analyze sales performance, profitability, product and regional performance, salesperson performance, customer segments, and discount-related profitability.

---

## 1. Project Overview

This project analyzes retail sales data to evaluate overall business performance and identify the main factors influencing revenue and profitability.

The analysis was developed using a structured workflow:

- Data Documentation
- Data Quality Assessment
- Data Cleaning and Validation
- Excel Pivot Table Analysis
- SQL Server Analysis
- Power BI Dashboard Development
- Business Insights and Recommendations

The project follows a business-oriented analytical approach, starting with understanding the dataset and validating data quality before performing analysis.

---

## 2. Tools

- **Microsoft Excel** — Data validation, cleaning, Pivot Tables, KPI analysis, and exploratory analysis
- **SQL Server / SSMS** — Data analysis and analytical queries
- **Power BI** — Interactive dashboards and visualization
- **PowerPoint** — Presentation of analytical findings and recommendations

---

## 3. Business Problem

The objective of this project is to evaluate retail sales performance and identify the key factors influencing revenue and profitability.

The analysis focuses on:

- Sales and profitability over time
- Product and category performance
- Regional performance
- Salesperson performance
- Customer and customer segment performance
- Discount and profitability relationships
- Product contribution to total sales
- Pareto (80/20) analysis

The project aims to answer business questions such as:

- How are sales and profitability performing overall and over time?
- Which products and categories contribute most to sales and profit?
- Which regions generate the highest sales and profit?
- How does salesperson performance vary across the business?
- How do different discount levels relate to profitability?
- Which customer segments and customers generate the most value?
- Which products contribute most to total sales?
- What does the Pareto (80/20) analysis reveal about sales concentration?

---

## 4. Dataset

### 4.1 Dataset Source

This project uses the **Retail Supply Chain Sales Dataset** from Kaggle.

Dataset source:

https://www.kaggle.com/datasets/shandeep777/retail-supply-chain-sales-dataset

### 4.2 Dataset Size

- **Rows:** 9,994
- **Columns:** 23

### 4.3 Data Grain

**One row represents one order line item.**

This distinction is important because a single order can contain multiple products or line items.

Therefore:

- `Row ID` represents an individual order-line record.
- `Order ID` can appear multiple times.
- Order-level metrics such as Total Orders must use distinct `Order ID` values rather than counting rows.

### 4.4 Key Identifiers

- **Row ID** — unique identifier for each order-line record
- **Order ID** — identifier of the customer order; can repeat when an order contains multiple line items
- **Customer ID** — identifier of the customer
- **Product ID** — identifier of the product

### 4.5 Main Data Fields

The dataset contains information across the following business areas:

**Order Information**
- Row ID
- Order ID
- Order Date
- Ship Date
- Ship Mode

**Customer Information**
- Customer ID
- Customer Name
- Segment

**Geographic Information**
- Country
- City
- State
- Postal Code
- Region

**Sales and Product Information**
- Retail Sales People
- Product ID
- Category
- Sub-Category
- Product Name

**Transaction Status**
- Returned

**Financial Metrics**
- Sales
- Discount
- Profit

**Volume**
- Quantity

### 4.6 Data Documentation

Before beginning the analysis, a separate Data Dictionary was prepared to document:

- Column names
- Business meaning
- Data types
- Field categories
- Identifier and metric roles

This documentation was used as a reference during data validation, cleaning, and analysis.

**Data Dictionary:**  
`Data_Dictionary.docx`

---

## 5. Data Quality Assessment & Cleaning

Before performing analytical calculations, the dataset was systematically reviewed to assess data quality and validate whether the records were suitable for business analysis.

The main validation areas were:

- Completeness
- Uniqueness
- Data types
- Categorical consistency
- Numerical validity
- Date validity
- Business logic
- Outliers
- Return-status handling

### 5.1 Completeness Check

The dataset was checked for blank or missing cells.

Excel's **Go To Special → Blanks** functionality was used to check the dataset for blank values.

**Result:** No blank cells were identified in the dataset.

The dataset was also searched for placeholder values such as:

- `N/A`
- `Unknown`
- `-`
- `0`

using exact cell matching.

No such placeholder values requiring treatment as missing data were identified.

---

### 5.2 Duplicate Check

The dataset was reviewed for duplicate records.

`Row ID` was checked for duplicates and no duplicate Row IDs were identified.

Repeated `Order ID` values were also investigated.

Because the dataset has an **order-line grain**, repeated Order IDs are expected when one order contains multiple line items. Therefore, repeated Order IDs were not treated as duplicate records.

This distinction was important for calculating order-level KPIs such as:

**Total Orders = Distinct Count of Order ID**

---

### 5.3 Data Type Validation

Column data types were reviewed and standardized where necessary.

Key data types included:

| Field | Data Type |
|---|---|
| Row ID | General |
| Order ID | General |
| Order Date | Date |
| Ship Date | Date |
| Ship Mode | General |
| Customer ID | General |
| Customer Name | General |
| Segment | General |
| Country | General |
| City | General |
| State | General |
| Postal Code | General |
| Region | General |
| Retail Sales People | General |
| Product ID | General |
| Category | General |
| Sub-Category | General |
| Product Name | General |
| Returned | General |
| Sales | Number |
| Quantity | Number |
| Discount | Number |
| Profit | Number |

`Quantity` was specifically converted from General format to a numeric format with zero decimal places to ensure correct aggregation and calculation in Pivot Tables.

Identifier fields such as `Row ID`, `Order ID`, `Customer ID`, and `Product ID` were retained as identifiers rather than being treated as numerical measures.

---

### 5.4 Categorical Data Validation

Categorical fields were reviewed using Excel functions such as `UNIQUE` and `FILTER`.

The following types of fields were checked:

- Region
- Category
- Sub-Category
- Ship Mode
- Segment
- Returned
- Salesperson
- Other categorical dimensions

No obvious inconsistent categorical values requiring correction were identified.

---

### 5.5 Numerical Validation

Numerical fields were checked against basic business rules.

#### Quantity

Quantity values were checked for zero or negative values.

**Result:** No invalid zero or negative quantities were identified.

#### Discount

Discount values were checked to ensure they remained within the expected range of:

**0 to 1 (0%–100%)**

No values outside this range were identified.

#### Sales and Profit

Sales and Profit values were reviewed for unusual or logically inconsistent values.

Negative Profit values were not automatically treated as errors because negative profit can represent legitimate loss-making transactions.

---

### 5.6 Date Validation

The relationship between `Order Date` and `Ship Date` was validated.

Business rule:

```text
Ship Date >= Order Date
```
All checked records followed this rule.

No records were identified where a product was shipped before the corresponding order date.

---

### 5.7 Business Logic Validation

Additional relationships between fields were checked to determine whether the data behaved logically from a business perspective.

#### Unit Price

A calculated Unit Price was created:

```text
Unit Price = Sales / Quantity
```
Unit prices were reviewed across products and transactions.

Different unit prices for the same product were not automatically treated as errors because prices can vary between transactions due to factors such as discounts, dates, regions, and sales conditions.

#### Profit and Sales

Profit values were reviewed against Sales to identify logically inconsistent records.

No obvious cases were identified where:

- Profit was greater than Sales
- Profit was lower than negative Sales
---
### 5.8 Outlier Investigation

Potential outliers were reviewed by sorting important numerical fields.

The following fields were investigated:

- Sales
- Quantity
- Profit

Large positive and negative Profit values were investigated rather than automatically removed. For example, the lowest observed Profit value was approximately -6,599.98. This record was investigated and had a 70% discount, providing a plausible business explanation for the large loss. Therefore, the record was retained. This follows the principle: An outlier is not automatically an error.



