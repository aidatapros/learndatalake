# learndatalake

This repo contains a 4 week self paced learning guide to make you confident in analysing data on the Databricks Free Edition platform.  It teach the basics of reading and writing data in the Lakehouse pattern.

# 🚀 Databricks Lakehouse Fundamentals: Onboarding & Certification Guide
# 🚀🚀 Databricks Free Edition: Zero-to-Hero (4-Week Training)

# Databricks Lakehouse Fundamentals: Onboarding & Certification Guide

Welcome to the Data Engineering team. As part of your onboarding, your first objective is to understand our core data architecture and achieve the **Databricks Lakehouse Fundamentals Accreditation**. 

This repository outlines the step-by-step process to complete the free training, understand the core concepts, and pass the exam.

---

## 🎯 Objective
Complete the Databricks Lakehouse Fundamentals learning path and pass the final assessment to earn your digital badge. This foundational knowledge is critical before you begin hands-on work with our data pipelines and Unity Catalog governance.

## 🛠️ Step 1: Account Setup
Before starting the training, you need to register for the Databricks Academy.
1. Go to the [Databricks Partner / Customer Academy](https://customer-academy.databricks.com/).
2. Sign up using your **company email address**.
3. Verify your email and log in to the portal.

## 📚 Step 2: The Training Pathway
Search the Academy catalog for the **Databricks Lakehouse Fundamentals** learning path. The training takes approximately 2 to 4 hours to complete and is broken down into the following core modules:

* **Introduction to the Data Lakehouse:** Why organizations are moving away from siloed Data Warehouses and Data Lakes to a unified Lakehouse architecture.
* **Databricks Architecture & Services:** The control plane vs. the data plane, and how Databricks interacts with cloud providers (AWS/Azure/GCP).
* **Data Management with Delta Lake:** Understanding ACID transactions, time travel, and the Bronze/Silver/Gold medallion architecture.
* **Data Governance with Unity Catalog:** How to secure, govern, and audit data, files, and machine learning models centrally.
* **Data Engineering & Databricks SQL:** An overview of Databricks Workflows, Delta Live Tables (DLT), and serverless SQL warehouses for BI reporting.
* **Machine Learning:** A high-level look at MLflow and Databricks AutoML.

> **💡 Pro Tip:** Do not skip the video summaries. Pay close attention to the distinctions between Databricks SQL, Data Science & Engineering, and Machine Learning workspaces.

## 📝 Step 3: Taking the Exam
Once you have completed the learning path, you will unlock the final assessment. 

* **Cost:** Free
* **Format:** Multiple-choice questions
* **Time Limit:** 20 minutes (typically)
* **Passing Score:** 80% (Usually 16 out of 20 questions correct)
* **Retakes:** You can retake the exam if you do not pass on the first attempt, but there may be a 24-hour cooling-off period.

### 🔑 Key Concepts to Review Before the Exam:
1. **Delta Lake:** Know what it is (an open-source storage layer) and its key features (ACID compliance, schema enforcement, time travel).
2. **Medallion Architecture:** Know the difference between Bronze (raw), Silver (cleansed/filtered), and Gold (business-level aggregates).
3. **Unity Catalog:** Understand that it provides a unified governance solution for all data and AI assets.
4. **Compute:** Differentiate between All-Purpose compute (interactive/dev) and Job compute (automated workflows).
5. **Personas:** Know which Databricks interface is designed for which user (e.g., Databricks SQL for Data Analysts, Machine Learning for Data Scientists).

## 🏆 Step 4: Post-Exam Actions
Once you pass the exam:
1. Claim your digital badge via Credly (you will receive an email from Databricks).
2. Take a screenshot of your passing certificate or badge.
3. Send the screenshot to your Team Lead / Onboarding Buddy so we can mark this milestone as complete.
4. Review the team's internal Jira board for your first hands-on Databricks task.

---



# 🚀 Databricks Free Edition: Zero-to-Hero (4-Week Training)

This repository contains a structured, 4-week roadmap to master the **Databricks Free Edition**. We focus on building confidence using the new **Serverless** architecture and the built-in `samples` catalog.

## 🛠 Prerequisites
* **Account:** [Databricks Free Edition](https://www.databricks.com/learn/free-edition).
* **Compute:** Ensure your notebook is attached to **Serverless** (green dot in the top-right corner).
* **Data:** We utilize the `samples` catalog (standard in Free Edition) to avoid manual file uploads.

---

## 📅 Weekly Curriculum

---

# 🧪 Lab Instructions: Week 1 & 2 (Analyst Focus)

These labs are optimized for the **Databricks Free Edition**. We will use the **Serverless SQL Warehouse**, the **Samples** catalog, and the **Databricks Assistant (Genie)**.

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

### Lab 1.2: Your First SQL Analysis
* **Task:** Identify the most profitable taxi payment methods.
* **Instructions:**
    1.  Create a new SQL Notebook: `Week1_Taxi_Analysis`.
    2.  Run the following query:
        ```sql
        SELECT 
            payment_type, 
            COUNT(*) as total_trips,
            AVG(fare_amount) as avg_fare
        FROM samples.nyctaxi.trips
        GROUP BY 1
        ORDER BY total_trips DESC;
        ```
    3.  **Visualization:** Click the **+** icon next to the "Results" tab ➡️ **Visualization** to create a Bar Chart.

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

## 📅 Week 2: Advanced Analytics & AI Generation
**Objective:** Leverage Databricks' built-in AI to handle complex logic and create interactive tools.

### Lab 2.1: Multi-Table Joins (The Retail Schema)
* **Task:** Analyze customer spending habits.
* **Instructions:**
    1.  Create a new SQL Notebook: `Week2_Retail_Intelligence`.
    2.  Join the `customer` and `orders` tables:
        ```sql
        SELECT 
            c.c_mktsegment,
            SUM(o.o_totalprice) AS total_revenue
        FROM samples.tpch.customer c
        JOIN samples.tpch.orders o ON c.c_custkey = o.o_custkey
        GROUP BY 1;
        ```

### Lab 2.2: Using Genie to Create Code (AI Assistant)
* **Task:** Use Natural Language to generate Spark and SQL code without manual typing.
* **Instructions:**
    1.  **Trigger the Assistant:** In a new cell, click the **Assistant (✨)** icon or use the shortcut `Cmd/Ctrl + I`.
    2.  **Generate SQL:** Type: *"Show me the top 5 longest trips in samples.nyctaxi.trips where the fare was over $50"* and hit **Generate**.
    3.  **Review & Accept:** Look at the code generated. If it looks correct, click **Accept**.
    4.  **Refine Code:** Use the Assistant to modify existing code. Highlight a block of code and ask: *"Add a column that calculates the tip percentage."*
    5.  **Explain Code:** If you see a complex function you don't recognize, highlight it and ask: *"What does this function do?"*

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
    3.  Change the dropdown value at the top and watch the data refresh instantly.

---  Week 3 and 4 still in development

## ✅ Checkpoint: Week 2 Review
By now, you should be comfortable with:
* [ ] Finding tables in the **Catalog**.
* [ ] Creating **Visualizations**.
* [ ] **Using Genie/Assistant** to write and explain code via natural language.
* [ ] Using **Widgets** for interactivity.

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
