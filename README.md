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

# 🧪 Lab Instructions: Week 1 & 2 (Analyst Focus)

These labs are optimized for the **Databricks Free Edition**. We will use the **Serverless SQL Warehouse** and the **Samples** catalog.

---

## 📅 Week 1: Data Discovery & Navigation
**Objective:** Master the Databricks UI, the Catalog Explorer, and basic SQL visualizations.

### Lab 1.1: The "No-Code" Discovery
* **Task:** Navigate the Catalog Explorer.
* **Instructions:**
    1.  Click the **Catalog** icon in the sidebar.
    2.  Navigate to `samples` ➡️ `nyctaxi` ➡️ `trips`.
    3.  **Explore the Tabs:**
        * **Sample Data:** Preview the first 100 rows.
        * **Details:** Find the "Owner" and the underlying file format (Delta).
        * **Insights:** View common join patterns or frequent queries (if available).

### Lab 1.2: Your First SQL Analysis
* **Task:** Identify the most profitable taxi payment methods.
* **Instructions:**
    1.  Create a new SQL Notebook: `Week1_Taxi_Analysis`.
    2.  Run the following query in Cell 1:
        ```sql
        SELECT 
            payment_type, 
            COUNT(*) as total_trips,
            AVG(fare_amount) as avg_fare,
            AVG(tip_amount) as avg_tip
        FROM samples.nyctaxi.trips
        GROUP BY 1
        ORDER BY total_trips DESC;
        ```
    3.  **Visualization:** Click the **+** icon next to the "Results" tab ➡️ **Visualization**.
        * **Type:** Bar Chart
        * **X-Column:** `payment_type`
        * **Y-Column:** `avg_tip`
    4.  **Observation:** Is there a correlation between payment type (Credit Card vs Cash) and tip amount?

### Lab 1.3: Data Quality Profiling
* **Task:** Use SQL to find "dirty" data.
* **Instructions:**
    1.  Identify trips with impossible values (e.g., zero distance but high fare).
        ```sql
        SELECT * FROM samples.nyctaxi.trips 
        WHERE trip_distance <= 0 AND fare_amount > 0;
        ```
    2.  **Self-Correction:** How many rows would you "lose" if you filtered these out?

---

## 📅 Week 2: Advanced Analytics & AI Assistant
**Objective:** Leverage Databricks' built-in AI to handle complex logic and create interactive tools.

### Lab 2.1: Multi-Table Joins (The Retail Schema)
* **Task:** Analyze customer spending habits by market segment.
* **Instructions:**
    1.  Create a new SQL Notebook: `Week2_Retail_Intelligence`.
    2.  We will join the `customer` and `orders` tables from the `tpch` schema.
        ```sql
        SELECT 
            c.c_mktsegment,
            SUM(o.o_totalprice) AS total_revenue,
            COUNT(o.o_orderkey) AS order_count
        FROM samples.tpch.customer c
        JOIN samples.tpch.orders o ON c.c_custkey = o.o_custkey
        GROUP BY 1
        ORDER BY total_revenue DESC;
        ```

### Lab 2.2: Using the Databricks Assistant
* **Task:** Let AI solve a "Window Function" problem.
* **Instructions:**
    1.  In a new cell, click the **Assistant (✨)** icon or press `Cmd/Ctrl + I`.
    2.  **Prompt:** *"Using the samples.tpch.orders table, write a query to find the top 3 most expensive orders for every year."*
    3.  **Review & Run:** Examine how the Assistant uses `ROW_NUMBER()` or `RANK()`. This is a great way to learn advanced SQL syntax on the fly.

### Lab 2.3: Building Interactive Widgets
* **Task:** Create a dashboard-ready notebook with filters.
* **Instructions:**
    1.  Add a dropdown widget to the top of your notebook:
        ```sql
        CREATE WIDGET DROPDOWN select_segment DEFAULT 'BUILDING' CHOICES (SELECT DISTINCT c_mktsegment FROM samples.tpch.customer);
        ```
    2.  Reference that widget in your query:
        ```sql
        SELECT * FROM samples.tpch.customer 
        WHERE c_mktsegment = getArgument('select_segment');
        ```
    3.  Change the dropdown value at the top of the notebook and notice how the data refreshes without editing the code.

---

## ✅ Checkpoint: Week 2 Review
By now, you should be comfortable with:
* [ ] Navigating the **Catalog** to find tables.
* [ ] Creating **Visualizations** directly from SQL output.
* [ ] Using the **Assistant** to generate or fix complex SQL.
* [ ] Using **Widgets** to make notebooks interactive.
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
