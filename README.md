# Superstore-Sales-Analysis
An interactive Superstore Sales Analysis project built using Power BI to analyze sales, profit, product performance, customer segments, and shipping operations.
Project Overview

# This project analyzes Superstore sales data using Microsoft Power BI to understand sales performance, profitability, product trends, customer segments, and shipping operations.
*1.Total sales by region.
    
    SELECT 
    region, sum(sales)
    FROM superstore_db.superstore
    group by region;

*2.Top 5 profitable category

    select 
      category, 
      sum(profit) as Total_profit
     from superstore 
     group by category
     order by Total_profit desc
     limit 5;

*3.Monthly sales trend.

    SELECT
    DATE_FORMAT(order_date, '%b') AS month_name,
    SUM(sales) AS total_sales
    FROM superstore
    GROUP BY MONTH(order_date), DATE_FORMAT(order_date, '%b')
    ORDER BY MONTH(order_date);

*4.Highest discount impact.

    Select 
    discount , round(Avg(profit),2)
    from superstore 
    Group by discount;

*5.Which 10 sub-categories generate the highest profit.

    Select 
    sub_category,
    Round(sum(profit),2) as Total_profit
    from superstore
    group by sub_category
    order by Total_profit desc
    limit 10;

*6.TOP 10 product name by sales.

    SELECT
    product_name,
    SUM(sales) AS total_sales
    FROM superstore
    GROUP BY product_name
    ORDER BY total_sales DESC
    LIMIT 10;

*7.Which region generates the highest sales and profit?

    SELECT
    region,
    SUM(sales) AS total_sales,
    SUM(profit) AS total_profit
    FROM superstore
    GROUP BY region
    ORDER BY total_sales DESC;

*8.Which products are generating a loss?

    SELECT
    product_name,
    SUM(sales) AS total_sales,
    SUM(profit) AS total_profit
    FROM superstore
    GROUP BY product_name
    HAVING SUM(profit) < 0
    ORDER BY total_profit ASC
    LIMIT 10;

*9.Which shipping mode has the shortest average shipping time.

    SELECT
    ship_mode,
    ROUND(AVG(DATEDIFF(ship_date, order_date)), 2)
        AS avg_shipping_days
    FROM superstore
    GROUP BY ship_mode
    ORDER BY avg_shipping_days;

*10.Which 3 products have the highest sales within each category?

    WITH product_sales AS (
    SELECT
        category,
        product_name,
        SUM(sales) AS total_sales,
        DENSE_RANK() OVER (
            PARTITION BY category
            ORDER BY SUM(sales) DESC
        ) AS product_rank
        FROM superstore
    GROUP BY category, product_name
    )
    SELECT
    category,
    product_name,
    total_sales,
    product_rank
    FROM product_sales
    WHERE product_rank <= 3
    ORDER BY category, product_rank;

*11.Who are the top 10 customers by sales?

    SELECT
    customer_name,
    SUM(sales) AS total_sales,
    SUM(profit) AS total_profit
    FROM superstore
    GROUP BY customer_id, customer_name
    ORDER BY total_sales DESC
    LIMIT 10;
