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

[Retail Supply Chain Sales Dataset](https://www.kaggle.com/datasets/shandeep777/retail-supply-chain-sales-dataset?utm_source=chatgpt.com).

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
`[Data Dictionary (Word Document)](Data_Dictionary.docx).

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

---

### 5.9 Returned Transactions

Transactions marked as returned were reviewed because the dataset contains both transaction amounts and return status.
Returned transactions were not deleted from the raw dataset.
For the main sales-performance analysis, transactions with the non-returned status:
```text
Returned = 'Not'
```
were included.

Returned transactions were excluded from the main sales and profitability calculations to avoid treating returned transactions as retained sales in the primary performance analysis.
The original records were preserved for potential future return-related analysis.

---

### 5.10 Final Data Preparation

After completing the data quality checks:

- Raw data was preserved.
- Invalid or inconsistent values were not artificially removed.
- Quantity was converted to a numeric format.
- Dates were validated.
- Numerical ranges were checked.
- Duplicate Row IDs were checked.
- Repeated Order IDs were interpreted according to the order-line grain.
- Returned transactions were excluded from the main performance analysis using the analysis rule described above.
- The dataset was considered ready for analytical analysis.

---

## 6. Excel Pivot Table Analysis

After completing the data quality assessment and preparation, Excel Pivot Tables were used to analyze sales performance from several business perspectives.

The analysis covered:

1. Overall Performance
2. Time Analysis
3. Product Performance
4. Regional Performance
5. Salesperson Performance
6. Discount & Profitability

---

### 6.1 Overall Performance

The first stage of the analysis focused on the overall performance of the business.

KPI Definitions

Total Sales: Total revenue generated from the included transactions.

Total Profit: Total profit generated from the included transactions.

Total Quantity: Total number of units sold.

Total Orders: Distinct number of orders based on Order ID.

Average Order Value (AOV)
```text
AOV = Total Sales / Total Orders
```
Overall Profit Margin
```text
Profit Margin = Total Profit / Total Sales
```
The overall Profit Margin was calculated from aggregated Profit and Sales rather than taking the simple average of row-level profit margins.
![Overall Performance](Excel_screenshots_overall_performance.png)

---

### 6.2 Time Analysis

The time analysis examined how sales performance changed over time.

The existing Calendar Table was used to support time-based analysis.

The analysis included:

- Sales by year
- Sales by month
- Profit by month
- Quantity by month
- Orders by month
- Month-over-Month (MoM) Sales Growth
- Best-performing month
- Lowest-performing month
- Year-over-Year (YoY) Sales Growth

MoM analysis was used to understand short-term changes in sales performance.
The analysis also identified November as the highest-sales month and February as the lowest-sales month within the analyzed period.
  ![Time Analysis](Excel_screenshots_time_analysis.png)
  
---

### 6.3 Product Performance

Product analysis was performed at multiple levels:

Category
Sub-Category
Product

The analysis examined:

Total Sales
Total Profit
Profit Margin
Quantity

This allowed products and product groups to be evaluated not only by revenue generation but also by profitability.

The analysis also helps identify:

- High-sales categories
- High-profit categories
- Loss-making sub-categories
- Top products by Sales
- Top products by Profit
- Products with high Profit Margin
- Products contributing significantly to total Sales
 ![Product Performance](Excel_screenshots_product_performance.png)

---

### 6.4 Regional Performance

Regional analysis was performed to compare business performance across geographic dimensions.

The analysis included:

- Region
- State

The following metrics were evaluated:

- Total Sales
- Total Profit
- Quantity
- Orders

The analysis was used to identify differences between geographic markets and to distinguish high-performing and lower-performing areas.
![Regional Performance](Excel_screenshots_regional_performance.png)

---

### 6.5 Salesperson Performance

Salesperson performance was analyzed using the Retail Sales People field.

The analysis included:

- Total Sales
- Total Profit
- Distinct Orders
  ![Salesperson Performance](Excel_screenshots_salesperson_performance.png)
---

### 6.6 Discount & Profitability Analysis

Discount levels were analyzed to understand their relationship with sales and profitability.

A Pivot Table was created with:

Rows: Discount
Values: Sum of Profit, Distinct Order Count, Sum of Sales, Profit Margin
Filter: Returned = Not


The analysis showed that average profitability generally declined at higher discount levels, with average Profit becoming negative at higher discount tiers.

However, the relationship was not perfectly linear. For example, the 10% discount level had a higher average Profit than the 0% discount level.

Therefore, the analysis identifies an association between discount levels and profitability rather than establishing that discount alone causes the change in profitability.

  ![Discount and Profitability](Excel_screenshots_discount_profitability.png)

---

## 7. Excel Analysis Summary

The Excel analysis established the main performance picture of the business before moving to SQL-based analysis.

The analysis covered:

Overall business KPIs
Sales and profitability trends over time
Product and category performance
Regional performance
Salesperson performance
Discount and profitability


The Excel analysis also established the key business metrics and analytical questions that were subsequently reproduced and extended using SQL Server.

📂 **File Path:** [`Excel/Retail-Supply-Chain-Sales-Dataset(ANALYSIS).xlsx`](Excel/Retail-Supply-Chain-Sales-Dataset(ANALYSIS).xlsx)

---

## 8. SQL Analysis

The validated dataset was subsequently imported into SQL Server for analytical querying.

The SQL analysis reproduces and extends the business questions explored during the Excel stage using SQL Server queries.

---

### 8.1 Overall Sales Performance

The first stage of the SQL analysis focuses on the overall sales performance of the company.

The following seven business questions were analyzed using SQL Server:

1. Total Sales
2. Total Orders
3. Total Quantity
4. Average Order Value (AOV)
5. Total Profit
6. Overall Profit Margin
7. Average Discount

All calculations in this section exclude returned transactions unless otherwise specified.

---

#### Question 1: What is the Total Sales of the company, excluding returned transactions?

```sql
select sum(sales) as [Total Sales]
from [Retail-Supply-Chain-Sales-Dataset]
where Returned='not'
```
Result: Total Sales: $2,116,696.58

#### Question 2: What is the Total Order Count of the company, excluding returned transactions?

```sql
select count(distinct Order_ID) as [Total Order]
from [Retail-Supply-Chain-Sales-Dataset]
where Returned='not'
```
Result: Total Orders: 4,713

#### Question 3: What is the Total Quantity of the company, excluding returned transactions?

```sql
select sum(quantity) as [Total Quantity]
from [Retail-Supply-Chain-Sales-Dataset]
where Returned='not'
```
Result: Total Quantity: 34,820 units

#### Question 4: What is the AOV of the company?

```sql
select cast(round(sum(Sales) /count(distinct Order_ID), 2, 0)as decimal(10,2)) as AOV
from [Retail-Supply-Chain-Sales-Dataset]
where Returned='not'
```
Result: Average Order Value (AOV): $449.12

#### Question 5: What is the Total Profit of the company?

```sql
select sum(profit) as [Total Profit]
from [Retail-Supply-Chain-Sales-Dataset]
where Returned='not'
```
Result: Total Profit: $263,164.66

#### Question 6: What is the Overall Profit Margin of the company?

```sql
select cast(sum(profit)/sum(sales)*100 as decimal(10,2)) as [Overal Profit Margin]
from [Retail-Supply-Chain-Sales-Dataset]
where Returned='not'
```
Result: Overall Profit Margin: 12.43%

#### Question 7: What is the Average Discount of the company?

```sql
select cast(avg(discount)*100 as decimal(10,2)) as [Average Discount]
from [Retail-Supply-Chain-Sales-Dataset]
where Returned='not'
```
Result: Average Discount: 15.73%

#### Question 8: What were the total sales for each year, excluding returned transactions?

```sql
select C.Year,sum (sales ) as [Total Sales]
from [Retail-Supply-Chain-Sales-Dataset] as RS
inner join Calendar as C
on C.Date=RS.Order_Date
where Returned='Not'
group by c.Year
order by C.year
```
Finding: Sales declined by 5.31% in 2015 compared with 2014, followed by strong growth in 2016 and 2017. The highest annual sales were recorded in 2017 at $657,713.12.

#### Question 9: What was the monthly sales trend across the analyzed period, excluding returned transactions?
```sql
select c.[Month Name],
sum (sales ) as [Total Sales]
from [Retail-Supply-Chain-Sales-Dataset] as RS
inner join Calendar as C
on C.Date=RS.Order_Date
where Returned='Not'
group by c.[Month Name],c.Month
order by c.Month
```
Finding: Monthly sales varied considerably across the year. November recorded the highest total sales at $253,077.36, while February recorded the lowest at $118,996.39.

#### Question 10: What was the monthly breakdown of total profit across the analyzed period, excluding returned transactions?

```sql
 select c.[Month Name],
sum (Profit) as [Total Profit]
from [Retail-Supply-Chain-Sales-Dataset] as RS
inner join Calendar as C
on C.Date=RS.Order_Date
where Returned='Not'
group by c.[Month Name],c.Month
order by c.Month
```
Finding: Monthly profit was highest in December at $30,274.05, followed by September at $29,567.89. April recorded the lowest monthly profit at $11,347.05. <br>
Additional Insight: The month with the highest sales was not the month with the highest profit, indicating that higher sales volume does not necessarily translate into the highest profitability

#### Question 11: What was the monthly breakdown of total orders and units sold, excluding returned transactions?

```sql
select c.[Month Name],
count(distinct order_id) as [Order Count],
sum (Quantity) as [Total Quantity]
from [Retail-Supply-Chain-Sales-Dataset] as RS
inner join Calendar as C
on C.Date=RS.Order_Date
where Returned='Not'
group by c.[Month Name],c.Month
order by c.Month
```
Finding: November had the highest number of orders (577) and units sold (4,402), while February had the lowest number of orders (250) and units sold (1,837).

#### Question 12: What was the Month-over-Month (MoM) sales growth rate, excluding returned transactions?

```sql
WITH Monthly_Sales_CTE AS (
SELECT 
C.Year,
C.Month,
C.[Month Name],
SUM(RS.Sales) AS MonthlySales
FROM [Retail-Supply-Chain-Sales-Dataset] AS RS
INNER JOIN Calendar AS C
ON C.Date = RS.Order_Date
WHERE RS.Returned = 'Not'
GROUP BY C.Year, C.Month, C.[Month Name]
)

SELECT 
Year,
Month,
[Month Name],
MonthlySales,
LAG(MonthlySales) OVER (ORDER BY Year, Month) AS PrevMonthSales,
    round(((MonthlySales - LAG(MonthlySales) OVER (ORDER BY Year, Month)) * 100.0) 
        / LAG(MonthlySales) OVER (ORDER BY Year, Month), 2) AS [MoM Sales Growth %]
FROM Monthly_Sales_CTE
ORDER BY Year, Month
```
Finding: Monthly sales growth was volatile throughout the analyzed period, with both substantial increases and decreases from month to month. November showed strong month-over-month growth in each year, particularly in 2014 (+88.53%) and 2015 (+80.54%).

#### Question 13: Which month had the highest total sales across the analyzed period, excluding returned transactions?

```sql
select top 1
c.[Month Name],
sum (Sales) as [Total Sales]
from [Retail-Supply-Chain-Sales-Dataset] as RS
inner join Calendar as C
on C.Date=RS.Order_Date
where Returned='Not'
group by c.[Month Name]
order by [Total Sales] desc
```
Result: November — $253,077.36

#### Question 14: Which month had the lowest total sales across the analyzed period, excluding returned transactions?

```sql
select top 1
c.[Month Name],
sum (Sales) as [Total Sales]
from [Retail-Supply-Chain-Sales-Dataset] as RS
inner join Calendar as C
on C.Date=RS.Order_Date
where Returned='Not'
group by c.[Month Name]
order by [Total Sales]
```
Result: February — $118,996.39

#### Question 15: What was the Year-over-Year (YoY) sales growth rate, excluding returned transactions?

```sql
WITH Annual_Sales_CTE AS (
SELECT 
C.Year,
SUM(RS.Sales) AS Annual_Sales
FROM [Retail-Supply-Chain-Sales-Dataset] AS RS
INNER JOIN Calendar AS C
ON C.Date = RS.Order_Date
WHERE RS.Returned = 'Not'
GROUP BY C.Year
)
SELECT 
Year,
Annual_Sales,
LAG(Annual_Sales) OVER (ORDER BY Year) AS PrevYearSales,
ROUND(((Annual_Sales - LAG(Annual_Sales) OVER (ORDER BY Year)) * 100.0) 
/ LAG(Annual_Sales) OVER (ORDER BY Year), 2) AS [YoY Sales Growth %]
FROM Annual_Sales_CTE
ORDER BY Year ASC
```
Finding: Sales declined by 5.31% in 2015, followed by strong growth of 33.01% in 2016 and a further 14.77% increase in 2017. Overall, annual sales reached their highest level in 2017.

Time Analysis Summary

-- Annual sales declined by 5.31% in 2015 but increased by 33.01% in 2016 and 14.77% in 2017. <br>
-- November generated the highest total sales, orders, and units sold across the analyzed period. <br>
-- February recorded the lowest total sales, orders, and units sold. <br>
-- December generated the highest total profit, despite November having the highest sales. <br>
-- Monthly sales growth was volatile, with both significant increases and decreases across different months.<br>

---

### 8.1 Product Performance
