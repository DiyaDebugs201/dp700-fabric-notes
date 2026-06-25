# Data Warehouse

## What is a Data Warehouse?

A Data Warehouse is a centralized analytical database designed for storing structured data and supporting business intelligence (BI) workloads.

It is optimized for:

* Reporting
* Dashboards
* Analytics
* SQL Queries

Think:

> A Warehouse is a highly organized library built specifically for analytics.

---

## Why Use a Data Warehouse?

Organizations need:

* Fast reporting
* Historical analysis
* Business metrics
* Dashboard performance

A Data Warehouse is designed specifically for these requirements.

---

## Warehouse in Microsoft Fabric

A Fabric Warehouse is a fully managed analytical database.

It provides:

* Full T-SQL support
* Structured storage
* High-performance analytical queries

Unlike Lakehouse, Warehouse is SQL-first.

---

## Key Characteristics

### Structured Data

Warehouses primarily work with:

* Tables
* Rows
* Columns
* Relationships

Best for:

* Sales
* Finance
* Customer analytics
* Business reporting

---

### Full T-SQL Support

Supports:

* SELECT
* INSERT
* UPDATE
* DELETE
* MERGE
* Stored Procedures

This is one of the biggest differences from a Lakehouse SQL Endpoint.

---

### Analytics Optimized

Designed for:

* Aggregations
* Joins
* Reporting workloads
* Power BI

---

## Typical Architecture

Source Systems
↓
Ingestion
↓
Warehouse
↓
Power BI
↓
Business Users

---

## Warehouse Objects

Common objects include:

### Tables

Store business data.

Example:

* Customers
* Orders
* Products

---

### Views

Virtual representations of data.

Used to simplify reporting.

---

### Stored Procedures

Reusable SQL logic.

Used for:

* Transformations
* Automation
* Data loading

---

### Functions

Reusable business calculations.

---

## Data Modeling

Warehouses often use dimensional models.

Common structures:

### Fact Tables

Store measurable business events.

Examples:

* Sales
* Orders
* Transactions

---

### Dimension Tables

Store descriptive information.

Examples:

* Customer
* Product
* Location
* Date

---

## Example

### FactSales

| CustomerID | ProductID | SalesAmount |
| ---------- | --------- | ----------- |
| 101        | 20        | 500         |

---

### DimCustomer

| CustomerID | CustomerName |
| ---------- | ------------ |
| 101        | Diya         |

---

## Slowly Changing Dimensions (SCD)

Used to manage historical changes.

### Type 0

No changes allowed.

---

### Type 1

Overwrite existing value.

History is lost.

---

### Type 2

Create a new row.

History is preserved.

Most commonly tested.

---

### Type 3

Store previous value in an additional column.

Limited history.

---

## Warehouse Performance Benefits

### Optimized Storage

Data is organized for analytical workloads.

---

### Faster Aggregations

Suitable for KPI reporting.

---

### Efficient SQL Execution

Optimized query engine.

---

## Common Warehouse Use Cases

### Financial Reporting

Monthly revenue analysis.

---

### Sales Dashboards

Regional performance metrics.

---

### Executive Reporting

Business KPIs.

---

### Historical Analysis

Trend reporting over time.

---

## Common DP-700 Scenarios

### Scenario 1

Requirement:

Business analysts use SQL extensively.

Solution:

Warehouse.

---

### Scenario 2

Requirement:

Power BI dashboard needs fast aggregated results.

Solution:

Warehouse.

---

### Scenario 3

Requirement:

Structured enterprise reporting.

Solution:

Warehouse.

---

## Common Exam Traps

### Trap 1

Question:

Does Warehouse support full T-SQL?

Answer:

Yes.

---

### Trap 2

Question:

Can Warehouse handle structured business reporting?

Answer:

Yes.

---

### Trap 3

Question:

Which SCD type preserves history?

Answer:

Type 2.

---

## Memory Tricks

Fact Table

= Event

Example:

Sale happened.

---

Dimension Table

= Description

Example:

Who bought it?

What product?

When?

---

Warehouse

= SQL Analytics Engine

---