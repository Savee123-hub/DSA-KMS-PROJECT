# DSA-KMS-PROJECT
This is where I started my portfolio building when taking a data analysis class on incubator hub

## PROJECT TPOIC: Kultra Mega Stores Inventory

## PROJECT OVERVIEW:
This repository presents a detailed analysis of KMS's sales, customers, and shipping performance using real business data. The project is divided into three main sections: Sales Analysis, Customer Analysis, and Shipping Analysis. Each section answers specific business questions to support data-driven decisions that can help KMS improve profitability, reduce operational inefficiencies, and better serve its customers.

### Data Source
This project is based on two primary datasets: “KMS SQL Case Study.csv” and “Orders_Status.csv”, both sourced from the DSA LMS Dashboard for analytical exploration.

### TOOL USED
- SQL Server (For data querying and analysis)  [Download here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
 
### Data cleaning and Preparation
The data cleaning and preparation stage includes:  
1. Importing the data and reviewing its structure  
2. Managing any missing or incomplete values  
3. Formatting and cleaning the data to ensure consistency and readiness for analysis

### Exploratory Data Analysis 
- EDA focused on analyzing the dataset to uncover insights and answer key business questions such as:  
  - Which product category had the highest sales?
  - What are the Top 3 and Bottom 3 regions in terms of sales?
  - What were the total sales of appliances in Ontario?
  - Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers
  - KMS incurred the most shipping cost using which shipping method?
  - Who are the most valuable customers, and what products or services do they typicall purchase?
  - Which small business customer had the highest sales?
  - Which Corporate Customer placed the most number of orders in 2009 – 2012?
  - Which consumer customer was the most profitable one?
  - Which customer returned items, and what segment do they belong to?
  - If the delivery truck is the most economical but the slowest shipping method and
Express Air is the fastest but the most expensive one, do you think the company
appropriately spent shipping costs based on the Order Priority? Explain your answer

### Data Analysis  
Here, I present essential code, queries, I applied throughout the data analysis to derive meaningful insights.

### SQL QUERIES AND ANSWERS 
- To get Which product category had the highest sales, run the below query.
  - The result given is "Technology Category" with Total_Sales of "5984248.183"

  ```` Sql
   SELECT 
    Product_category, 
    SUM(Sales) AS Total_Sales
   FROM 
    [dbo].[KMS Sql Case Study]
  GROUP BY 
    Product_category
  ORDER BY 
    Total_Sales DESC
  ````

- To get the Top 3 and Bottom 3 regions in terms of sales, run the below query.
  - Top 3 region are "West, Ontario, Prarie"
  - Bottom 3 region are "Nunavut, Northwest Territories, Yukon"

```` sql
   SELECT TOP 3
	Region, sum(Sales) as total_sales
FROM [dbo].[KMS Sql Case Study]
GROUP BY Region
order by total_sales desc


SELECT TOP 3
	Region, sum(Sales) as total_sales
FROM [dbo].[KMS Sql Case Study]
GROUP BY Region
order by total_sales ASC
````



