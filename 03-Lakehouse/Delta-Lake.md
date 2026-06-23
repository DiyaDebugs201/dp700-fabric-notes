# Delta Lake

## What is Delta Lake?

Delta Lake is an open-source storage layer that adds reliability, performance, and transactional capabilities to data stored in a Lakehouse.

In Microsoft Fabric, Lakehouse tables are typically stored as Delta Tables.

Think:

> Delta Lake = Data Lake + Database Reliability

---

## Why Delta Lake Exists

Traditional data lakes have several challenges:

* No transactions
* Poor data consistency
* Difficult updates and deletes
* No version history
* Concurrent write issues

Delta Lake solves these problems.

---

## Key Features of Delta Lake

### ACID Transactions

Delta Lake supports ACID properties.

#### Atomicity

A transaction either completes fully or fails completely.

No partial updates.

---

#### Consistency

Data remains valid before and after a transaction.

---

#### Isolation

Multiple users can work simultaneously without corrupting data.

---

#### Durability

Once committed, data remains stored even after failures.

---

## Time Travel

One of the most powerful Delta Lake features.

Allows querying previous versions of a table.

Example:

Version 1 → Original Data

Version 2 → Updated Data

Version 3 → New Records Added

You can access earlier versions when needed.

---

## Version History

Every change creates a new table version.

Benefits:

* Auditing
* Recovery
* Debugging
* Historical analysis

---

## Schema Enforcement

Prevents invalid data from being written.

Example:

Expected:

CustomerID = Integer

Incoming:

CustomerID = Text

Delta Lake can reject invalid records.

---

## Schema Evolution

Allows table structure to change over time.

Example:

Original Table:

CustomerID
Name

Later:

CustomerID
Name
Email

Delta Lake can accommodate changes when configured.

---

## Delta Tables

Delta Tables are tables stored using the Delta format.

Benefits:

* Reliable
* Query optimized
* Transactional
* Scalable

Most Fabric Lakehouse tables are Delta Tables.

---

## Delta Log

Every Delta Table contains a transaction log.

Purpose:

Track:

* Inserts
* Updates
* Deletes
* Schema changes

Think:

> Delta Log = Table's Audit Trail

---

## Common Operations

### Insert

Add new records.

---

### Update

Modify existing records.

---

### Delete

Remove records.

---

### Merge

Combine insert and update operations.

Often used in:

* Incremental loading
* Slowly Changing Dimensions

---

## Performance Optimization

### OPTIMIZE

Compacts small files into larger files.

Benefits:

* Faster queries
* Better performance

Example:

Many small files
↓
OPTIMIZE
↓
Fewer large files

---

### Z-ORDER

Improves data layout for filtering.

Useful when queries frequently filter specific columns.

Example:

Filter by:

CustomerID

Region

Date

Z-ORDER helps related data stay physically close together.

Benefits:

* Faster query execution
* Reduced data scanning

---

### VACUUM

Removes obsolete files no longer needed.

Benefits:

* Frees storage
* Cleans old file versions

Important:

VACUUM does NOT delete active data.

It removes old files that are no longer referenced.

---

## Delta Lake in Fabric

Common workflow:

Raw Files
↓
Lakehouse
↓
Delta Tables
↓
SQL Analytics
↓
Power BI

---

## Delta Lake and Medallion Architecture

Bronze
↓
Silver
↓
Gold

Each layer commonly stores data as Delta Tables.

Benefits:

* Versioning
* Reliability
* Performance

---

## Common DP-700 Scenarios

### Scenario 1

Requirement:

Recover a previous version of a table.

Solution:

Time Travel.

---

### Scenario 2

Requirement:

Improve query performance.

Solution:

OPTIMIZE.

---

### Scenario 3

Requirement:

Speed up filtering on specific columns.

Solution:

Z-ORDER.

---

### Scenario 4

Requirement:

Remove old unused files.

Solution:

VACUUM.

---

## Common Exam Traps

### Trap 1

Question:

Does VACUUM remove current data?

Answer:

No.

It removes obsolete files.

---

### Trap 2

Question:

Which feature allows historical access?

Answer:

Time Travel.

---

### Trap 3

Question:

Which feature improves query performance by reorganizing files?

Answer:

OPTIMIZE.

---

### Trap 4

Question:

Which feature improves filtering performance?

Answer:

Z-ORDER.

---

## Memory Tricks

ACID

A = Atomicity

C = Consistency

I = Isolation

D = Durability

---

OPTIMIZE

= Combine Files

---

Z-ORDER

= Organize Data

---

VACUUM

= Clean Garbage

---

Time Travel

= Go Back in Time

---