# Sales Performance Analysis for a Telecommunication Company

## Project Overview
This project aims to provide insights into the sales performance of a telecommunication company over the past years. By analyzing various aspects of the sales data, we seek to identify customer behavior, product popularity, and revenue trends.


![SALES TREND OVER THE YEARS](https://github.com/promise-the-data-analsyt/Sales-Performance-Analysis-for-a-Telecommunication-Company/assets/169470196/8d27f9b4-2126-4bf8-b84d-3da517dbbe74)

### Tools

- Excel - Data Cleaning 
- PostgreSQL - Data Analysis
- PowerBI - Creating Reports

### Project Steps:
##### 1. Data Collection and Extraction
##### 2. Data Transformation
##### 3. Data Analysis
##### 4. Creating a Power BI Dashboard
##### 5. Report Presentation

### Data Analysis
```sql
SELECT a.name AS customers_name,
       SUM(o.smartphones_qty) ,
       SUM(o.smartwatches_qty),
       SUM(o.tablets_qty),
       COUNT(a.name) AS No_of_Transaction,
       SUM(o.total) AS total_quantity,
       SUM(o.total_amt_usd)AS total_revenue_usd
FROM accounts a
JOIN orders o
ON a.id = o.account_id
GROUP BY customers_name
ORDER BY total_revenue_usd  DESC
```

```sql
SELECT
 w.channel AS channel_name,
       COUNT(w.channel ) AS No_of_Transactions,
       SUM(total) AS total_quantity,
       SUM(total_amt_usd) AS total_revenue_usd
FROM  orders o
JOIN accounts a
ON o.account_id=a.id
JOIN web_events w
ON a.id=w.account_id
GROUP BY channel_name
ORDER BY total_revenue_usd DESC
```

```sql
SELECT r.name AS region_name,
       COUNT( r.name) AS  No_of_Transactions,
       SUM(o.total) AS total_quantity,
       SUM(o.total_amt_usd) AS total_revenue_usd
FROM orders o
JOIN accounts a
ON a.id = o.account_id
JOIN sales_reps s
ON a.sales_rep_id = s.id
JOIN region r
ON s.region_id = r.id
GROUP BY region_name
ORDER BY total_revenue_usd DESC
```

```sql
SELECT DATE_TRUNC ('year', occurred_at) AS year,
       COUNT(DATE_TRUNC ('year', occurred_at))  AS No_of_Transactions,
       SUM(total) AS total_quantity,  
       SUM (total_amt_usd) AS total_revenue_usd
FROM orders
GROUP BY year  
ORDER BY year
```

### Results

The analysis results are as follows:
1. The company's sales has been steadily increasing over the year with a noticeable peak in 2016.
2. In 2016 - 2017, there was a very sharp drop in sales throughtout the year.
3. The Northeast region recorded highest sales among other regions.
4. The Direct channel has the highest sales from other channels
5. Customers purchased more of smartphones than other two produts


### Recommendation

Based on the analysis, we recommend the following:
1. Focus on investing more on smartphones
2. Invest in marketing and promotion in other regions especially Midwest with poorest sales
3. Also invest in marketing and promotions on other channels
