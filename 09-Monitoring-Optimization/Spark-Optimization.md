# Spark Optimization

> **📖 DP-700 Skill Area:** Monitor and Optimize an Analytics Solution
>
> **⭐ Exam Priority:** ⭐⭐⭐⭐⭐ (Very High)

---

# 📌 What is Spark Optimization?

Spark Optimization is the process of improving the performance and efficiency of Spark applications by reducing execution time, minimizing resource usage, and maximizing parallel processing.

A well-optimized Spark job:

- Runs faster
- Uses less memory
- Uses fewer CPU resources
- Scales efficiently
- Handles large datasets reliably

---

# 🏢 Real-World Analogy

Imagine sorting 10,000 exam papers.

### Method 1

One teacher checks all papers.

❌ Very slow

---

### Method 2

Ten teachers each check 1,000 papers.

✅ Much faster

Spark works the same way by distributing work across multiple executors.

---

# Spark Optimization Goals

The main objectives are:

- Reduce execution time
- Reduce shuffle operations
- Balance workload
- Reduce memory consumption
- Increase parallelism

---

# Partitioning

Spark processes data in partitions.

Example:

```
1,000,000 Rows

↓

4 Partitions

↓

250,000 Rows Each
```

Each partition can be processed in parallel.

Good partitioning improves performance.

---

# Repartition vs Coalesce

Both change the number of partitions, but they work differently.

## Repartition

- Can increase or decrease partitions
- Performs a full shuffle
- Produces balanced partitions

Example:

```python
df = df.repartition(8)
```

Use when you need even distribution.

---

## Coalesce

- Primarily reduces partitions
- Avoids a full shuffle where possible
- Faster than repartition for reducing partitions

Example:

```python
df = df.coalesce(4)
```

Use when reducing partitions before writing data.

---

# Repartition vs Coalesce

| Repartition | Coalesce |
|-------------|----------|
| Increase or decrease partitions | Mostly decrease partitions |
| Causes shuffle | Minimizes shuffle |
| Better balancing | Faster for reducing partitions |

---

# Shuffle Operations

A shuffle occurs when Spark redistributes data between executors.

Example operations:

- GROUP BY
- JOIN
- DISTINCT
- ORDER BY

Shuffles are expensive because they involve:

- Network transfer
- Disk I/O
- Serialization

Reducing unnecessary shuffles improves performance.

---

# Data Skew

Data skew happens when one partition receives significantly more data than others.

Example:

```
Partition 1

100 Rows

Partition 2

120 Rows

Partition 3

95 Rows

Partition 4

950,000 Rows
```

Most executors finish quickly.

One executor continues working.

The entire job waits.

---

# Handling Data Skew

Possible solutions:

- Repartition data
- Use better partition keys
- Filter unnecessary data
- Broadcast small tables where appropriate

Balanced partitions improve performance.

---

# Broadcast Join

Suppose:

Customers Table

10 MB

Sales Table

500 GB

Instead of moving the huge Sales table, Spark broadcasts the small Customers table to every executor.

```
Small Table

↓

Broadcast

↓

Each Executor
```

Benefits:

- Less network traffic
- Faster joins
- Reduced shuffle

Use Broadcast Join only when one table is small.

---

# Caching

Frequently used DataFrames can be cached in memory.

Example:

```python
df.cache()
```

Benefits:

- Faster repeated access
- Reduced recomputation

Drawback:

Consumes memory.

Only cache reused datasets.

---

# Persistence

Persistence is similar to caching but allows different storage levels.

Examples:

- Memory
- Disk
- Memory + Disk

Persistence provides more flexibility than caching.

---

# Lazy Evaluation

Spark does not execute transformations immediately.

Example:

```python
df.filter(...)
df.select(...)
df.groupBy(...)
```

Nothing runs yet.

Execution begins only when an **action** is called.

Examples of actions:

- show()
- collect()
- count()
- write()

This behavior is called **Lazy Evaluation**.

---

# Predicate Pushdown

Suppose a table contains:

10 million rows.

You only need:

```
Region = "South"
```

Instead of loading everything:

Spark pushes the filter down to the storage engine.

Benefits:

- Less data read
- Faster queries
- Lower memory usage

---

# Adaptive Query Execution (AQE)

AQE allows Spark to optimize execution while the query is running.

Spark can:

- Change join strategies
- Merge small partitions
- Handle skew automatically

Benefits:

- Better performance
- Reduced execution time
- More efficient resource usage

---

# Spark UI

Spark UI helps diagnose performance issues.

Useful sections include:

- Jobs
- Stages
- Tasks
- Executors
- SQL
- Storage

Engineers use Spark UI to identify bottlenecks.

---

# Spark Optimization Workflow

```
Slow Spark Job

↓

Open Spark UI

↓

Identify Bottleneck

↓

Check Partitions

↓

Check Shuffle

↓

Optimize

↓

Run Again

↓

Compare Performance
```

---

# Best Practices

✔ Partition large datasets appropriately.

✔ Avoid unnecessary shuffles.

✔ Use Broadcast Joins for small lookup tables.

✔ Cache reused DataFrames.

✔ Filter data early.

✔ Remove unnecessary columns.

✔ Monitor Spark UI regularly.

✔ Avoid excessive collect() operations on large datasets.

✔ Keep transformations simple.

---

# DP-700 Exam Tips

⭐ **Very High Priority**

Remember these common optimizations:

| Problem | Solution |
|---------|----------|
| Too many small partitions | Coalesce |
| Uneven workload | Repartition |
| Small lookup table | Broadcast Join |
| Repeated DataFrame usage | Cache |
| Reads too much data | Predicate Pushdown |
| Runtime optimization | AQE |

---

# Common Mistakes

### ❌ Mistake 1

Using repartition unnecessarily.

It causes expensive shuffles.

---

### ❌ Mistake 2

Caching every DataFrame.

Caching consumes memory.

---

### ❌ Mistake 3

Ignoring data skew.

One overloaded partition can slow the entire Spark job.

---

### ❌ Mistake 4

Calling collect() on very large datasets.

This can overwhelm the driver.

---

# Interview Questions

### Q1. What is the difference between repartition() and coalesce()?

Repartition performs a full shuffle and can increase or decrease partitions.

Coalesce mainly reduces partitions while minimizing shuffle.

---

### Q2. Why are shuffle operations expensive?

Because they involve network communication, disk I/O, and data redistribution.

---

### Q3. When should Broadcast Join be used?

When one table is much smaller than the other.

---

### Q4. What is Lazy Evaluation?

Spark delays execution until an action such as count() or show() is called.

---

### Q5. What is Predicate Pushdown?

Filtering data at the storage layer before it reaches Spark.

---

### Q6. What is Adaptive Query Execution (AQE)?

A Spark feature that optimizes query execution dynamically at runtime.

---

# 🧠 Memory Trick

Remember:

**P-S-B-C-L**

```
P → Partition

S → Shuffle

B → Broadcast

C → Cache

L → Lazy Evaluation
```

When a Spark question says:

> "The job is slow..."

Mentally check:

**P-S-B-C-L**

---