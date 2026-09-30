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
To ensure the dataset was analytics-ready, the following baseline validations were evaluated: <br>
1. Data Quality Assessment (Key Questions Asked)
**Missing & Null Values:** Are there any empty or missing critical fields (e.g., Sales, Profit, Order Date, Customer ID)?
**Duplicate Records:** Do duplicate transaction rows or duplicate Order IDs exist?
**Data Type Consistency:** Are numerical fields (Sales, Profit, Quantity) correctly formatted as numeric values, and dates formatted as Standard Date types?
**Outliers & Anomalies:** Are there negative sales values, unrealistic profit margins, or logical errors in order vs. ship dates?
**Data Integrity & Standard Formatting:** Are text fields (e.g., Country, Region, Category) consistent without trailing spaces or case-sensitivity variations?






