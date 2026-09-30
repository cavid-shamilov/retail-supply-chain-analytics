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




