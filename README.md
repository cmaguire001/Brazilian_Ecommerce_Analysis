# Brazilian E-Commerce Analysis

## Overview

This project analyzes the **Brazilian E-Commerce Public Dataset (Olist)** from Kaggle to explore customer behavior, orders, and payments. The analysis is performed in **Python (Pandas) and SQL** within a Jupyter Notebook/Google Colab environment. Gpt-prompted the questions and I wrote my own code, struggling through each line to learn as I go. 

Kaggle dataset link: [Olist Brazilian E-Commerce Public Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

The goal is to demonstrate **basic data analyst skills** including data exploration, joins, aggregations, and business metric calculations.

---

## Key Questions

* How many customers and orders exist?
* What is the **average order value (AOV)**?
* How often do customers place multiple orders?
* How do payments relate to orders and customers?

---

## Dataset

The project uses the **Olist Brazilian E-Commerce Dataset**, which includes:

* `customers`
* `orders`
* `order_items`
* `payments`
* `products`
* `sellers`

Tables are joined using primary and foreign keys like `order_id` and `customer_id`.

---

## Tools & Technologies

* Python
* Pandas
* SQL (via Pandas)
* Google Colab / Jupyter Notebook

---

## Example Metrics

* Total orders
* Total customers
* Total payment value
* Average Order Value (AOV)
* Customer order frequency

Example query from the notebook:

```sql
SELECT SUM(payment_value) / COUNT(DISTINCT order_id) AS AOV
FROM payments;
```
## Skills Demonstrated

* SQL joins (INNER, LEFT)
* Aggregations with `COUNT`, `SUM`, `GROUP BY`
* Calculating business metrics like AOV
* Translating business questions into queries
---
## Key Insights from Brazilian E-Commerce Analysis

  * Customer Base & Orders
    
  There are tens of thousands of customers, with multiple orders per customer in some cases.
  A significant portion of customers place only one order, indicating a potential for improving retention and repeat purchases.
  * Average Order Value (AOV)
    
  The overall AOV is approximately 160.99 BRL.
  Most orders fall within a similar range, showing consistent purchasing behavior.
  * Payments Analysis
    
  Multiple payment methods are used, with some orders using split payments.
  The sum of payments aligns with total orders, indicating that most payments are captured correctly.
  * Order Frequency
    
  Repeat customers exist but are relatively low compared to first-time buyers.
  Highlighting opportunities for customer engagement strategies to increase repeat purchases.

## PROJECT EXTENSION 
Olist Brazilian E-commerce Customer Heat Map 

This project visualizes customer distribution across Brazil using Olist’s customer and geolocation datasets. The goal is to create an interactive heat map / bubble map showing where the most customers are located, while efficiently handling large, high-cardinality data in Tableau Public.

## Project Overview

Datasets used:

olist_customers_dataset.csv

olist_geolocation_dataset.csv


## Objective:
Visualize the concentration of customers by city across Brazil, highlighting the largest customer bases while keeping the visualization performant.

## Tools:

Tableau Pubic 


## Steps to Build the Heat Map

1. Load and Relate the Data

Created a relationship between the customers and geolocations tables using customer_id.

Avoided joins at the raw row level to prevent Tableau from exploding the number of rows.


2. Use Generated Latitude and Longitude

Used Tableau’s generated Lat/Lng fields for mapping instead of raw CSV columns.

This ensures compatibility with Tableau’s optimized geography engine.


3. Aggregate Customers per City

Created a calculated field for number of customers per city:

COUNT([customer_unique_id])

Avoided COUNTD or LODs for filtering to prevent memory errors.


4. Filter and Limit Data

Applied Top N city filter:

Dragged customer_city → Filters → Top → By field → Top 200 by COUNT(customer_unique_id).


Optional: added customer_state as a context filter to further reduce memory usage.


5. Build the Map

Rows: Longitude (generated)

Columns: Latitude (generated)

Marks (Circle):

Size → COUNT([customer_unique_id])

Color → COUNT([customer_unique_id])

Detail → customer_city

7. Final Optimizations

Removed unnecessary customer_city from Detail for memory efficiency.

Verified bubble sizes matched customer counts.

Optional: created color gradients to represent customer density visually.

---

## Key Learnings / Takeaways

High-cardinality geospatial data can easily exceed Tableau Public memory limits.

Use Top N filters, context filters, and aggregates at the city level to optimize performance.

Table calculations are ideal for conditional labels without increasing memory footprint.

Tableau Public’s geography engine is optimized when using generated Lat/Lng rather than raw CSV columns.

---

## Screenshot of Map in images.

link to tableau public
   https://public.tableau.com/shared/7RBSX3Y69?:display_count=n&:origin=viz_share_link
  
## Repository Structure

```
Brazilian_Ecommerce_Analysis/
│
├── Brazilian_Ecommerce_Analysis.ipynb
├── README.md
```
## Author

**Christopher Maguire**
Aspiring Data Analyst | SQL • Analytics

---

