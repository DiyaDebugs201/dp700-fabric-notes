# Loading Patterns

## What are Loading Patterns?

A loading pattern defines **how data is moved** from source systems into an analytics platform.

Choosing the correct loading pattern improves:

* Performance
* Cost efficiency
* Data quality
* Scalability

Microsoft Fabric supports several loading strategies depending on business requirements.

---

# Types of Loading Patterns

The most common loading patterns are:

* Full Load
* Incremental Load
* Change Data Capture (CDC)

---

# Full Load

## What is Full Load?

A Full Load copies **all records** from the source into the destination every time the process runs.

### Workflow

Source Table
↓

Copy Every Record
↓

Lakehouse / Warehouse

---

## Example

Customer Table

100,000 records

Every night:

↓

Load all 100,000 records again.

---

## Advantages

* Simple to implement.
* Easy to troubleshoot.
* No need to track changes.

---

## Disadvantages

* Slow for large datasets.
* Higher compute and storage costs.
* Unnecessary processing of unchanged data.

---

## Best Used When

* Small datasets
* Initial migrations
* One-time imports

---

# Incremental Load

## What is Incremental Load?

Incremental Load copies **only new or modified records** since the last successful load.

### Workflow

Source Table
↓

Identify New/Updated Records
↓

Load Only Those Records

---

## Example

Yesterday:

100,000 records

Today:

250 new records

Incremental Load copies only the **250 new or updated rows**.

---

## Advantages

* Faster execution
* Lower compute cost
* Better scalability
* Reduced network traffic

---

## Disadvantages

* More complex implementation
* Requires tracking changes
* Error handling can be more difficult

---

## Best Used When

* Large datasets
* Daily ingestion
* Enterprise systems
* Cloud analytics

---

# Change Data Capture (CDC)

## What is CDC?

Change Data Capture identifies changes in a source system and captures:

* Inserts
* Updates
* Deletes

instead of reading the entire table.

---

## Why CDC?

Without CDC:

Every row must be compared.

With CDC:

Only changed rows are processed.

---

## Benefits

* Very efficient
* Faster incremental processing
* Reduces unnecessary reads
* Ideal for enterprise databases

---

## Example

Customer Table

Yesterday:

100,000 rows

Today:

10 Inserts

3 Updates

1 Delete

CDC processes only those 14 changes.

---

# Full Load vs Incremental Load vs CDC

| Feature            | Full Load | Incremental Load | CDC     |
| ------------------ | --------- | ---------------- | ------- |
| Loads All Data     | ✅         | ❌                | ❌       |
| Loads Only Changes | ❌         | ✅                | ✅       |
| Detects Deletes    | ❌         | Sometimes        | ✅       |
| Performance        | Lower     | Higher           | Highest |
| Complexity         | Low       | Medium           | High    |

---

# Handling Duplicate Records

Duplicates commonly occur because of:

* Multiple source systems
* Reprocessing
* Manual data entry

Common solutions:

* Remove duplicates
* Use DISTINCT
* Apply ROW_NUMBER()
* Use MERGE operations

---

# Handling Missing Data

Missing values can reduce data quality.

Common approaches:

* Replace with default values
* Fill using business rules
* Remove invalid rows
* Keep NULL when appropriate

---

# Handling Late-Arriving Data

## What is Late-Arriving Data?

Data that reaches the analytics platform later than expected.

Example:

A sales transaction occurs at 10:00 AM but arrives at 3:00 PM.

---

## Why It Matters

Late-arriving data can affect:

* Reports
* KPIs
* Aggregations
* Dashboards

---

## Common Strategies

* Reprocess affected partitions
* Merge late records
* Update existing tables
* Use timestamps to identify delayed data

---

# Relationship with Slowly Changing Dimensions (SCD)

Loading patterns often work together with SCDs.

Example:

Incremental Load

↓

Customer Address Changed

↓

SCD Type 2

↓

Create a new historical record instead of overwriting the old one.

---

# Loading Patterns in Microsoft Fabric

Typical workflow:

Source Database
↓

Pipeline

↓

Lakehouse

↓

Spark / SQL

↓

Bronze

↓

Silver

↓

Gold

Incremental loading is commonly used between Bronze and Silver layers.

---

# Common DP-700 Scenarios

### Scenario 1

Requirement:

Load a 5-million-row table every night.

Only today's records changed.

Answer:

Incremental Load.

---

### Scenario 2

Requirement:

Initial migration of a new database.

Answer:

Full Load.

---

### Scenario 3

Requirement:

Capture inserts, updates, and deletes.

Answer:

Change Data Capture (CDC).

---

### Scenario 4

Requirement:

A transaction arrives several hours late.

Answer:

Handle Late-Arriving Data.

---

### Scenario 5

Requirement:

Remove repeated customer records before reporting.

Answer:

Deduplication.

---

# Common Exam Traps

### Trap 1

Question:

Which loading pattern is simplest?

Answer:

Full Load.

---

### Trap 2

Question:

Which loading pattern is most efficient for large datasets?

Answer:

Incremental Load.

---

### Trap 3

Question:

Which technique captures deletes?

Answer:

CDC.

---

### Trap 4

Question:

Does Incremental Load always detect deletes?

Answer:

No. That depends on the implementation. CDC is specifically designed to capture inserts, updates, and deletes.

---

# Memory Tricks

Full Load

= Move the Entire House

---

Incremental Load

= Move Only New Furniture

---

CDC

= Security Camera

Only records what changed.

---

Late-Arriving Data

= Student enters class after attendance.

---
