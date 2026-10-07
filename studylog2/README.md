## Study Log 2

### I am taking Data Engineering Learning Plan course, lesson 3: Build Data Pipelines with Apache Spark Declarative Pipelines.

### [03 Aug] — Read the official exam guide

Resource: Databricks Certified Data Engineer Associate exam guide, May 2026 version <br>
Status: ✅ Done. <br>
Takeaways:  <br>
The exam covers 7 domains; know the weightings before you study anything else — see the table in README.md.
No formal prerequisites, but hands-on experience with everything in the guide is explicitly recommended by Databricks, not just reading about it.
Open questions: none yet.  

### [07 Aug] — Started "Data Ingestion with Lakeflow Connect" (self-paced)

Resource: Databricks Academy self-paced course, Data Ingestion with Lakeflow Connect <br>
Status: ✅ Done. <br>
Takeaways: (fill in as you go — what does Lakeflow Connect actually do, which source connectors did you try, what surprised you) <br>
Open questions: (add anything unclear so a reviewer or the next learner can help) <br>

### [10 August 2026] — Building pipelines with Lakeflow Spark Declarative Pipelines

Resources: <br>
Databricks Academy self-paced course, Build Data Pipelines with Lakeflow Spark Declarative Pipelines (3 sections / 22 lessons / ~2 hrs, Associate level)
Databricks Community learning series: "Build Data Pipelines with Lakeflow Spark" <br>
Status: 🟡 In progress <br>
Takeaways: (fill in — e.g. streaming tables vs materialized views vs temporary views, how you set up data-quality expectations, first impressions of the event log / monitoring UI) <br>
Open questions: (e.g. "still unclear on AUTO CDC INTO for slowly changing dimensions — need another pass")
<pre>
-----
Because there is no lab available for self-paced version of the previous course, I took another course named "Get Started with Data Engineering" which includes lab after every lesson for practicing. Below is my progress of this course. 
**###[14-17 August 2026] - Lesson 1: Find Your Data and Create a Delta Table**
Take away: 
Navigated the Unity Catalog hierarchy (catalog → schema → volume)
Previewed raw CSV data using read_files
Created first Delta table using CREATE TABLE AS SELECT
Verified the table in both SQL and Catalog Explorer
</pre>

<pre>
**###[21-24 August 2026] - Lesson 2: Modify Data with INSERT, UPDATE, and DELETE**
Take away:
Every INSERT, UPDATE, and DELETE creates a new version of the table. Delta Lake tracks all of these versions automatically, which means I can always see what my data looked like before a change
After this lesson, I'm able to:
Added rows with INSERT INTO
Changed a value with UPDATE ... SET ... WHERE
Removed a row with DELETE FROM ... WHERE
Verified all changes are tracked with DESCRIBE HISTORY
</pre>

<pre>
**###[28-31 August 2026] - Lesson 3: Explore Version History and Time Travel**
Take away:
Each operation created a new version in Delta Lake. Delta Lake automatically maintains a transaction log that records every operation performed on a table. View a Delta table's change log and query data from any previous version is essential in case of auditing, debugging and recovery the data.
After this lesson, I'm able to:
Viewed the full change log with DESCRIBE HISTORY
Queried previous versions with VERSION AS OF
Compared row counts across versions to detect changes
Used the @v shorthand syntax for time travel
</pre>

<pre>
**###[04-07 September 2026] - Lesson 4: Ingest Data with CTAS and the Upload UI**
Take a way: 
Create a table as select: use when building a pipeline, need reproducibility, or want to select specific columns from the source file
Catalog Explorer Upload: use when someone hands you a CSV and you need it in a table fast. Quick, ad-hoc imports where reproducibility is not a concern.
After this lesson, I'm able to:
Created a table with CTAS using explicit format options (format, header, inferSchema)
Selected specific columns to produce a clean table without _rescued_data
Created a table using the Catalog Explorer Upload UI with no code
Verified both methods produced working Delta tables
CTAS is code-driven and repeatable. The Upload UI is fast but manual.
</pre>

<pre>
**###[11-14 September 2026] - Lesson 5: Load Data Incrementally with COPY INTO**
Take away:
COPY INTO is safe to run on a schedule because it never double-loads data. For production workloads at scale, Databricks recommends streaming tables as a more scalable alternative, but the incremental loading concept is the same.
After this lesson, I'm able to:
Created an empty table with a defined schema
Loaded 6 rows from 2 CSV files using COPY INTO
Proved idempotency — re-running loaded 0 rows because the files were already processed
Verified the transaction log only records actual changes
</pre>

<pre>
**###[21 September 2026] - Lesson 6: Build a Medallion Architecture Pipeline**
Take away:
The Medallion Architecture organizes data into three layers. Each layer adds quality and structure, moving data from raw ingestion to business-ready analytics:
Bronze — Raw Ingestion: Data exactly as it arrived. No transformations, no filtering. The source of truth for what was received.
Silver — Cleaned & Enriched: Data is cleaned, standardized, and enriched. Duplicates removed, types corrected, audit columns added. The foundation for analysis.
Gold — Business-Ready: Aggregated, filtered, or joined for specific business use cases. What dashboards and analysts consume.
The reason why there are 3 layers is keeping raw data separate from cleaned data means we can always go back to the source. If a transformation has a bug, we fix the Silver logic and re-run it from Bronze. We never lose the original data.
After this lesson, I'm able to:
Created a Bronze table with raw data using COPY INTO
Created a Silver table with transformations (UPPER, audit timestamps)
Created a Gold table with aggregated, business-ready data
Used the INSERT OVERWRITE pattern for refreshable Gold tables
Explored lineage, permissions, and insights in Catalog Explorer
</pre>

<pre>
**###[25-28 September 2026] - Lesson 7: Automate Your Pipeline with a LakeFlow Job**
Take away:
Create a multi-task LakeFlow Job that orchestrates the Bronze → Silver → Gold pipeline with task dependencies, and monitor its execution. A LakeFlow Job runs one or more notebooks as tasks, with dependencies between them. We can define what runs, in what order, and on what schedule.
After this lesson, I'm able to:
Created a LakeFlow Job with two tasks and a dependency
Explored scheduling options (cron, file arrival, table updates)
Ran the job and monitored each task's execution
Verified the automated pipeline produced the same Bronze → Silver → Gold results
</pre>

<pre>
**###[02-05 October 2026] - Lesson 8: Build a Declarative Pipeline with Spark Declarative Pipelines**
Take away:
Spark Declarative Pipelines handles execution order, incremental processing, error recovery, and infrastructure; we just define the tables. 
Compare to imperative pipeline: less code, automatic orchestration, and built-in data quality.
After this lesson, I'm able to:
Defined a full Bronze → Silver → Gold pipeline in 3 SQL statements
Used a streaming table for incremental ingestion (Bronze)
Used materialized views for transformations (Silver) and aggregations (Gold)
Added data quality expectations to catch issues automatically
Configured and ran an ETL Pipeline that handled orchestration, compute, and execution order for you
</pre>
