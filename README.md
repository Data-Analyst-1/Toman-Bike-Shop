## Toman Bike Shop

### Project Overview 

A bike shop analysis project looking into metrics such as the total number of riders, total revenue, total profit, and profit margin.
Toman Bike Shop

### Data Sources 
The primary data source were two csv files, bike share year 1, and bike share year 2.

### Tools
- MYSQL 
- Power BI 

### Data Cleaning and Preparation
In the initial stages of data cleaning and preparation, the following tasks were performed:
- Database creation in MySQL
- Data loading and inspection in MySQL
- Handling missing values 
- Data transformation 

### Exploratory Data Analysis
These questions were explored in detail:
1. The total revenue, profit, and profit margin.
2. The sum of riders.
3. Hourly and seasonal revenue distribution.
4. Rider demographics.

```sql

with all_years as (
select * 
from bike_share_yr_0
union all
select *
from bike_share_yr_1)

select distinct month(try_cast(dteday as date)) as month_number, 
       season, 
	   a.yr, 
	   weekday, 
	   hr, 
	   rider_type, 
	   riders, 
	   price, 
	   COGS,
       riders*price as revenue, 
	   riders*price - COGS as profit
from all_years as a
left join cost_table as b
on a.yr = b.yr
where month(try_cast(dteday as date)) is not null;


SELECT TOP 5 * FROM sales;

SELECT FORMAT(CAST(Date as DATE), 'MMM') AS Month, SUM(GrossIncome) AS revenue
FROM sales
GROUP BY FORMAT(CAST(Date as DATE), 'MMM');


SELECT TOP 100 * FROM sales;
SELECT Gender, SUM(CAST(TotalCost AS FLOAT)) AS total_cost
FROM sales 
GROUP BY Gender 
ORDER BY total_cost DESC;


SELECT Gender, SUM(TRY_CAST(TotalCost AS FLOAT)) AS total_cost
FROM sales 
WHERE ISNUMERIC(YourColumn) = 1
GROUP BY Gender 
ORDER BY total_cost DESC;

SELECT Gender,
   SUM(CASE 
        WHEN ISNUMERIC(TotalCost) = 1 THEN TRY_CAST(TotalCost AS FLOAT)
        ELSE NULL 
    END) AS Total_Cost
FROM sales
WHERE TotalCost IS NOT NULL AND LTRIM(RTRIM(TotalCost)) != ''
GROUP BY Gender;

SELECT Gender, ROUND(SUM(GrossIncome),2) AS total_income
FROM sales 
GROUP BY Gender;

SELECT City, ROUND(SUM(GrossIncome),2) AS income_by_city
FROM sales 
GROUP BY City 
ORDER BY sales_by_city DESC;
```

### Data Analysis Results
- The Bike Shop had a total revenue of $15M, a profit of $10M, and a total of 3 million riders.
- 81% of the riders were registered while 19% were casual.
- The shop made the most profits in the third quarter and the least in the first quarter.
- A display of hourly sales data across the week with higher earnings in midday and early evening hours, particularly around 10 to 15 hours, suggesting these are the most profitable times.
- Overall, 2022 performed better compared to 2021 in terms of revenue, profit, and the profit margin.


![Bike share](https://github.com/user-attachments/assets/dc5eabad-270d-45f6-9d2b-f13390861a90)


### Recommendation
Maximize the season and hours during the riders are most busy, which was the third season, and 10 to 15 hours respectively. 



