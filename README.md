
SELECT TOP (1000) [transactions_id]
      ,[sale_date]
      ,[sale_time]
      ,[customer_id]
      ,[gender]
      ,[age]
      ,[category]
      ,[quantiy]
      ,[price_per_unit]
      ,[cogs]
      ,[total_sale]
  FROM [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]
      select
      count(*)
      from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]

   Select * from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]
   where transactions_id is null

   Select * from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]
   where sale_date is null

   Select * from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]
   where sale_time is null
   -- Data cleaning
   Select * from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]
   where 
           transactions_id is null
           or
           sale_date is null
           or
           sale_time is null
           or
           gender is null
           or 
           category is null
           or
           quantiy is null
           or
           cogs is null
           or
           total_sale is null ;
-- 
Delete from  [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]
        where 
           transactions_id is null
           or
           sale_date is null
           or
           sale_time is null
           or
           gender is null
           or 
           category is null
           or
           quantiy is null
           or
           cogs is null
           or
           total_sale is null ;
-- Data Exploration
-- How many sales we have?
select count(*) as total_sale from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]

-- How many unique customers we have?
select count( DISTINCT customer_id) as total_sale from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]
select  DISTINCT category as retail_sales from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]

--Data Analysis & Business Key Problem & Analysis
--Q.1 Write a SQL query to retrive all colums for sales made on '2022-11-05'

select *
from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]
where sale_date = '2022-11-05'

--Q.2 write a SQL query to retrive all transactions where the category is 'clothing' and the quantity sold is more than 10 in the month of Nov-2022


   select * 
from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]
where category='Clothing'
  AND
  quantiy>=4
  AND
  YEAR(sale_date)=2022
  AND
  MONTH(sale_date)=11;


  --Q.3 Write  a SQL query to calculate the total sales for each category
  select 
      category,
sum(total_sale) as net_sale

  from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]
  group by category;


  --Q.4 Write a SQL query to find the average age of customers who purchased items from the 'beauty'category.
  select
     AVG(age) as avg_age
from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]
where category='Beauty';


--Q.5 Write a SQL query to find all transations where the total_sale is greater than 1000.
select * from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]
where total_sale >1000

Q.6 Write a SQL query to find the total number of transaction (transaction_id) made by each ----gender in each category.
        select 
             category,
             gender ,
             count(*) as total_trans
        from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]
        group by category,gender ;

--Q.7 Write a SQL query to calculate the average sale for each month. find out best selling month in each year
with MonthlySales As(
select
  Year(sale_date) as [year ],
   month(sale_date) as [Month],
   avg(total_sale) as avg_total_sale
   
from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]
group by Year(sale_date),month(sale_date) 
)
select 
     [year ],
     [Month],
     avg_total_sale ,
     RANK() over (partition by[year] order by avg_total_sale desc)as[ rank]
   
   from MonthlySales
   order by [year ] Desc,[ rank]  Asc;




   --Q.8 Write a SQL query the top 5 customers based on the highest total sales
   select 
      customer_id,
      sum(total_sale) as total_sales
   
   from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]
   group by customer_id
   order by  total_sales desc


   --Q.9 Write a SQL query to find the number of unique customers who purchased items from each category
   select 
      category,
      count(distinct(customer_id)) as cnt_unique_cs
   
   from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ]
   group by category ;
   

   --Q.10 Write a SQL query to create each shift and number of orders(Example Morning <=12,Afternoon between 12&17,evening>17)
   with hourly_sale
   as (
   select *,
       case
           when datepart(hour,sale_time) <12 then 'Morning'
           when datepart(hour,sale_time) between 12 and 17 then 'Afternoon'
           else 'Evening'
           end as shift
   from [sql_P1].[dbo].[SQL - Retail Sales Analysis_utf ])
   select 
      shift,
      count(*) as total_orders
from hourly_sale
group by shift


# Retail Sales Analysis SQL Project

## Project Overview
- **Project Title:** Retail Sales Analysis
- **Level:** Beginner
- **Database:** sql_P1

This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze retail sales data. The project involves setting up a retail sales database, performing Exploratory Data Analysis (EDA), and answering specific business questions through SQL queries.

## Objectives
1. **Set up a retail sales database:** Create and populate a retail sales database with the provided sales data.
2. **Data Cleaning:** Identify and remove any records with missing or null values.
3. **Exploratory Data Analysis (EDA):** Perform basic exploratory data analysis to understand the dataset.
4. **Business Analysis:** Use SQL to answer specific business questions and derive insights from the sales data.

## Project Structure
- **Database Setup:** Creating the database and tables.
- **Data Exploration & Cleaning:** Running queries to check row counts, null values, and basic metrics.
- **Data Analysis & Findings:** Answering business questions (such as top customers, sales by category, monthly averages, etc.).

## Reports
- **Sales Summary:** A detailed report summarizing total sales, customer demographics, and category performances.
- **Trend Analysis:** Insights into sales trends across different months and shifts.
- **Customer Insights:** Reports on top customers and unique customer counts per category.

## Conclusion
This project serves as a comprehensive introduction to SQL for data analysts, covering database setup, data cleaning, exploratory data analysis, and business-driven SQL queries. The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.

## How to Use
1. **Clone the Repository:** Clone this project repository from GitHub.
2. **Set Up the Database:** Run the SQL scripts provided in the database setup file to create and populate the database.
3. **Run the Queries:** Use the SQL queries provided in the analysis files to perform your analysis.
4. **Explore and Modify:** Feel free to modify the queries to explore different aspects of the dataset or answer additional business questions.

## Author - Rokaia Tamer
This project is part of my portfolio, showcasing the SQL skills essential for data analyst roles. If you have any questions, feedback, or would like to collaborate, feel free to connect with me on LinkedIn:

[LinkedIn Profile](https://www.linkedin.com/in/rokaia-tamer-a52904362?utm_source=share_via&utm_content=profile&utm_medium=member_android)
