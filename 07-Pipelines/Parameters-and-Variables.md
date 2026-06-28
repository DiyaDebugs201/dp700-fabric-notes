# Pipeline Parameters and Variables

## Introduction

Real-world data engineering pipelines rarely process the same data every day.

Examples:

- January.csv today
- February.csv tomorrow
- March.csv next month

Instead of creating three different pipelines, Microsoft Fabric allows us to create one reusable pipeline using **Parameters** and **Variables**.

Think:

> Parameters = Input values provided before the pipeline starts.

> Variables = Values created or modified while the pipeline is running.

---

# Why Use Parameters and Variables?

Without them:

Pipeline A → January.csv

Pipeline B → February.csv

Pipeline C → March.csv

This creates unnecessary duplication.

With parameters:

One Pipeline

↓

Input File Name

↓

Process Any File

The same pipeline can now process any dataset.

Benefits:

- Reusability
- Flexibility
- Easier maintenance
- Less duplicated work

---

# Parameters

## What are Parameters?

Parameters are values passed into a pipeline **before execution begins**.

Once the pipeline starts, parameter values remain constant.

Think of a parameter as an argument passed to a function in programming.

Example:

```
Pipeline Parameter

FileName

↓

Sales_January.csv
```

Tomorrow:

```
FileName

↓

Sales_February.csv
```

The pipeline logic remains unchanged.

---

# Characteristics of Parameters

- Set before execution.
- Read-only during execution.
- Used for dynamic pipelines.
- Can be referenced by activities.

---

# Common Parameter Examples

| Parameter | Example Value |
|-----------|---------------|
| FileName | Sales.csv |
| Folder | Bronze |
| Country | India |
| Year | 2026 |
| Month | June |
| Lakehouse | SalesLakehouse |

---

# Why Parameters are Useful

Instead of:

```text
Read Files/January.csv
```

Use:

```text
Read Files/@FileName
```

Now the pipeline works with any file.

---

# Variables

## What are Variables?

Variables store values during pipeline execution.

Unlike parameters, variables **can change** as the pipeline runs.

Think:

Parameter

↓

Input

↓

Never changes

Variable

↓

Temporary memory

↓

Can change many times

---

# Characteristics of Variables

- Created inside the pipeline.
- Can be updated.
- Used in conditions and loops.
- Can store intermediate values.

---

# Common Variable Examples

| Variable | Purpose |
|-----------|----------|
| RowCount | Number of records processed |
| CurrentFile | Current file being processed |
| RetryCount | Number of retries |
| ErrorMessage | Failure reason |
| Status | Success / Failed |

---

# Parameter vs Variable

| Feature | Parameter | Variable |
|----------|-----------|----------|
| Set Before Execution | Yes | No |
| Can Change | No | Yes |
| Read Only | Yes | No |
| Used as Input | Yes | Yes |
| Temporary Storage | No | Yes |

---

# Example

Suppose today's input file is:

Sales_March.csv

Parameter:

```
FileName

↓

Sales_March.csv
```

Pipeline starts.

During execution:

Variable:

```
RowsProcessed

↓

0

↓

1500

↓

5000

↓

10000
```

The variable changes as work progresses.

---

# Set Variable Activity

Used to assign a value to a variable.

Example:

```
Status

↓

Running
```

Later:

```
Status

↓

Completed
```

---

# Append Variable Activity

Adds values to an array variable.

Example:

```
Failed Files

↓

January.csv

↓

February.csv

↓

March.csv
```

Useful for logging.

---

# Using Parameters in Activities

Example:

Copy Activity

Instead of:

```
Files/Sales.csv
```

Use:

```
Files/@pipeline().parameters.FileName
```

Now the source file becomes dynamic.

---

# Using Variables

Suppose:

Current Retry Count

↓

RetryCount

Each retry updates:

0

↓

1

↓

2

↓

3

---

# Parameters in Notebooks

A Notebook Activity can receive parameters from a pipeline.

Pipeline:

```
Year = 2026
```

Notebook:

Receives:

```
2026
```

The notebook processes only data for that year.

---

# Parameters in Copy Activity

Source:

```
Files/@pipeline().parameters.FileName
```

Destination:

```
Tables/@pipeline().parameters.TableName
```

The same Copy Activity works for many datasets.

---

# Variables with Conditions

Example:

```
RowCount

↓

0 ?
```

If yes:

Send Notification

Otherwise:

Continue Processing

---

# Variables in Loops

Example:

ForEach

↓

Current File

↓

Store in Variable

↓

Process File

↓

Next File

---

# Real Fabric Example

Suppose a company receives one sales file every day.

Pipeline Parameter:

```
FileName
```

Input:

```
Sales_2026_06_20.csv
```

Pipeline:

```
Copy Activity

↓

Notebook

↓

Warehouse

↓

Refresh Report
```

Tomorrow only the parameter changes.

No new pipeline is needed.

---

# Best Practices

## Use Parameters For

- File names
- Folder paths
- Dates
- Country names
- Lakehouse names
- Table names

These values change between executions.

---

## Use Variables For

- Counters
- Row counts
- Status
- Error messages
- Retry attempts
- Intermediate values

These values change during execution.

---

# Common DP-700 Scenarios

### Scenario 1

Need one pipeline to process different monthly files.

Answer:

Pipeline Parameter.

---

### Scenario 2

Need to count processed records.

Answer:

Variable.

---

### Scenario 3

Need to store an execution status.

Answer:

Variable.

---

### Scenario 4

Need to pass a file name into a Notebook.

Answer:

Parameter.

---

### Scenario 5

Need to maintain a list of failed files.

Answer:

Append Variable Activity.

---

### Scenario 6

Need to reuse one Copy Activity for many files.

Answer:

Parameter.

---

# Common Exam Traps

### Trap 1

Question:

Can a parameter change during execution?

Answer:

No.

---

### Trap 2

Question:

Can a variable change?

Answer:

Yes.

---

### Trap 3

Question:

Which is better for file names?

Answer:

Parameter.

---

### Trap 4

Question:

Which stores retry counts?

Answer:

Variable.

---

### Trap 5

Question:

Which activity changes variable values?

Answer:

Set Variable Activity.

---

# Memory Tricks

Parameter

= Input

---

Variable

= Memory

---

Set Variable

= Assign value

---

Append Variable

= Add to list

---

Parameter

= Fixed

---

Variable

= Flexible

---