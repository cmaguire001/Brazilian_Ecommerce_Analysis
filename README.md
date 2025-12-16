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

