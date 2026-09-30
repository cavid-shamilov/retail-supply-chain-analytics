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
### Data Quality Assessment & Business Logic Validation

To ensure data integrity prior to running exploratory analysis, a comprehensive audit was executed across categorical consistency, numerical boundaries, and business rules.

#### 1. Invalid & Inconsistent Value Checks
* **Categorical Consistency:** Validated unique entries across `Region` and `Category` fields to eliminate typos, trailing spaces, or duplicate representations. Verified that `Returned` status strictly holds binary standard values (e.g., 'Not' / 'Returned').
* **Numerical Boundary Audit:** Checked `Quantity` for zeros or negative values, ensured `Discount` rate stays strictly within the logical range of 0.00 to 1.00 (0%–100%), and audited `Sales` and `Profit` for anomalies.
* **Geographical Fields:** Screened `Postal Code` entries for format inconsistencies and missing spatial mappings.

#### 2. Business Logic & Operational Validation
* **Temporal Logic:** Confirmed that `Ship Date` is strictly equal to or after `Order Date` for all transactions (`Ship Date >= Order Date`).
* **Commercial Integrity:** Verified logic between `Quantity`, `Sales`, and `Unit Price` to ensure consistent order line items.
* **Profitability & Discount Dynamics:** Cross-examined high-discount records against profit performance to identify margin erosion and negative-profit patterns.
* **Return Alignment:** Audited order-level return flags against underlying transactional totals for proper aggregation.

#### 3. Key Excel Data Cleaning & Formatting Actions
* **Data Type Standardization:** Corrected column formatting issues; notably converted the `Quantity` field from raw `General` text format to standard numeric data type to enable proper aggregation and mathematical calculations in Pivot Tables.
* **Text Normalization:** Applied string formatting (`TRIM`, Case Normalization) to remove whitespace inconsistencies across customer names and categories.
* **Numeric Precision:** Formatted all monetary values (`Sales`, `Profit`) to standard two-decimal Currency formats.






