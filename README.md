# learndatalake

This repo contains a library of notebooks to teach the basics of the bronze, silver, gold, data engineering pattern.
# 🚀 Databricks Free Edition: Zero-to-Hero (4-Week Training)

This repository contains a structured, 4-week roadmap to master the **Databricks Free Edition**. We focus on building confidence using the new **Serverless** architecture and the built-in `samples` catalog.

## 🛠 Prerequisites
* **Account:** [Databricks Free Edition](https://www.databricks.com/learn/free-edition).
* **Compute:** Ensure your notebook is attached to **Serverless** (green dot in the top-right corner).
* **Data:** We utilize the `samples` catalog (standard in Free Edition) to avoid manual file uploads.

---

## 📅 Weekly Curriculum

### 📊 Week 1: The Modern Data Analyst (SQL & Discovery)
**Goal:** Navigate the UI and perform exploratory data analysis.
* **Key Concept:** Data Discovery using the **Catalog Explorer**.
* **Dataset:** `samples.nyctaxi.trips`
* **Tasks:**
    1.  Explore the sidebar: Locate **Workspace**, **Catalog**, and **Dashboards**.
    2.  Create a new SQL Notebook and run:
        ```sql
        SELECT * FROM samples.nyctaxi.trips LIMIT 100;
        ```
    3.  **Visualization:** Use the `+` button in the result cell to create a "Bar Chart" showing `fare_amount` by `pickup_zip`.
    4.  **Filter Logic:** Write a query to find the top 5 busiest drop-off locations.

### 📈 Week 2: AI-Assisted Analytics & Dashboards
**Goal:** Use Databricks Assistant and build reporting layers.
* **Key Concept:** Using **Genie/Assistant** to accelerate development.
* **Dataset:** `samples.tpch.customer` and `samples.tpch.orders`
* **Tasks:**
    1.  Join the Customer and Orders tables to calculate total spend per market segment.
    2.  **Assistant Prompting:** Highlight your code and use the Assistant (the ✨ icon) to "Optimize this query" or "Fix errors."
    3.  **Lakehouse Dashboards:** Create a new Dashboard and pin your notebook visualizations to it to create a live report.

### ⚙️ Week 3: Data Engineering Patterns (The Lakehouse)
**Goal:** Transition from querying to building data pipelines.
* **Key Concept:** The **Medallion Architecture** (Bronze ➡️ Silver).
* **Tasks:**
    1.  **Schema Setup:** Create your own playground database:
        ```sql
        CREATE SCHEMA IF NOT EXISTS training_ground;
        ```
    2.  **Silver Layer:** Create a "cleaned" table from the samples:
        ```sql
        CREATE TABLE training_ground.cleaned_taxi AS
        SELECT * FROM samples.nyctaxi.trips 
        WHERE trip_distance > 0 AND fare_amount > 0;
        ```
    3.  **Delta Time Travel:** Update a row, then use `VERSION AS OF` to see the data before the change.

### 🤖 Week 4: Productionalizing with PySpark & Workflows
**Goal:** Automation and scripting logic.
* **Key Concept:** Converting SQL logic to **PySpark** and scheduling jobs.
* **Tasks:**
    1.  **PySpark Basics:** Open a Python cell and load a table into a DataFrame:
        ```python
        df = spark.table("samples.nyctaxi.trips")
        display(df.groupBy("payment_type").avg("fare_amount"))
        ```
    2.  **Workflows:** Navigate to **Jobs & Pipelines** and create a new Job that runs your Week 3 cleaning notebook once a day.
    3.  **Collaboration:** Use the **Share** button to practice notebook co-authoring.

---

## 📂 Useful Discovery Commands
Paste these into a notebook to see what’s available in your environment:

```sql
-- See available data catalogs
SHOW CATALOGS;

-- Explore the NYC Taxi sample data
SHOW TABLES IN samples.nyctaxi;

-- List underlying sample files
-- (In Free Edition, use %python)
%python
display(dbutils.fs.ls("/databricks-datasets/"))
