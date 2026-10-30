# Superstore-Sales-Analysis
An interactive Superstore Sales Analysis project built using Power BI to analyze sales, profit, product performance, customer segments, and shipping operations.
Project Overview

# This project analyzes Superstore sales data using Microsoft Power BI to understand sales performance, profitability, product trends, customer segments, and shipping operations.
1.Total sales by region.
    '''SELECT 
    region, sum(sales)
    FROM superstore_db.superstore
    group by region;'''
