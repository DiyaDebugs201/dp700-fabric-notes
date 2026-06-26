# ETL vs ELT

## What are ETL and ELT?

ETL and ELT are two common data integration patterns used to move data from source systems into an analytics platform.

Both involve three steps:

* Extract
* Transform
* Load

The difference is **when the transformation happens**.

---

# ETL (Extract → Transform → Load)

## What is ETL?

In ETL, data is transformed **before** it is loaded into the destination.

### Workflow

Source Systems
↓
Extract
↓
Transform
↓
Load into Storage

---

## How ETL Works

1. Extract data from source systems.
2. Clean and transform the data.
3. Load the transformed data into the destination.

---

## Advantages

* Only clean data is stored.
* Good for legacy systems.
* Data quality checks happen early.

---

## Disadvantages

* Slower for large datasets.
* Requires separate transformation infrastructure.
* Less flexible if business rules change.

---

## Example

A retail company extracts customer data, removes duplicates, standardizes date formats, and then loads the cleaned data into a data warehouse.

---

# ELT (Extract → Load → Transform)

## What is ELT?

In ELT, raw data is loaded into the destination first.

Transformations happen later inside the analytics platform.

### Workflow

Source Systems
↓
Extract
↓
Load into OneLake / Lakehouse
↓
Transform using Spark or SQL

---

## How ELT Works

1. Extract raw data.
2. Load it into Fabric.
3. Transform it using Spark, SQL, or Dataflows.

---

## Advantages

* Faster ingestion.
* Preserves raw data.
* Supports multiple transformation needs.
* Scales well for cloud platforms.

---

## Disadvantages

* Raw data may contain duplicates or errors.
* Requires sufficient compute resources for transformations.

---

# Why Fabric Uses ELT

Microsoft Fabric is designed around ELT because:

* OneLake provides scalable storage.
* Spark performs distributed transformations.
* Data can be reused for different business needs.
* Raw data is preserved for auditing and reprocessing.

This fits naturally with the Medallion Architecture.

---

# ETL vs ELT Comparison

| Feature                  | ETL        | ELT   |
| ------------------------ | ---------- | ----- |
| Transform Before Loading | ✅ Yes      | ❌ No  |
| Transform After Loading  | ❌ No       | ✅ Yes |
| Raw Data Preserved       | Usually No | Yes   |
| Cloud Friendly           | Less       | More  |
| Fabric Preferred         | No         | Yes   |

---

# ETL and the Medallion Architecture

In Fabric:

Bronze Layer
↓
Raw data loaded (ELT)

↓

Silver Layer
↓
Cleaned and transformed

↓

Gold Layer
↓
Business-ready analytics

ELT aligns naturally with this architecture.

---

# Common Transformation Tasks

During ELT, common transformations include:

* Removing duplicates
* Handling null values
* Filtering records
* Joining tables
* Aggregating data
* Standardizing formats
* Creating calculated columns

These transformations are commonly performed using:

* Spark
* SQL
* Dataflows Gen2

---

# ETL vs ELT in Microsoft Fabric

Typical Fabric workflow:

Source System
↓
Pipeline
↓
OneLake / Lakehouse
↓
Spark Notebook / SQL / Dataflow Gen2
↓
Delta Tables
↓
Power BI

---

# Common DP-700 Scenarios

### Scenario 1

Requirement:

Keep an untouched copy of the original data.

Answer:

ELT

---

### Scenario 2

Requirement:

Apply transformations after loading data into Fabric.

Answer:

ELT

---

### Scenario 3

Requirement:

Legacy system transforms data before loading.

Answer:

ETL

---

### Scenario 4

Requirement:

Use Spark to clean large datasets after ingestion.

Answer:

ELT

---

# Common Exam Traps

### Trap 1

Question:

Which approach is preferred in Microsoft Fabric?

Answer:

ELT.

---

### Trap 2

Question:

Which approach preserves raw data?

Answer:

ELT.

---

### Trap 3

Question:

Which approach transforms data before loading?

Answer:

ETL.

---

# Memory Trick

ETL

= Clean → Store

---

ELT

= Store → Clean

---

Think:

ETL = Wash clothes **before** putting them in the wardrobe.

ELT = Put clothes in the wardrobe first, then organize and fold them later.

---