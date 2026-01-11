# Brazilian E-Commerce Analysis

## Overview

This project analyzes the **Brazilian E-Commerce Public Dataset (Olist)** from Kaggle to explore customer behavior, orders, and payments. The analysis is performed in **Python (Pandas) and SQL** within a Jupyter Notebook/Google Colab environment. In Phase 1 Ai helped prompt the questions and I wrote the SQL code, struggling through each line to learn as I go. 

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

This project visualizes customer distribution across Brazil using Olist’s customer and geolocation datasets. The goal is to create an interactive heat map / bubble map showing where the most customers are located, while efficiently handling large, high-cardinality data in Tableau Public. I used Ai-Assitance to help guide me through this process.

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
## Project Extension part 2

Google colab notebook keep crashing due to file storage issues.
Colab does not save the kaggle CSVs permentanly so I had to keep uploading them.(very ineffective) 
I asked GPT for a better method to run SQL and store the CSV and I discovered Codespaces within Github.
I used GitHub Codespaces to write and run the code, saving all the CSVs I downloaded from Kaggle directly in my repository.

First, I installed DuckDB in Python, which let me run SQL queries directly on the CSV files without needing a heavy database. I (Ai-assisted) wrote a script to load all the CSVs — including orders, customers, order items, and payments — into DuckDB tables. This made the data easier to work with and allowed me to check that all rows were loaded correctly.

Next, I combined these tables into a single fact table called fct_orders. I calculated the total revenue for each order, brought in customer information, added payment details, and created a flag to identify repeat customers. This table became the foundation for all my analysis.

Once the fact table was ready, I wrote scripts to generate key metrics for visualization. I exported monthly revenue, revenue from repeat vs new customers, and revenue by state into separate CSV files. These files were ready to be used in Tableau for creating dashboards.

### Project extension Part 3 : Live dashboard Setup 

Live Dashboard (PostgreSQL + Metabase)
Overview

This project demonstrates how to build a live analytics dashboard using a real database and SQL — without exporting CSV files.
The dashboard updates automatically whenever the underlying data changes.

Tools Used

PostgreSQL (Neon, free tier) – stores the data

Metabase (self-hosted via Docker) – dashboards and charts

SQL – data aggregation and business logic

All tools are free and open-source.

The goal is to simulate how a junior analyst would support business reporting in a real company.

How It Works (High Level)

Data is stored in a PostgreSQL database

SQL queries calculate metrics like totals and averages

Metabase connects directly to the database

Dashboards update live as data changes

No manual exports or refreshes required.

Why This Matters

Uses production-style tools (Postgres + BI layer)

Demonstrates real SQL skills (joins, grouping, filtering)

Mirrors how analytics teams work in practice

Skills Demonstrated

Data modeling

Building live dashboards

Translating raw data into business insights

# Metabase + Neon Database Setup

A quick guide for setting up Metabase dashboards connected to a Neon PostgreSQL database on Chrome OS Linux.

## What I Built

- **Metabase** running in Docker for data visualization and dashboards
- **Neon PostgreSQL** database for cloud-hosted data storage
- **ngrok tunnel** to share dashboards publicly

## Prerequisites

- Chrome OS with Linux (Penguin) enabled
- Docker installed
- Neon account with a database created

## Setup Steps

### 1. Install Docker and PostgreSQL Client

```bash
sudo apt update
sudo apt install docker.io postgresql-client -y
sudo systemctl start docker
sudo systemctl enable docker
```

### 2. Fix Docker Permissions

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
sudo chmod 666 /var/run/docker.sock
```

### 3. Run Metabase

```bash
docker run -d -p 3000:3000 --name metabase metabase/metabase
```

Access locally at: `http://penguin.linux.test:3000`

### 4. Connect to Neon Database

Get your connection string from Neon Console, which looks like:
```
postgresql://username:password@host.neon.tech/dbname?sslmode=require
```

In Metabase setup, configure PostgreSQL connection with:
- **Host**: Your Neon endpoint (e.g., `ep-xxx.us-east-2.aws.neon.tech`)
- **Port**: `5432`
- **Database**: Your database name
- **Username**: From connection string
- **Password**: From connection string
- **SSL**: Enabled

### 5. Add Sample Data

Connect via psql:
```bash
psql 'your-neon-connection-string-here'
```

Create a test table:
```sql
CREATE TABLE sales (
    id SERIAL PRIMARY KEY,
    date DATE,
    product VARCHAR(100),
    amount DECIMAL(10,2),
    region VARCHAR(50)
);

INSERT INTO sales (date, product, amount, region) VALUES
('2024-01-15', 'Widget A', 1250.00, 'North'),
('2024-01-16', 'Widget B', 890.50, 'South'),
('2024-01-17', 'Widget A', 2100.00, 'East'),
('2024-01-18', 'Widget C', 1500.75, 'West'),
('2024-01-19', 'Widget B', 3200.00, 'North');
```

### 6. Share Dashboards Publicly with ngrok

Install ngrok from https://ngrok.com and authenticate, then:

```bash
ngrok http 3000
```

Share the generated `https://` URL. Others can access your dashboard through this public link.

## Usage

- **Create dashboards**: Click "+ New" → "Question" in Metabase
- **Share publicly**: Use the ngrok URL instead of localhost
- **Keep ngrok running**: Don't close the terminal while sharing

## Useful Commands

```bash
# Check running containers
docker ps

# View Metabase logs
docker logs metabase

# Stop Metabase
docker stop metabase

# Restart Metabase
docker start metabase

# Stop ngrok
# Press Ctrl+C in the ngrok terminal
```

## Notes

- ngrok URLs change on each restart (free plan)
- Keep the ngrok terminal open while sharing
- Docker permissions reset after Linux container restart (re-run `chmod` if needed)

## Troubleshooting

**Can't access Metabase?**
- Use `penguin.linux.test:3000` instead of `localhost:3000`
- Check if container is running: `docker ps`

**Permission denied for Docker?**
- Run: `sudo chmod 666 /var/run/docker.sock`

**Neon connection fails?**
- Verify SSL is enabled in Metabase
- Double-check connection string details

# Auto-Updating Dashboard

## What This Does

Creates a live dashboard that automatically updates with new sales data every 5 minutes. Stakeholders can view it through a shared link without needing any software or accounts.

## How It Works

1. **Data Storage**: Sales data lives in a Neon cloud database
2. **Visualization**: Metabase creates charts and graphs from the data
3. **Auto-Updates**: A script adds new sales records every 5 minutes
4. **Sharing**: ngrok creates a public link anyone can access

## Accessing the Dashboard

Share this link with stakeholders:
```
https://overapprehensively-unremissive-arlo.ngrok-free.dev/public/question/01c829d4-b98a-4d77-bd5b-3175990187d0
```

They can bookmark it and refresh anytime to see the latest data.

## How to Keep It Running

- **Keep the terminal with ngrok open** - closing it breaks the link
- **Restart ngrok if needed** - if you restart, send the new link to stakeholders
- The auto-update script runs in the background automatically

## Adding Data Manually

If you want to add specific data (not just automatic updates):

1. Open terminal
2. Connect to database: `psql 'your-connection-string'`
3. Add records: `INSERT INTO sales (date, product, amount, region) VALUES ('2024-01-26', 'Widget A', 1500.00, 'North');`

The dashboard will reflect changes within 1-2 minutes, or refresh the page to see immediately.

check out the Monthly Revenue dashboard from the Olist ecommerce data :   https://overapprehensively-unremissive-arlo.ngrok-free.dev/public/question/66068a45-6122-4c48-a727-52d463722c45      click visit site to enter
follow the free and fragile pipeline  [Auto Script on home PC linux ] → [Neon PostgreSQL] → [Metabase (Docker)] → [ngrok] → [Live dashoard! ]

## Making It Permanent

Current setup is free but requires:
- Keeping your computer on
- Sending new links when ngrok restarts

For a permanent solution, consider:
- **Railway** ($5/month) - dashboard stays online 24/7 with permanent link
- **ngrok paid** ($8/month) - keeps your current setup but with permanent link

## Troubleshooting

**Stakeholders can't access the link?**
- Check if ngrok terminal is still open
- Send them the current ngrok URL

**Dashboard not updating?**
- Refresh the page
- Check if auto-update script is running: `./insert_sales.sh`

**Need help?**
- Contact: cmaguire001@gmail.com



Notes

This project was built on a Chromebook using a Linux container and Docker, demonstrating a fully free and portable analytics setup.



## Author

**Christopher Maguire**
Aspiring Data Analyst | SQL • Analytics

---

