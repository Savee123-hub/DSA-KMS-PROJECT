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
- ### To get Which product category had the highest sales, run the below query.
  - The result given is "Technology Category" 

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

- ### To get the Top 3 and Bottom 3 regions in terms of sales, run the below query.
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

- ### To get the total sales of appliances in Ontario, run the below query.
  - The result given is "202346.840"

```` Sql
SELECT 
	Region, sum(Sales)as total_sales , Product_Sub_Category
FROM [dbo].[KMS Sql Case Study]
WHERE REGION = 'ONTARIO'and Product_Sub_Category='Appliances'
GROUP BY Region,Product_Sub_Category
order by total_sales
````

- ### KMS incurred the most shipping cost using which shipping method, run the below query.
  - The result given is "Delivery Truck"

```` Sql
  select 
ship_mode,sum (shipping_cost)as total_cost
from [dbo].[KMS Sql Case Study]
group by ship_mode
order by total_cost desc
````

- ### To get the most valuable customers, and the products or services they typicall purchase, run the below query.

```` sql
  select top 10
Customer_Name,product_Name,sum(Profit) as total_profit
from [dbo].[KMS Sql Case Study]
group by Customer_Name, product_Name
order by total_profit desc
````
- ### The result given:
  - Top Valuable Customers and Their Most Purchased Products
    
| Customer Name       | Most Profitable Product                                                                          | Total Profit |
|---------------------|--------------------------------------------------------------------------------------------------|--------------|
| Emily Phan          | Polycom ViewStation™ ISDN Videoconferencing Unit                                                 | 27,221.00    |
| Clytie Kelty        | Canon PC940 Copier                                                                               | 15,601.00    |
| Andy Reiter         | Polycom ViaVideo™ Desktop Video Communications Unit                                              | 14,440.00    |
| Deborah Brumfield   | Hewlett Packard LaserJet 3310 Copier                                                             | 13,340.00    |
| Karen Carlisle      | Canon Image Class D660 Copier                                                                    | 12,749.00    |
| Rick Wilson         | HP Business Color Inkjet 3000 [N, DTN] Series Printers                                           | 12,607.00    |
| Raymond Book        | Hewlett Packard LaserJet 3310 Copier                                                             | 11,984.00    |
| Logan Haushalter    | Hewlett Packard LaserJet 3310 Copier                                                             | 11,630.00    |
| Nick Crebassa       | HP Business Color Inkjet 3000 [N, DTN] Series Printers                                           | 11,562.00    |
| John Stevenson      | Fellowes PB500 Electric Punch Plastic Comb Binding Machine with Manual Bind                      | 11,535.00    |


- ### To get Which small business customer had the highest sales, run the below query.
  - The result given is "Dennis Kane"

````sql
  select top 1
customer_name, customer_segment, sum(sales) as highest_sales
from[dbo].[KMS Sql Case Study]
where customer_segment='Small business'
group by customer_name,customer_segment
order by highest_sales desc
```` 

- ### To get Which Corporate Customer placed the most number of orders in 2009 – 2012, run the below query.
  - The result given is "Roy Skaria"

````sql
  alter table [dbo].[KMS Sql Case Study]
add order_year int

update [dbo].[KMS Sql Case Study]
set order_year =year(order_date)

select top 1
Customer_Name,Customer_Segment,count (distinct Order_year)as sumed_year,
sum(Order_Quantity)as most_Orders
from [dbo].[KMS Sql Case Study]
where Customer_Segment='Corporate' 
group by Customer_Name,Customer_Segment
order by most_Orders desc
````

- ### To get Which consumer customer was the most profitable one, run the below query.
  - The result given is "Emily Phan"

````sql
   select top 1
customer_name, customer_segment, sum (profit) as most_profitable
from[dbo].[KMS Sql Case Study]
where customer_segment= 'Consumer'
group by customer_name, customer_segment
order by most_profitable desc
````

- ### To get Which customer returned items, and what segment they belong to, run the below query.
  - The result given is "see result afer running the query below"

````sql
   select distinct
[dbo].[KMS Sql Case Study].Order_ID,
[dbo].[KMS Sql Case Study].Customer_Name,
[dbo].[KMS Sql Case Study].Customer_Segment,
[dbo].[Order_Status].Status
from[dbo].[KMS Sql Case Study]
inner join [dbo].[Order_Status]
on [dbo].[Order_Status].Order_ID=[dbo].[KMS Sql Case Study].Order_ID
````

- ## Advise to the management of KMS on what to do to increase the revenue from the bottom 10 customers

| Customer Name      | Product Description                                                    | product_Category | Order_Priority       | Shipping Mode   | Shipping Cost | Profit       |
|--------------------|------------------------------------------------------------------------|--------------|----------------|------------------|----------------|--------------|
| Roy Phan           | Polycom ViewStation™ ISDN Videoconferencing Unit                      | Technology   | Low            | Regular Air      | 24.00          | -14,141.00   |
| Laurel Workman     | Polycom ViewStation™ ISDN Videoconferencing Unit                      | Technology   | Medium         | Regular Air      | 24.00          | -12,558.00   |
| Adrian Barton      | Polycom ViewStation™ ISDN Videoconferencing Unit                      | Technology   | Not Specified  | Regular Air      | 24.00          | -11,984.00   |
| Maxwell Schwartz   | Canon imageCLASS 2200 Advanced Copier                                 | Technology   | High           | Regular Air      | 24.00          | -11,861.00   |
| Nathan Mautz       | Canon imageCLASS 2200 Advanced Copier                                 | Technology   | Medium         | Express Air      | 24.00          | -11,769.00   |
| Julia West         | Riverside Palais Royal Lawyers Bookcase, Royale Cherry Finish         | Furniture    | Critical       | Delivery Truck   | 45.00          | -11,054.00   |
| Roger Demir        | Polycom ViewStation™ ISDN Videoconferencing Unit                      | Technology   | Not Specified  | Regular Air      | 24.00          | -10,264.00   |
| Julia Barnett      | Riverside Palais Royal Lawyers Bookcase, Royale Cherry Finish         | Furniture    | Not Specified  | Delivery Truck   | 45.00          | -9,612.00    |
| Cyra Reiten        | Canon imageCLASS 2200 Advanced Copier                                 | Technology   | Not Specified  | Regular Air      | 24.00          | -9,079.00    |
| Irene Maddox       | Okidata Pacemark 4410N Wide Format Dot Matrix Printer                 | Technology   | High           | Delivery Truck   | 9.00           | -8,570.00    |

#### Above is the table containing the bottom 10 customers.
#### Looking at the bottom 10 customers by total profit, they all show negative profits, meaning the company is losing money on these transactions.
### ADVICE TO THE MANAGEMENT:
#### The company should urgently evaluate the pricing, shipping strategy, and customer profitability. High losses from low-priority customers using expensive shipping methods show inefficiencies. Adjusting the shipping mode, reevaluating product margins, and possibly restructuring customer agreements can help turn losses into profits.



- ### If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one, do you think the company appropriately spent shipping costs based on the Order Priority? Explain your answer
### MY VIEW:
#### Based on my deep analysis, it a NO because The company appears to be mismanaging its shipping strategy, spending more on low-priority orders while underinvesting in urgent ones. This imbalance, along with recurring losses, points to an urgent need to realign logistics with order priority and improve cost control.




