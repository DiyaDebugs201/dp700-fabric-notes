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