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
### **Sales trend overtime:**
- To analyze yearly sales trends, use the following SQL query:
  ```sql
  SELECT EXTRACT(Year FROM orderdate) AS Year,
       ROUND(CAST(SUM(unitprice * quantity) AS numeric), 2) AS "Year Sales"
  FROM orders
  JOIN order_details USING (orderid)
  GROUP BY Year
  ORDER BY Year;
This query extracts the year from the `orderdate`, calculates the total sales for each year, and rounds the result to two decimal places. The **CAST** function was used to change the 'quantity' data type, so that the 'round' function can be applied on it.

- To analyze monthly sales trends, use the following SQL query:
  ```sql
  SELECT TO_CHAR (orderdate, 'Month') AS Month,
       ROUND(CAST(SUM(unitprice * quantity) AS numeric), 2) AS "Monthly Sales"
  FROM orders
  JOIN order_details USING (orderid)
  GROUP BY Month
  ORDER BY Month;

### **Best and Worst selling products:**
- Best Selling product
  ```sql
  SELECT products.productid, productname, ROUND (CAST(SUM (od.unitprice*quantity)AS numeric), 2) AS "Quantity Sold" 
	FROM products 
	JOIN order_details od USING (productid)
	GROUP BY products.productid, productname
	ORDER BY ROUND (CAST(SUM (od.unitprice*quantity)AS numeric), 2) DESC
	LIMIT 1;

- Worst Selling product
  ```sql
  SELECT products.productid, productname, ROUND (CAST(SUM (od.unitprice*quantity) AS numeric),2) AS "Quantity Sold" 
	FROM products 
	JOIN order_details od USING (productid)
	GROUP BY products.productid, productname
	ORDER BY ROUND (CAST(SUM (od.unitprice*quantity) AS numeric),2) 
	LIMIT 1; 
  
### **Key Customers:**
```sql
SELECT companyname KeyCustomers, ROUND (CAST (SUM (od.unitprice*quantity) AS numeric), 2) AS "Orders"
	FROM customers
	JOIN orders USING (customerid)
	JOIN order_details od
	USING (orderid)
	GROUP BY KeyCustomers
	ORDER BY ROUND (CAST (SUM (od.unitprice*quantity) AS numeric), 2) DESC
```

### **Shipping costs analysis:**
- To analyse the shipping costs among the different providers, use this sql query:
  ```sql
  SELECT shippers.companyname AS "Shipping Provider", 
       SUM(freight) AS "Avg Shipping Cost", 
       COUNT(orderid) AS "Total Shipments"
	FROM orders
	JOIN shippers ON orders.shipvia = shippers.shipperid
	GROUP BY shippers.companyname
	ORDER BY AVG(freight) DESC;
  ```
## **Insights and Recommendations**
  1. Sales Trends Over Time
- **Insights:** The yearly sales trend shows steady growth, with a noticeable increase in revenue over the years. Seasonal spikes in sales are observed during holiday periods, indicating higher demand during specific times of the year.
- **Recommendations:**  Plan marketing campaigns and promotions during peak seasons (e.g., holidays) to maximize sales.
- Ensure sufficient stock levels during high-demand periods to avoid stockouts and meet customer expectations.
- Continue focusing on strategies that drive consistent yearly growth, such as expanding product offerings or entering new markets.

 2. Best and Worst Selling Products
- **Insights:** Product X generates the highest revenue, indicating strong customer demand, while product Y has minimal sales, suggesting low customer interest or potential issues with pricing, quality, or marketing.
- **Recommendations:** Highlight Product X in marketing campaigns and bundle it with complementary products to drive further sales.
- Investigate why Product Y is underperforming. Consider revising its pricing, improving quality, or discontinuing it if it’s no longer viable.
- Regularly review the product portfolio to identify high-performing and underperforming products, ensuring resources are allocated effectively.

 3. Key Customers
- **Insights:** A small group of customers contributes significantly to total sales, indicating strong relationships with high-value clients. The top customer, Company A, accounts for a large portion of revenue.
- **Recommendations:** Offer personalized services, loyalty programs, or exclusive discounts to retain high-value customers.
- Analyze customer data to identify potential high-value customers and develop targeted strategies to nurture these relationships.
- Segment customers based on their purchasing behavior and tailor marketing efforts to each segment for better engagement.

 4. Shipping Costs Analysis
- **Insights:** Shipping costs vary significantly across providers, with Provider A being the most expensive on average.
- Some providers offer lower costs but may have longer delivery times or other trade-offs.
- **Recommendations:** Evaluate the cost-effectiveness and reliability of shipping providers. Consider switching to more cost-efficient providers without compromising delivery quality.
- Negotiate better rates with current providers or explore bulk shipping discounts to reduce costs.
- Regularly review shipping performance metrics (e.g., delivery times, customer satisfaction) to ensure a balance between cost and service quality.

