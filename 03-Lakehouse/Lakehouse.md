# Lakehouse

## What is a Lakehouse?

A Lakehouse is a data architecture that combines the flexibility of a Data Lake with the analytical capabilities of a Data Warehouse.

It allows organizations to store, process, and analyze data in a single platform.

Think:

> Data Lake + Data Warehouse = Lakehouse

---

## Why Do We Need a Lakehouse?

Traditionally:

### Data Lake

Advantages:

* Stores any type of data
* Highly scalable
* Low storage cost

Disadvantages:

* Limited governance
* Less optimized for analytics

---

### Data Warehouse

Advantages:

* Fast analytical queries
* Structured data
* Strong governance

Disadvantages:

* Less flexible
* Primarily structured data

---

A Lakehouse combines the strengths of both.

---

## Lakehouse in Microsoft Fabric

A Lakehouse is a Fabric item that stores data in OneLake.

It supports:

* Structured data
* Semi-structured data
* Unstructured data

Examples:

* CSV
* JSON
* Parquet
* Images
* Log files
* Delta Tables

---

## Lakehouse Architecture

Lakehouse

├── Files
├── Tables
└── SQL Analytics Endpoint

---

## Files Area

Used for storing raw files.

Examples:

* CSV
* JSON
* Parquet
* Images

Typically used during ingestion.

---

## Tables Area

Stores managed Delta Tables.

Advantages:

* ACID transactions
* Better query performance
* Versioning support
* Optimized analytics

Used for transformed and curated data.

---

## SQL Analytics Endpoint

Every Lakehouse automatically provides a SQL Analytics Endpoint.

Purpose:

Allow SQL users to query Lakehouse tables.

Characteristics:

* Read-only SQL interface
* Supports analytical queries
* Automatically generated

Important:

The SQL Analytics Endpoint is read-only.

The Lakehouse itself is not read-only.

Spark can still write data into the Lakehouse.

---

## Lakehouse and OneLake

Relationship:

OneLake
↓
Lakehouse
↓
Files & Tables

OneLake provides storage.

Lakehouse provides structure and analytics capabilities.

---

## Lakehouse and Spark

Lakehouse is optimized for Spark workloads.

Spark is commonly used for:

* Data ingestion
* Transformation
* Cleaning
* Aggregation
* Machine learning

Data is typically written into Delta Tables.

---

## Common Data Engineering Workflow

Source Systems
↓
OneLake
↓
Lakehouse Files
↓
Spark Transformations
↓
Lakehouse Tables
↓
Analytics

---

## Benefits of Lakehouse

### Unified Storage

Single platform for raw and processed data.

---

### Open Formats

Supports:

* Delta
* Parquet
* CSV
* JSON

---

### Scalability

Handles large volumes of data.

---

### Analytics Ready

Supports SQL and Spark.

---

## Lakehouse vs Data Lake

| Feature       | Data Lake | Lakehouse |
| ------------- | --------- | --------- |
| Raw Storage   | Yes       | Yes       |
| SQL Analytics | Limited   | Strong    |
| Governance    | Limited   | Better    |
| Delta Tables  | No        | Yes       |

---

## Lakehouse vs Warehouse

| Feature       | Lakehouse    | Warehouse   |
| ------------- | ------------ | ----------- |
| Data Types    | All Types    | Structured  |
| Spark Support | Yes          | Limited     |
| SQL Support   | SQL Endpoint | Full T-SQL  |
| Flexibility   | High         | Lower       |
| Analytics     | Strong       | Very Strong |

---

## DP-700 Exam Scenarios

### Scenario 1

Data arrives as JSON and CSV files.

Requirement:

Store and transform data.

Solution:

Use a Lakehouse.

---

### Scenario 2

Data Engineers use Spark.

Requirement:

Store transformed data.

Solution:

Lakehouse with Delta Tables.

---

### Scenario 3

Business users need SQL access.

Requirement:

Query Lakehouse data.

Solution:

Use SQL Analytics Endpoint.

---

## Common Exam Traps

### Trap 1

Question:

Is a Lakehouse read-only?

Answer:

No.

Only the SQL Analytics Endpoint is read-only.

---

### Trap 2

Question:

Can a Lakehouse store unstructured data?

Answer:

Yes.

Supports structured, semi-structured, and unstructured data.

---

## Memory Trick

Lakehouse

= Data Lake Storage

*

Warehouse Analytics

---

## DP-700 Exam Focus

Know:

* Files vs Tables
* SQL Analytics Endpoint
* Spark integration
* Lakehouse architecture
* OneLake relationship
* Lakehouse vs Warehouse

---

## Quick Revision

* Lakehouse combines Data Lake and Warehouse capabilities.
* Stores all data types.
* Built on OneLake.
* Contains Files and Tables.
* Tables use Delta format.
* Supports Spark processing.
* SQL Analytics Endpoint is automatically generated.
* SQL Endpoint is read-only.
* Lakehouse itself supports read and write operations.
* One of the most important DP-700 topics.
