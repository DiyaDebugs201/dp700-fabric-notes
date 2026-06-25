# Lakehouse vs Warehouse

## Why This Comparison Matters

Both Lakehouse and Warehouse can store and analyze data in Microsoft Fabric.

The challenge is knowing:

> When should you choose Lakehouse?
>
> When should you choose Warehouse?

This is one of the most common DP-700 exam themes.

---

# Quick Summary

Choose:

### Lakehouse

When:

* Using Spark
* Working with files
* Handling structured and unstructured data
* Building data engineering pipelines
* Using Delta Tables

---

### Warehouse

When:

* Using SQL heavily
* Building reports and dashboards
* Working with structured data
* Supporting business analysts

---

# Core Difference

## Lakehouse

Combines:

* Data Lake
* Data Warehouse

Supports:

* Files
* Spark
* SQL Analytics Endpoint
* Delta Tables

---

## Warehouse

Relational analytical database.

Supports:

* Full T-SQL
* Reporting
* Business intelligence
* Structured data

---

# Comparison Table

| Feature              | Lakehouse | Warehouse    |
| -------------------- | --------- | ------------ |
| Storage              | OneLake   | OneLake      |
| Structured Data      | Yes       | Yes          |
| Semi-Structured Data | Yes       | Limited      |
| Unstructured Data    | Yes       | No           |
| Spark Support        | Yes       | No           |
| Delta Tables         | Yes       | No           |
| Full T-SQL Support   | No        | Yes          |
| SQL Endpoint         | Read-Only | Read + Write |
| Data Engineering     | Excellent | Limited      |
| BI Reporting         | Good      | Excellent    |
| Flexibility          | High      | Moderate     |

---

# Data Types

## Lakehouse

Supports:

* CSV
* JSON
* Parquet
* Images
* Videos
* Logs
* Delta Tables

---

## Warehouse

Supports:

* Structured relational tables

Best for:

* Business reporting
* Analytics

---

# SQL Support

## Lakehouse

Provides:

SQL Analytics Endpoint

Characteristics:

* Read-only
* Query Lakehouse tables
* Reporting access

---

## Warehouse

Provides:

Full T-SQL capabilities.

Supports:

* INSERT
* UPDATE
* DELETE
* MERGE
* Stored Procedures

---

# Spark Support

## Lakehouse

Fully integrated with Spark.

Used for:

* ETL
* ELT
* Data cleansing
* Aggregation
* Machine Learning

---

## Warehouse

Not designed for Spark-first workloads.

---

# Data Engineering Use Cases

Choose Lakehouse when:

* Building ingestion pipelines
* Working with raw files
* Creating Medallion Architecture
* Using Delta Lake

---

# Business Intelligence Use Cases

Choose Warehouse when:

* Creating dashboards
* Running SQL reports
* Performing business analytics
* Building dimensional models

---

# Common Scenarios

## Scenario 1

Requirement:

Data arrives as JSON files.

Need:

Spark transformations.

Answer:

Lakehouse

---

## Scenario 2

Requirement:

Business analysts primarily use SQL.

Need:

Full T-SQL support.

Answer:

Warehouse

---

## Scenario 3

Requirement:

Store raw and processed data.

Answer:

Lakehouse

---

## Scenario 4

Requirement:

Power BI reporting with structured tables.

Answer:

Warehouse

---

## Scenario 5

Requirement:

Implement Bronze, Silver, and Gold layers.

Answer:

Lakehouse

---

## Scenario 6

Requirement:

Fact and Dimension tables for reporting.

Answer:

Warehouse

---

# Decision Tree

Do you need Spark?

YES
→ Lakehouse

NO
↓
Need Full T-SQL?

YES
→ Warehouse

NO
↓
Need Raw Files?

YES
→ Lakehouse

NO
↓
Need Structured Reporting?

YES
→ Warehouse

---

# Common Exam Traps

## Trap 1

Question:

Both use OneLake?

Answer:

Yes.

---

## Trap 2

Question:

Can Lakehouse store files?

Answer:

Yes.

---

## Trap 3

Question:

Can Warehouse store unstructured data?

Answer:

No.

---

## Trap 4

Question:

Which supports Delta Tables?

Answer:

Lakehouse.

---

## Trap 5

Question:

Which supports full T-SQL?

Answer:

Warehouse.

---

# Memory Trick

Lakehouse

= Data Engineer's Home

---

Warehouse

= Data Analyst's Home

---

Lakehouse

= Spark First

---

Warehouse

= SQL First

---

# DP-700 Exam Focus

Know:

* Spark → Lakehouse
* Delta Tables → Lakehouse
* Raw Files → Lakehouse
* Full T-SQL → Warehouse
* Reporting → Warehouse
* Structured Data → Warehouse
* Medallion Architecture → Lakehouse

These comparisons appear frequently in scenario-based questions.

---

# Quick Revision

* Both use OneLake.
* Lakehouse supports all data types.
* Warehouse focuses on structured data.
* Lakehouse supports Spark.
* Warehouse supports full T-SQL.
* Lakehouse uses Delta Tables.
* Warehouse is optimized for reporting.
* Lakehouse is optimized for data engineering.
* SQL Endpoint in Lakehouse is read-only.
* Warehouse supports read and write SQL operations.
