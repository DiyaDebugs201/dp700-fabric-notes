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
# Spark Transformations

## What are Spark Transformations?

Transformations are operations that modify a DataFrame and produce a new DataFrame.

Spark transformations are **lazy**, meaning they do not execute immediately. Spark builds an execution plan and only performs the work when an action (such as `show()` or `count()`) is called.

Think:

> Raw Data → Transform → Clean Data → Analytics

---

# Types of Transformations

Some common transformations include:

- select()
- filter()
- where()
- withColumn()
- withColumnRenamed()
- drop()
- dropDuplicates()
- distinct()
- join()
- groupBy()
- agg()
- union()

---

# Selecting Columns

Used to retrieve only the required columns.

Example:

```python
df.select("CustomerName", "Sales")
```

Useful when you don't need every column in a dataset.

---

# Filtering Rows

Used to retrieve rows matching a condition.

Example:

```python
df.filter(df.Sales > 1000)
```

or

```python
df.where("Sales > 1000")
```

Example:

Retrieve customers whose sales exceed ₹1000.

---

# Creating New Columns

Use `withColumn()`.

Example:

```python
df.withColumn("GST", df.Sales * 0.18)
```

Creates a calculated column.

---

# Renaming Columns

```python
df.withColumnRenamed("Sales", "TotalSales")
```

Useful for improving readability.

---

# Dropping Columns

```python
df.drop("Age")
```

Removes unnecessary columns.

---

# Removing Duplicate Rows

```python
df.dropDuplicates()
```

Useful when multiple records contain identical values.

---

# Distinct Values

```python
df.select("City").distinct()
```

Returns only unique values.

Example:

Cities:

Mumbai

Delhi

Delhi

Bengaluru

Result:

Mumbai

Delhi

Bengaluru

---

# Sorting Data

Ascending:

```python
df.orderBy("Sales")
```

Descending:

```python
df.orderBy(df.Sales.desc())
```

---

# Grouping Data

Use `groupBy()` to group similar records.

Example:

```python
df.groupBy("Department")
```

Usually combined with aggregations.

---

# Aggregation Functions

Aggregation functions summarize grouped data into meaningful values.

### Common Aggregation Functions

| Function | Purpose | Example |
|----------|----------|---------|
| sum() | Calculates total | Total Sales |
| avg() | Calculates average | Average Salary |
| count() | Counts records | Number of Employees |
| max() | Finds highest value | Highest Sale |
| min() | Finds lowest value | Lowest Salary |

Example:

```python
df.groupBy("Department").sum("Sales")
```

Average:

```python
df.groupBy("Department").avg("Sales")
```

Count:

```python
df.groupBy("Department").count()
```

Maximum:

```python
df.groupBy("Department").max("Sales")
```

Minimum:

```python
df.groupBy("Department").min("Sales")
```

---

# Aggregation with agg()

The `agg()` function allows multiple aggregations in a single operation.

Example:

```python
from pyspark.sql.functions import sum, avg, max

df.groupBy("Department").agg(
    sum("Sales").alias("Total Sales"),
    avg("Sales").alias("Average Sales"),
    max("Sales").alias("Highest Sale")
)
```

---

# Joins

Joins combine data from multiple DataFrames.

Example:

Customers

+

Orders

↓

Combined Data

---

## Inner Join

Returns only matching rows.

```python
df1.join(df2, "CustomerID", "inner")
```

Example:

Customers:

| CustomerID | Name |
|------------|------|
| 1 | Alice |
| 2 | Bob |

Orders:

| CustomerID | Order |
|------------|-------|
| 1 | Laptop |
| 3 | Phone |

Result:

| CustomerID | Name | Order |
|------------|------|-------|
| 1 | Alice | Laptop |

---

## Left Join

Returns every row from the left DataFrame.

Matching values are added from the right DataFrame.

```python
df1.join(df2, "CustomerID", "left")
```

---

## Right Join

Returns every row from the right DataFrame.

```python
df1.join(df2, "CustomerID", "right")
```

---

## Full Outer Join

Returns all rows from both DataFrames.

Missing values become NULL.

```python
df1.join(df2, "CustomerID", "outer")
```

---

# Union

Combines two DataFrames vertically.

Example:

January Sales

+

February Sales

↓

Combined Sales

```python
df1.union(df2)
```

Both DataFrames should have the same schema.

---

# Distinct vs dropDuplicates()

### distinct()

Removes duplicate rows from the entire DataFrame.

```python
df.distinct()
```

---

### dropDuplicates()

Removes duplicate rows based on selected columns.

Example:

```python
df.dropDuplicates(["CustomerID"])
```

Useful when only specific columns determine uniqueness.

---

# Window Functions

Window functions perform calculations across related rows while keeping every row in the output.

Unlike `groupBy()`, they do **not** collapse rows.

---

## Why Use Window Functions?

Window functions are useful when you need:

- Ranking
- Previous row values
- Next row values
- Running totals
- Moving averages

without losing individual records.

---

## row_number()

Assigns a unique sequential number.

Example:

| Sales | Row Number |
|--------|------------|
| 900 | 1 |
| 800 | 2 |
| 800 | 3 |

Even duplicate values receive different numbers.

Example:

```python
from pyspark.sql.window import Window
from pyspark.sql.functions import row_number

windowSpec = Window.orderBy("Sales")

df.withColumn(
    "RowNumber",
    row_number().over(windowSpec)
)
```

---

## rank()

Assigns the same rank to equal values but skips numbers afterward.

Example:

Scores:

100

90

90

80

Ranks:

1

2

2

4

Notice Rank **3** is skipped.

---

## dense_rank()

Assigns the same rank to equal values without leaving gaps.

Scores:

100

90

90

80

Dense Rank:

1

2

2

3

This is commonly tested in DP-700.

---

## lag()

Returns the previous row's value.

Example:

| Month | Sales | Previous Month |
|--------|-------|----------------|
| Jan | 100 | NULL |
| Feb | 120 | 100 |
| Mar | 150 | 120 |

Useful for trend analysis.

---

## lead()

Returns the next row's value.

Example:

| Month | Sales | Next Month |
|--------|-------|------------|
| Jan | 100 | 120 |
| Feb | 120 | 150 |
| Mar | 150 | NULL |

Useful for forecasting and comparisons.

---

# Running Total Example

Window functions can calculate cumulative totals.

Example:

| Month | Sales | Running Total |
|--------|-------|---------------|
| Jan | 100 | 100 |
| Feb | 200 | 300 |
| Mar | 150 | 450 |

---

# SQL vs PySpark

Spark:

```python
df.filter(df.Sales > 1000)
```

SQL:

```sql
SELECT *
FROM Sales
WHERE Sales > 1000;
```

Spark:

```python
df.groupBy("Department").sum("Sales")
```

SQL:

```sql
SELECT Department,
SUM(Sales)
FROM Sales
GROUP BY Department;
```

---

# Typical Transformation Workflow

CSV File

↓

Read into DataFrame

↓

Handle NULL Values

↓

Remove Duplicates

↓

Join Customer Table

↓

Calculate GST

↓

Group by Region

↓

Aggregate Sales

↓

Write Delta Table

---

# Real Fabric Example

Raw Sales CSV

↓

Spark Notebook

↓

dropDuplicates()

↓

Fill NULL values

↓

Join Customer Table

↓

Calculate Revenue

↓

Write Silver Delta Table

↓

Power BI Dashboard

---

# Common DP-700 Scenarios

### Scenario 1

Requirement:

Calculate total sales department-wise.

Answer:

`groupBy()` + `sum()`

---

### Scenario 2

Requirement:

Merge Customer and Orders tables.

Answer:

`join()`

---

### Scenario 3

Requirement:

Combine January and February sales.

Answer:

`union()`

---

### Scenario 4

Requirement:

Assign ranking without gaps.

Answer:

`dense_rank()`

---

### Scenario 5

Requirement:

Retrieve previous month's sales.

Answer:

`lag()`

---

### Scenario 6

Requirement:

Retrieve next month's forecast.

Answer:

`lead()`

---

### Scenario 7

Requirement:

Remove duplicate customer records.

Answer:

`dropDuplicates()`

---

### Scenario 8

Requirement:

Find unique cities.

Answer:

`distinct()`

---

# Common Exam Traps

### Trap 1

Question:

Difference between `rank()` and `dense_rank()`?

Answer:

- `rank()` skips numbers after ties.
- `dense_rank()` does not.

---

### Trap 2

Question:

Does `groupBy()` return every row?

Answer:

No.

It summarizes data.

---

### Trap 3

Question:

Which function combines tables horizontally?

Answer:

`join()`

---

### Trap 4

Question:

Which function combines tables vertically?

Answer:

`union()`

---

### Trap 5

Question:

Which function removes duplicate rows?

Answer:

`dropDuplicates()`

---

### Trap 6

Question:

Which function returns previous-row values?

Answer:

`lag()`

---

### Trap 7

Question:

Which function returns next-row values?

Answer:

`lead()`

---

# Memory Tricks

select()

= Choose columns

---

filter()

= Choose rows

---

groupBy()

= Create groups

---

sum()

= Total

---

avg()

= Average

---

join()

= Connect tables

---

union()

= Stack tables

---

distinct()

= Unique values

---

dropDuplicates()

= Remove repeated records

---

row_number()

= Always unique

---

rank()

= Skips numbers

---

dense_rank()

= No skipped numbers

---

lag()

= Previous

---

lead()

= Next

---

# DP-700 Exam Focus

Know:

- select()
- filter()
- where()
- withColumn()
- groupBy()
- agg()
- join()
- union()
- distinct()
- dropDuplicates()
- Window functions
- Aggregation functions
- SQL vs PySpark equivalents

These are among the most frequently used operations in Spark notebooks and are commonly tested in scenario-based questions.

---

# Quick Revision

- Transformations create new DataFrames.
- Transformations are lazy and execute only after an action.
- `select()` retrieves columns.
- `filter()` and `where()` retrieve rows.
- `withColumn()` creates calculated columns.
- `groupBy()` groups records before aggregation.
- `agg()` performs multiple aggregations together.
- `join()` combines DataFrames horizontally.
- `union()` combines DataFrames vertically.
- `distinct()` returns unique rows.
- `dropDuplicates()` removes duplicate records.
- `row_number()` always assigns unique numbers.
- `rank()` skips numbers after ties.
- `dense_rank()` does not skip numbers.
- `lag()` returns previous-row values.
- `lead()` returns next-row values.
- Spark transformations are fundamental for data engineering in Microsoft Fabric.