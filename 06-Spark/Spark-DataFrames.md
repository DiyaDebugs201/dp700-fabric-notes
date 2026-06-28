# Spark DataFrames

## What is a DataFrame?

A DataFrame is the primary data structure in Apache Spark.

It is a distributed table consisting of rows and columns, similar to a SQL table or a Pandas DataFrame, but designed to process massive datasets across multiple machines.

Think:

> DataFrame = Excel Sheet that can be split across many computers.

---

# Why Use DataFrames?

DataFrames provide:

* Distributed processing
* High performance
* SQL-like operations
* Schema support
* Automatic optimization
* Easy integration with Spark SQL

Most Fabric Notebook transformations are performed using DataFrames.

---

# Creating a DataFrame

DataFrames are commonly created by reading data from external sources.

Example:

```python
df = spark.read.csv("Files/sales.csv")
```

Now `df` represents the data stored in the CSV file.

---

# Reading Data

The Spark Session (`spark`) is used to read data.

Common syntax:

```python
df = spark.read.format("<format>").load("<path>")
```

---

# Supported File Formats

Spark supports many file formats.

| Format  | Purpose                        |
| ------- | ------------------------------ |
| CSV     | Comma-separated values         |
| JSON    | Semi-structured data           |
| Parquet | Columnar storage format        |
| Delta   | Transactional Lakehouse tables |
| ORC     | Optimized columnar format      |
| Avro    | Row-based serialization        |

---

# Reading CSV

```python
df = spark.read.csv("Files/customers.csv")
```

With header:

```python
df = spark.read.option("header", True).csv("Files/customers.csv")
```

---

# Reading JSON

```python
df = spark.read.json("Files/customers.json")
```

---

# Reading Parquet

```python
df = spark.read.parquet("Files/customers.parquet")
```

---

# Reading Delta Tables

```python
df = spark.read.format("delta").load("Tables/Sales")
```

Delta is the preferred format in Microsoft Fabric Lakehouses.

---

# Displaying Data

Show records:

```python
df.show()
```

Display schema:

```python
df.printSchema()
```

Count rows:

```python
df.count()
```

Preview data:

```python
display(df)
```

(`display()` is commonly used in Fabric notebooks.)

---

# Selecting Columns

Select one column:

```python
df.select("CustomerName")
```

Multiple columns:

```python
df.select("CustomerName", "Sales")
```

---

# Filtering Rows

Example:

```python
df.filter(df.Sales > 1000)
```

or

```python
df.where("Sales > 1000")
```

---

# Creating New Columns

Example:

```python
df.withColumn("Tax", df.Sales * 0.18)
```

Creates a new calculated column.

---

# Renaming Columns

```python
df.withColumnRenamed("Sales", "TotalSales")
```

---

# Dropping Columns

```python
df.drop("Age")
```

---

# Removing Duplicate Rows

```python
df.dropDuplicates()
```

Useful during data cleansing.

---

# Handling NULL Values

Remove rows containing NULL values:

```python
df.na.drop()
```

Replace NULL values:

```python
df.na.fill(0)
```

Example:

Replace missing sales values with 0.

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

# Writing Data

General syntax:

```python
df.write.format("<format>").save("<path>")
```

---

# Writing Delta Tables

```python
df.write.format("delta").save("Tables/Sales")
```

This is one of the most common operations in Fabric.

---

# Write Modes

| Mode      | Purpose                    |
| --------- | -------------------------- |
| overwrite | Replace existing data      |
| append    | Add new records            |
| ignore    | Skip if destination exists |
| error     | Fail if destination exists |

---

Example:

```python
df.write.mode("overwrite").save("Tables/Sales")
```

---

# DataFrame Lifecycle

Source

↓

Read

↓

Transform

↓

Validate

↓

Write

↓

Lakehouse Table

---

# Typical Fabric Workflow

CSV File

↓

Spark Read

↓

DataFrame

↓

Clean Data

↓

Write Delta Table

↓

Power BI

---

# Advantages of DataFrames

* Distributed
* Optimized
* Easy to use
* Supports SQL
* Works with Delta Lake
* Handles very large datasets

---

# Common DP-700 Scenarios

### Scenario 1

Requirement:

Read a Delta table into Spark.

Answer:

```python
spark.read.format("delta")
```

---

### Scenario 2

Requirement:

Replace existing table contents.

Answer:

```python
mode("overwrite")
```

---

### Scenario 3

Requirement:

Add new records without deleting old ones.

Answer:

```python
mode("append")
```

---

### Scenario 4

Requirement:

Remove duplicate customer records.

Answer:

```python
dropDuplicates()
```

---

### Scenario 5

Requirement:

Handle missing values.

Answer:

```python
na.drop()
```

or

```python
na.fill()
```

---

# Common Exam Traps

### Trap 1

Question:

Which format is preferred for Fabric Lakehouses?

Answer:

Delta.

---

### Trap 2

Question:

Which mode replaces existing data?

Answer:

Overwrite.

---

### Trap 3

Question:

Which mode keeps existing data and adds new records?

Answer:

Append.

---

### Trap 4

Question:

How do you remove duplicate rows?

Answer:

`dropDuplicates()`

---

# Memory Tricks

Read

= Bring data into Spark.

---

Transform

= Clean and modify.

---

Write

= Save results.

---

Append

= Add more.

---

Overwrite

= Replace everything.

---

Delta

= Fabric's preferred storage format.

---