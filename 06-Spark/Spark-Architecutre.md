# Apache Spark Architecture

## What is Apache Spark?

Apache Spark is a distributed data processing engine designed to process large volumes of data quickly across multiple machines.

In Microsoft Fabric, Spark is commonly used for:

* Data ingestion
* Data transformation
* Data cleaning
* Data engineering
* Machine learning
* Batch processing
* Streaming processing

Think:

> Spark = A team of workers solving one big problem together instead of one person doing everything.

---

# Why Do We Need Spark?

Imagine processing:

* 10 KB file → Laptop is enough.
* 10 GB file → May take time.
* 10 TB file → Single computer struggles.
* 100 TB file → Practically impossible on one machine.

Spark divides the work across multiple computers (nodes), allowing them to process data in parallel.

---

# Distributed Computing

Instead of:

One Computer

↓

Processes Everything

Spark uses:

Many Computers

↓

Each processes part of the data

↓

Results are combined

This is called **distributed computing**.

---

# Spark Architecture Overview

Spark Cluster

├── Driver Node
└── Worker Nodes
├── Executor
├── Executor
└── Executor

---

# Driver Node

The Driver is the brain of a Spark application.

Responsibilities:

* Starts the Spark application.
* Creates the execution plan.
* Divides work into tasks.
* Sends tasks to executors.
* Collects results.

Think:

> Driver = Project Manager.

---

# Worker Nodes

Worker nodes perform the actual processing.

Responsibilities:

* Execute assigned tasks.
* Store intermediate results.
* Return results to the Driver.

Think:

> Workers = Employees doing the actual work.

---

# Executors

Executors run inside worker nodes.

Responsibilities:

* Execute tasks.
* Read data.
* Write data.
* Cache data in memory.
* Return results to the Driver.

Think:

> Executors = Workers' hands.

---

# Spark Session

The Spark Session is the entry point for working with Spark.

It allows you to:

* Read data
* Create DataFrames
* Run SQL
* Write data
* Configure Spark

In Fabric Notebooks, a Spark Session is created automatically.

---

# Spark Context

The Spark Context manages communication between the Driver and the Spark Cluster.

It is responsible for:

* Allocating resources
* Scheduling tasks
* Managing executors

Modern Spark applications usually access it through the Spark Session.

---

# DataFrames

Spark primarily processes data using **DataFrames**.

A DataFrame is a distributed table with rows and columns.

Example:

| CustomerID | Name | Sales |
| ---------- | ---- | ----- |
| 101        | Diya | 500   |

Benefits:

* Easy to work with
* Optimized execution
* Supports SQL-like operations

---

# Partitions

A partition is a smaller piece of a dataset.

Instead of processing one huge file:

100 GB File

↓

Split into 10 partitions

↓

Each executor processes one partition simultaneously.

Benefits:

* Parallel processing
* Faster execution
* Better scalability

---

# Parallel Processing

Spark processes multiple partitions at the same time.

Example:

8 partitions

↓

8 executors

↓

All processed simultaneously.

This significantly reduces processing time.

---

# Lazy Evaluation

Spark does not execute transformations immediately.

Instead, it builds an execution plan and waits until an **action** is called.

Example:

```python
df.filter(...)
  .select(...)
  .groupBy(...)
```

No processing happens yet.

When an action like `.show()` or `.count()` is called, Spark executes the entire plan.

Benefits:

* Optimized execution
* Reduced unnecessary work
* Better performance

---

# Transformations vs Actions

## Transformations

Create a new DataFrame without executing immediately.

Examples:

* filter()
* select()
* join()
* groupBy()
* withColumn()

Lazy.

---

## Actions

Trigger actual execution.

Examples:

* show()
* collect()
* count()
* write()

Immediate.

---

# Spark in Microsoft Fabric

Common workflow:

Data Source

↓

Lakehouse

↓

Spark Notebook

↓

Transform DataFrame

↓

Write Delta Table

↓

Power BI

---

# Advantages of Spark

* Distributed processing
* High performance
* Fault tolerant
* Handles very large datasets
* Supports batch and streaming
* Integrates with Delta Lake

---

# Common DP-700 Scenarios

### Scenario 1

Requirement:

Process 500 GB of data efficiently.

Answer:

Spark distributes the workload across executors.

---

### Scenario 2

Requirement:

Clean millions of records before loading into Silver tables.

Answer:

Spark Notebook.

---

### Scenario 3

Requirement:

Improve processing speed.

Answer:

Increase parallelism through partitions.

---

### Scenario 4

Requirement:

Run SQL and PySpark in the same notebook.

Answer:

Spark Session supports both.

---

# Common Exam Traps

### Trap 1

Question:

Who coordinates the Spark application?

Answer:

Driver Node.

---

### Trap 2

Question:

Who executes tasks?

Answer:

Executors.

---

### Trap 3

Question:

What enables parallel processing?

Answer:

Partitions.

---

### Trap 4

Question:

Do transformations execute immediately?

Answer:

No.

They are lazily evaluated until an action is performed.

---

# Memory Tricks

Driver

= Team Leader

---

Worker

= Office

---

Executor

= Employee

---

Partition

= Divide the work

---

Transformation

= Plan

---

Action

= Execute

---

Spark Session

= Main entrance into Spark

---