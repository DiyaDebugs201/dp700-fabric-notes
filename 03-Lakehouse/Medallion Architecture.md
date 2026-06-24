# Medallion Architecture

## What is Medallion Architecture?

Medallion Architecture is a data design pattern used to organize and improve data quality as it moves through different stages of processing.

The architecture consists of three layers:

Bronze
↓
Silver
↓
Gold

Each layer increases data quality, structure, and business value.

---

## Why Use Medallion Architecture?

Raw data is often:

* Incomplete
* Duplicated
* Inconsistent
* Difficult to analyze

Instead of transforming everything at once, data is gradually refined through multiple layers.

Benefits:

* Better data quality
* Easier troubleshooting
* Clear data lineage
* Improved governance
* Scalable processing

---

## Bronze Layer

### Purpose

Store raw data exactly as received from source systems.

Think:

> Landing Zone

---

### Characteristics

* Raw data
* Minimal transformations
* Historical records preserved
* May contain duplicates
* May contain null values

---

### Data Sources

Examples:

* Databases
* APIs
* CSV files
* JSON files
* Event streams

---

### Example

Raw Sales Data:

| CustomerID | Amount |
| ---------- | ------ |
| 101        | 500    |
| 101        | 500    |
| NULL       | 300    |

Problems remain unchanged.

---

## Silver Layer

### Purpose

Clean, validate, and standardize data.

Think:

> Data Preparation Layer

---

### Typical Transformations

* Remove duplicates
* Handle missing values
* Standardize formats
* Apply business rules
* Join datasets

---

### Example

Raw Bronze Data:

| CustomerID | Amount |
| ---------- | ------ |
| 101        | 500    |
| 101        | 500    |
| NULL       | 300    |

Silver Data:

| CustomerID | Amount |
| ---------- | ------ |
| 101        | 500    |

Duplicates and invalid records removed.

---

## Gold Layer

### Purpose

Provide business-ready data for reporting and analytics.

Think:

> Executive Dashboard Layer

---

### Typical Transformations

* Aggregations
* KPIs
* Metrics
* Dimensional modeling
* Business calculations

---

### Example

Monthly Sales Summary:

| Month   | Total Sales |
| ------- | ----------- |
| January | ₹1,20,000   |

Optimized for reporting.

---

## End-to-End Flow

Source Systems
↓
Bronze
↓
Silver
↓
Gold
↓
Power BI / Analytics

---

## Medallion Architecture in Fabric

A Fabric Lakehouse commonly stores:

### Bronze Tables

Raw ingestion data.

---

### Silver Tables

Validated and cleaned data.

---

### Gold Tables

Business-ready analytics data.

---

## Relationship with Delta Lake

Each layer commonly uses Delta Tables.

Benefits:

* ACID Transactions
* Time Travel
* Version History
* Better Performance

---

## Common Transformations by Layer

| Activity        | Bronze | Silver    | Gold |
| --------------- | ------ | --------- | ---- |
| Raw Storage     | Yes    | No        | No   |
| Deduplication   | No     | Yes       | Yes  |
| Data Validation | No     | Yes       | Yes  |
| Aggregation     | No     | Limited   | Yes  |
| Reporting Ready | No     | Partially | Yes  |

---

## Example: E-Commerce System

### Bronze

Store:

* Orders
* Customers
* Products

Exactly as received.

---

### Silver

Transform:

* Remove duplicate orders
* Fix invalid records
* Standardize formats

---

### Gold

Create:

* Daily Sales
* Monthly Revenue
* Top Products
* Customer KPIs

Used by dashboards.

---

## Benefits

### Improved Data Quality

Data becomes progressively cleaner.

---

### Easier Troubleshooting

Problems can be traced back to a specific layer.

---

### Better Governance

Clear separation of responsibilities.

---

### Reusability

Different teams can consume data from appropriate layers.

---

## Common DP-700 Scenarios

### Scenario 1

Requirement:

Preserve original source data.

Solution:

Store in Bronze Layer.

---

### Scenario 2

Requirement:

Remove duplicates and fix missing values.

Solution:

Silver Layer.

---

### Scenario 3

Requirement:

Prepare data for Power BI dashboards.

Solution:

Gold Layer.

---

### Scenario 4

Requirement:

Create KPI summaries.

Solution:

Gold Layer.

---

## Common Exam Traps

### Trap 1

Question:

Which layer stores raw data?

Answer:

Bronze.

---

### Trap 2

Question:

Which layer handles data cleansing?

Answer:

Silver.

---

### Trap 3

Question:

Which layer is optimized for reporting?

Answer:

Gold.

---

### Trap 4

Question:

Can Delta Tables exist in all layers?

Answer:

Yes.

---

## Memory Trick

Bronze

= Raw Data

---

Silver

= Clean Data

---

Gold

= Business Data

---

Think:

Bronze Mine
↓
Silver Refinery
↓
Gold Jewelry

Value increases at each stage.

---