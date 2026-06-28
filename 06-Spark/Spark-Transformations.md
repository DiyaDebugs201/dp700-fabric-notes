# Spark Performance Optimization

## Why Optimize Spark?

Spark is designed for processing massive datasets, but poor implementation can still result in:

- Slow execution
- High compute costs
- Memory issues
- Long-running notebooks
- Resource bottlenecks

Performance optimization ensures Spark jobs complete faster while using fewer resources.

---

# Common Causes of Poor Performance

- Too many small files
- Poor partitioning
- Unnecessary shuffles
- Reading unnecessary rows or columns
- Expensive joins
- Data skew
- Lack of caching

---

# Partitioning

A partition is a smaller chunk of a dataset processed independently.

Benefits:

- Parallel processing
- Better scalability
- Faster execution

### Too Few Partitions

One executor does most of the work → Slow.

### Too Many Partitions

High scheduling overhead → Slow.

Goal: Balance the number of partitions with available executors.

---

# Repartition vs Coalesce

## repartition()

- Increase or decrease partitions
- Causes a shuffle
- Better data distribution

```python
df = df.repartition(8)
```

## coalesce()

- Mainly reduces partitions
- Minimizes shuffling

```python
df = df.coalesce(4)
```

---

# Caching

Cache stores a DataFrame in memory for reuse.

```python
df.cache()
```

Use when the same DataFrame is referenced multiple times.

Benefits:

- Avoids recomputation
- Faster notebooks

---

# Persist

Provides more storage options than cache.

```python
df.persist()
```

Storage options include:

- Memory
- Disk
- Memory + Disk

---

# Predicate Pushdown

Filter data as early as possible.

Instead of reading all records then filtering, Spark pushes filters to the storage layer.

Benefits:

- Less I/O
- Faster execution

---

# Column Pruning

Read only the required columns.

Instead of:

- CustomerID
- Name
- Address
- Phone
- Sales

Read only:

- CustomerID
- Sales

Benefits:

- Lower memory usage
- Faster scans

---

# Shuffle Operations

A shuffle redistributes data between executors.

Common operations causing shuffles:

- groupBy()
- join()
- distinct()
- orderBy()

Shuffles are expensive because they involve network traffic and disk I/O.

Reduce shuffle by:

- Filtering early
- Selecting required columns
- Using broadcast joins
- Proper partitioning

---

# Broadcast Join

When joining a very large table with a small lookup table, broadcast the small table.

Benefits:

- Avoids shuffling the large table
- Faster joins

Typical example:

Sales (millions of rows)

+

Country lookup (200 rows)

---

# Delta Table Optimization

## OPTIMIZE

Compacts many small files into fewer larger files.

```sql
OPTIMIZE Sales;
```

Benefits:

- Faster scans
- Reduced fragmentation

---

## Z-ORDER

Improves filtering performance.

```sql
OPTIMIZE Sales
ZORDER BY (CustomerID);
```

Use when queries repeatedly filter by the same column.

---

## VACUUM

Deletes obsolete Delta files.

```sql
VACUUM Sales;
```

Important:

VACUUM removes old files—not current table data.

---

## ANALYZE TABLE

Collects table statistics.

```sql
ANALYZE TABLE Sales COMPUTE STATISTICS;
```

Helps the optimizer generate better execution plans.

---

## DESCRIBE HISTORY

Displays Delta transaction history.

```sql
DESCRIBE HISTORY Sales;
```

Useful for:

- Auditing
- Troubleshooting
- Time travel

---

# Data Skew

Occurs when one partition contains much more data than others.

Effects:

- One executor works much longer
- Poor cluster utilization
- Slow jobs

Reduce skew by:

- Better partition keys
- Repartitioning
- Broadcast joins

---

# Spark Optimization Workflow

Read Delta Table

↓

Filter Early

↓

Select Required Columns

↓

Transform

↓

Cache if reused

↓

Write Delta Table

↓

OPTIMIZE

↓

Z-ORDER (if needed)

↓

VACUUM

---

# Common DP-700 Scenarios

## Scenario 1

Repeatedly using the same DataFrame?

**Answer:** `cache()`

---

## Scenario 2

Thousands of tiny Delta files?

**Answer:** `OPTIMIZE`

---

## Scenario 3

Users constantly filter by CustomerID?

**Answer:** `Z-ORDER`

---

## Scenario 4

Need to reclaim storage?

**Answer:** `VACUUM`

---

## Scenario 5

Need better query planning?

**Answer:** `ANALYZE TABLE`

---

## Scenario 6

Need previous versions of a Delta table?

**Answer:** `DESCRIBE HISTORY`

---

## Scenario 7

Joining a massive fact table with a tiny lookup table?

**Answer:** Broadcast Join

---

# Common Exam Traps

| Question | Correct Answer |
|-----------|----------------|
| Does VACUUM delete current records? | No |
| Which command compacts files? | OPTIMIZE |
| Which command improves filtering? | Z-ORDER |
| Which stores DataFrames in memory? | cache() |
| Which operations cause shuffles? | groupBy, join, distinct, orderBy |

---

# Memory Tricks

- **Partition** = Divide work
- **Cache** = Remember
- **Broadcast Join** = Share the small table with everyone
- **OPTIMIZE** = Merge files
- **Z-ORDER** = Organize for searching
- **VACUUM** = Clean old files
- **ANALYZE TABLE** = Gather statistics
- **DESCRIBE HISTORY** = Timeline

---
