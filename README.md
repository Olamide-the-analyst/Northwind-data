# Northwind Data Analysis 
This repository contains SQL queries and analysis performed on the Northwind Database, a sample database provided by Maven Analytics. The Northwind database represents a fictional company called Northwind Traders, which imports and exports specialty foods from around the world. This dataset is widely used for learning and practicing SQL, data analysis, and business intelligence.

## **Table of Content**
1. Project overview
2. Analysis objectives
3. SQL queries
4. Insights and recommendations
5. How to use this repository

## **Project Overview**
The Northwind database represents Northwind Traders, a global specialty foods distributor that sources high-quality, unique food products from suppliers worldwide and sells them to restaurants, cafes, and retailers. The company operates in multiple regions, including North America, Europe, and Asia, and serves a diverse customer base ranging from small businesses to large enterprises. Northwind Traders focuses on building long-term relationships with customers and suppliers, offering personalized service and maintaining a reputation for quality and reliability. The company manages its operations through efficient product sourcing, order fulfillment, and logistics, ensuring timely delivery of goods to its customers.

## **Analysis Objectives**
The goal of this project is to analyze the Northwind database to uncover actionable insights that can help the company improve its operations, customer relationships, and profitability. Key questions addressed in this analysis include:
- **Sales Trends:** How have sales performed over time? Are there seasonal patterns or trends?
- **Product Performance:** Which products are the best and worst sellers? How can product offerings be optimized?
- **Customer Insights:** Who are Northwind's key customers? How can the company strengthen relationships with high-value customers?
- **Shipping Costs:** Are shipping costs consistent across providers? How can logistics be optimized to reduce costs?

## **SQL Queries**
- **Sales trend overtime **
  'sql'
  SELECT EXTRACT(Year FROM orderdate) AS Year,
       ROUND(CAST(SUM(unitprice * quantity) AS numeric), 2) AS "Year Sales Trend"
FROM orders
JOIN order_details USING (orderid)
GROUP BY Year
ORDER BY Year;

