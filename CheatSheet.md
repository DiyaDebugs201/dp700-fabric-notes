# 🚀 DP-700 Microsoft Fabric Cheat Sheet

> Last Minute Revision | Interview Quick Notes | Exam Day Guide

---

# 🏢 Fabric Overview

Microsoft Fabric is an end-to-end unified analytics platform.

It combines:

- Data Engineering
- Data Factory
- Data Science
- Data Warehouse
- Real-Time Intelligence
- Power BI
- OneLake

Think:

```
Everything Data
        ↓
 Microsoft Fabric
```

---

# OneLake

✔ One storage for the entire tenant

✔ Built on Azure Data Lake Storage Gen2

✔ Automatically created

✔ Cannot be deleted

✔ Stores all Fabric items

✔ Supports Shortcuts

---

# Workspace

Workspace = Project Folder

Contains:

- Lakehouse
- Warehouse
- Notebook
- Pipeline
- Reports
- Semantic Models
- Dataflows

---

# Lakehouse vs Warehouse

| Lakehouse | Warehouse |
|------------|-----------|
| Structured + Unstructured | Structured Only |
| Files + Tables | Tables |
| Spark + SQL | SQL |
| SQL Endpoint is Read Only | Full Read & Write |
| Delta Tables | T-SQL |

Remember:

Lakehouse = Data Engineering

Warehouse = Business Analytics

---

# OneLake Shortcuts

Purpose:

Access external data

WITHOUT

Copying data

Supports:

- ADLS
- Amazon S3
- Google Cloud Storage

Shortcut = Virtual Link

---

# Medallion Architecture

```
Bronze

↓

Silver

↓

Gold
```

Bronze

Raw Data

Silver

Cleaned Data

Gold

Business Ready Data

---

# ETL vs ELT

ETL

Extract

↓

Transform

↓

Load

Traditional

---

ELT

Extract

↓

Load

↓

Transform

Modern

Fabric mainly follows ELT.

---

# Data Loading

Full Load

Loads everything.

Incremental Load

Loads only changed records.

Preferred for large datasets.

---

# Batch vs Streaming

Batch

Large chunks

Scheduled

Spark

Pipelines

---

Streaming

Real Time

Continuous

Eventstreams

KQL

---

# Slowly Changing Dimensions

Type 0

Never Change

---

Type 1

Overwrite

---

Type 2

Add New Version

---

Type 3

Store Limited History

---

# Delta Lake

Provides:

✔ ACID Transactions

✔ Time Travel

✔ Schema Enforcement

✔ Transaction Log

✔ High Performance

---

# Important Delta Commands

OPTIMIZE

Small File Compaction

---

VACUUM

Delete obsolete files

---

ZORDER

Improve filtering performance

---

ANALYZE TABLE

Collect statistics

---

DESCRIBE HISTORY

View transaction history

---

# Spark Architecture

```
Driver

↓

Executors

↓

Tasks
```

Spark Session starts execution.

Spark Context manages cluster communication.

---

# Spark Optimization

Partition Data

↓

Reduce Shuffle

↓

Broadcast Small Tables

↓

Cache Frequently Used Data

↓

Filter Early

Remember:

P-S-B-C-F

---

# Repartition vs Coalesce

Repartition

✔ Increase or decrease partitions

✔ Causes shuffle

---

Coalesce

✔ Mostly reduce partitions

✔ Minimal shuffle

---

# Lazy Evaluation

Transformations

↓

Nothing Executes

↓

Action Called

↓

Execution Starts

Actions:

- count()
- show()
- collect()
- write()

---

# Broadcast Join

Small Table

↓

Copied to Executors

↓

Join Faster

Use only when one table is small.

---

# Pipelines

Used for:

- ETL/ELT
- Scheduling
- Automation
- Data Movement

Common Activities

- Copy
- Notebook
- Dataflow
- Stored Procedure
- If Condition
- ForEach
- Wait

---

# Dataflow Gen2

Low-code transformation

Power Query

Best for:

Business users

---

# Notebook

Best for:

PySpark

SQL

Python

Machine Learning

Complex transformations

---

# Choose the Right Tool

Pipeline

Automation

Notebook

Complex Spark

Dataflow

Low-code ETL

Warehouse

SQL Analytics

Lakehouse

Big Data

Eventstream

Streaming

---

# Eventstream

Used for

Real-time ingestion

Processes:

IoT

Sensors

Logs

Events

---

# Security

Authentication

Who are you?

Authorization

What can you do?

---

Workspace Roles

Admin

Everything

---

Member

Read

Write

Share

---

Contributor

Create

Edit

Cannot manage users

---

Viewer

Read Only

---

Security Types

RLS

Row Level

CLS

Column Level

OLS

Object Level

Sensitivity Labels

Protect sensitive data

---

CI/CD

Development

↓

Testing

↓

Production

Deployment Pipelines move changes safely.

---

Monitoring Hub

Monitor:

Pipelines

Notebooks

Refreshes

Jobs

Errors

Duration

---

Common Errors

Notebook

Out of Memory

Pipeline

Activity Failed

Warehouse

Slow Query

Shortcut

Permission

Refresh

Credential Error

---

Performance Optimization

✔ Filter Early

✔ Remove Unused Columns

✔ Optimize Tables

✔ Partition Data

✔ Cache Carefully

✔ Reduce Shuffle

✔ Update Statistics

✔ Batch Loads

---

Warehouse Optimization

Avoid

SELECT *

Use

SELECT Required Columns

Always filter early.

---

Important SQL

GROUP BY

JOIN

ROW_NUMBER()

RANK()

DENSE_RANK()

LAG()

LEAD()

SUM()

AVG()

COUNT()

---

PySpark Basics

read()

write()

filter()

select()

join()

groupBy()

agg()

cache()

repartition()

coalesce()

---

KQL Basics

Real-Time Intelligence

Eventhouse

Streaming Queries

Window Functions

---

Troubleshooting Flow

Problem

↓

Monitoring Hub

↓

Logs

↓

Root Cause

↓

Fix

↓

Retest

Remember:

I-L-R-F-T

---

Microsoft Loves Asking...

✔ Incremental vs Full Load

✔ ETL vs ELT

✔ Pipeline vs Notebook vs Dataflow

✔ Lakehouse vs Warehouse

✔ OneLake Shortcuts

✔ Delta Commands

✔ Spark Optimization

✔ Monitoring Hub

✔ Semantic Model Refresh

✔ Workspace Roles

✔ RLS vs CLS

✔ Eventstream

✔ Batch vs Streaming

✔ Performance Optimization

✔ Troubleshooting

---

# Memory Tricks

B → S → G

Bronze

Silver

Gold

---

O → Z → A → V → H

Optimize

ZORDER

Analyze

Vacuum

History

---

P → S → B → C → F

Partition

Shuffle

Broadcast

Cache

Filter

---

I → L → R → F → T

Identify

Logs

Root Cause

Fix

Test

---

F → P → P → C

Filter

Partition

Parallel

Cache

---

S → F → J → S

Select Columns

Filter Early

Reduce Joins

Statistics

---

# 30-Second Revision

Fabric = Unified Analytics Platform

OneLake = Single Storage

Workspace = Project Container

Lakehouse = Spark + Files

Warehouse = SQL Analytics

Pipeline = Automation

Notebook = Spark

Dataflow = Low-Code ETL

Eventstream = Streaming

Bronze → Silver → Gold

ELT > ETL

Incremental > Full (Large Data)

OPTIMIZE = Compact Files

VACUUM = Remove Old Files

ZORDER = Faster Filtering

ANALYZE = Statistics

DESCRIBE HISTORY = Transactions

Monitoring Hub = First Stop

Authentication = Who

Authorization = What

Remember:

**Filter Early**

**Partition Data**

**Reduce Shuffle**

**Monitor Everything**

**Fix Root Cause, Not Symptoms**