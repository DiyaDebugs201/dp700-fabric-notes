# Dynamic Expressions

## Introduction

Imagine a pipeline that always reads:

```
Sales.csv
```

Tomorrow the file becomes:

```
Sales_July.csv
```

Next month:

```
Sales_August.csv
```

Without dynamic expressions, you would have to edit the pipeline every month.

Dynamic expressions allow Microsoft Fabric to generate values while the pipeline is running.

Instead of fixed values:

```
Sales.csv
```

Use:

```
Sales_@{Month}.csv
```

Now the pipeline automatically works for every month.

---

# What are Dynamic Expressions?

A Dynamic Expression is an expression that is evaluated during pipeline execution.

Instead of writing fixed values, you can build values using:

- Parameters
- Variables
- Functions
- Dates
- System values

This makes pipelines reusable and intelligent.

---

# Why Use Dynamic Expressions?

Benefits include:

- Dynamic file names
- Dynamic folder paths
- Dynamic table names
- Dynamic SQL queries
- Conditional logic
- Reusable pipelines

---

# Expression Language

Microsoft Fabric provides an expression language similar to Azure Data Factory.

Expressions begin with:

```
@
```

Example:

```
@pipeline().parameters.FileName
```

This retrieves the FileName parameter.

---

# Referencing Parameters

Suppose a pipeline parameter:

```
FileName

↓

Sales.csv
```

Expression:

```
@pipeline().parameters.FileName
```

Returns:

```
Sales.csv
```

---

# Referencing Variables

Suppose a variable:

```
Status

↓

Completed
```

Expression:

```
@variables('Status')
```

Returns:

```
Completed
```

---

# Referencing System Values

Fabric also provides built-in system values.

Examples:

Current Pipeline Name

```
@pipeline().Pipeline
```

Run ID

```
@pipeline().RunId
```

Current Trigger Time

```
@trigger().scheduledTime
```

These values are automatically generated.

---

# String Concatenation

Concatenation combines multiple values into one string.

Example:

Parameter:

```
Month = June
```

Expression:

```
@concat('Sales_', pipeline().parameters.Month, '.csv')
```

Output:

```
Sales_June.csv
```

---

# Dynamic Folder Paths

Instead of:

```
Files/June/
```

Use:

```
Files/@{Month}/
```

Now the folder changes automatically.

Example:

```
Files/January/

Files/February/

Files/March/
```

---

# Dynamic Table Names

Instead of:

```
Sales2025
```

Build:

```
Sales2026
```

Expression:

```
@concat('Sales', pipeline().parameters.Year)
```

---

# Date Functions

Current UTC Date

```
@utcNow()
```

Example output:

```
2026-06-28T10:00:00Z
```

---

# Formatting Dates

Example:

```
@formatDateTime(utcNow(),'yyyy-MM-dd')
```

Output:

```
2026-06-28
```

Useful for:

- Folder names
- Reports
- File names

---

# Adding Days

Example:

```
@addDays(utcNow(),1)
```

Tomorrow's date.

---

# Subtracting Days

Example:

```
@addDays(utcNow(),-7)
```

Seven days ago.

Useful for incremental loads.

---

# Conditional Expressions

Example:

```
@if(greater(RowCount,0),'Continue','Stop')
```

Meaning:

If rows exist

↓

Continue

Otherwise

↓

Stop

---

# Comparison Functions

Common comparisons:

```
equals()

greater()

less()

greaterOrEquals()

lessOrEquals()
```

These are used inside conditions.

---

# Logical Functions

Useful functions:

```
and()

or()

not()
```

Example:

```
If

Country = India

AND

Rows > 1000

↓

Continue
```

---

# Empty Check

Check whether a value exists.

Example:

```
@empty(variables('FileName'))
```

Returns:

True

or

False

---

# Length Function

Returns the number of characters.

Example:

```
@length('Fabric')
```

Returns:

```
6
```

---

# Replace Function

Example:

```
@replace('Sales.csv','Sales','Orders')
```

Output:

```
Orders.csv
```

---

# Split Function

Example:

```
Sales,Customer,Product
```

Split using comma.

Returns:

```
Sales

Customer

Product
```

---

# Substring

Example:

```
Sales2026.csv
```

Extract:

```
2026
```

Useful for parsing filenames.

---

# Dynamic SQL

Instead of:

```sql
SELECT * FROM Sales
```

Build dynamically:

```sql
SELECT * FROM Sales2026
```

Table name comes from a parameter.

---

# Dynamic File Processing

Parameter:

```
Month

↓

June
```

Expression:

```
Sales_June.csv
```

Tomorrow:

```
Sales_July.csv
```

Pipeline logic stays unchanged.

---

# Dynamic Pipeline Example

Input:

```
Year = 2026

Month = June
```

Pipeline builds:

```
Files/2026/June/Sales.csv
```

Everything is generated dynamically.

---

# Best Practices

Use expressions for:

- File names
- Dates
- Folder paths
- Table names
- Conditions
- Incremental loads

Avoid hardcoding whenever possible.

---

# Common DP-700 Scenarios

### Scenario 1

Need today's date in a filename.

Answer:

```
utcNow()
```

---

### Scenario 2

Need to combine text with a parameter.

Answer:

```
concat()
```

---

### Scenario 3

Need yesterday's date.

Answer:

```
addDays()
```

---

### Scenario 4

Need to check if a variable is empty.

Answer:

```
empty()
```

---

### Scenario 5

Need a dynamic folder path.

Answer:

Use parameters with expressions.

---

### Scenario 6

Need conditional execution.

Answer:

```
if()
```

---

### Scenario 7

Need current pipeline Run ID.

Answer:

System variables.

---

# Common Exam Traps

### Trap 1

Question:

How do expressions begin?

Answer:

```
@
```

---

### Trap 2

Question:

Which function combines strings?

Answer:

```
concat()
```

---

### Trap 3

Question:

Which function returns today's UTC date?

Answer:

```
utcNow()
```

---

### Trap 4

Question:

Which function formats dates?

Answer:

```
formatDateTime()
```

---

### Trap 5

Question:

Which function checks for empty values?

Answer:

```
empty()
```

---

# Memory Tricks

Dynamic Expression

= Build at runtime

---

concat()

= Join text

---

utcNow()

= Current time

---

formatDateTime()

= Pretty date

---

addDays()

= Move forward/backward

---

if()

= Decision

---

variables()

= Runtime memory

---

parameters()

= User input

---

# DP-700 Exam Focus

Know:

- Dynamic Expressions
- Parameters
- Variables
- concat()
- utcNow()
- formatDateTime()
- addDays()
- if()
- equals()
- greater()
- empty()
- Dynamic file paths
- Dynamic table names
- Runtime values

Questions are usually scenario-based, asking which function or expression should be used.

---

# Quick Revision

- Dynamic expressions make pipelines flexible and reusable.
- Expressions start with `@`.
- Use `pipeline().parameters` to access parameters.
- Use `variables()` to access variables.
- `concat()` joins strings.
- `utcNow()` returns the current UTC time.
- `formatDateTime()` formats dates.
- `addDays()` calculates past or future dates.
- `if()` implements conditional logic.
- Dynamic expressions eliminate hardcoded values and support automated, production-ready pipelines.