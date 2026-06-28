# Pipeline Activities

## What are Pipeline Activities?

A **Pipeline Activity** is an individual task that performs a specific operation within a Microsoft Fabric Pipeline.

Think of a pipeline as a workflow.

Each step inside that workflow is called an **activity**.

Example:

```
Copy Customer Data
        ↓
Clean Data
        ↓
Run Notebook
        ↓
Load to Lakehouse
        ↓
Refresh Power BI Model
```

Each box represents an activity.

---

# Why are Activities Needed?

Instead of manually performing every task:

- Copy files
- Run notebooks
- Transform data
- Load tables
- Send notifications

Fabric automates the entire workflow using activities.

Benefits include:

- Automation
- Reusability
- Scheduling
- Monitoring
- Error handling

---

# Types of Pipeline Activities

Microsoft Fabric provides many built-in activities.

The most important ones for DP-700 are:

| Activity | Purpose |
|-----------|---------|
| Copy Data | Copy data between sources |
| Notebook | Execute Spark notebooks |
| Dataflow Gen2 | Run Power Query transformations |
| Stored Procedure | Execute SQL stored procedures |
| Script | Execute SQL scripts |
| Web Activity | Call REST APIs |
| Wait | Pause execution |
| If Condition | Execute based on a condition |
| Switch | Multiple conditional branches |
| ForEach | Repeat an activity |
| Until | Repeat until a condition is met |
| Set Variable | Store values |
| Append Variable | Add values to arrays |

---

# Copy Data Activity

## Purpose

Copies data from one location to another.

Example:

```
SQL Server

↓

Lakehouse
```

or

```
CSV

↓

Warehouse
```

Supports:

- SQL Server
- Azure SQL
- OneLake
- Blob Storage
- Amazon S3
- Google Cloud Storage
- REST APIs
- SharePoint
- Excel
- CSV

Common use cases:

- Daily data ingestion
- Initial data migration
- Incremental data loading

---

# Notebook Activity

Runs a Microsoft Fabric Spark Notebook.

Used for:

- PySpark transformations
- SQL transformations
- Machine Learning
- Delta Lake processing

Example:

```
Raw Data

↓

Notebook

↓

Silver Table
```

---

# Dataflow Gen2 Activity

Executes a Dataflow Gen2.

Used when:

- Low-code transformations
- Business users
- Power Query transformations

Typical workflow:

```
CSV

↓

Power Query

↓

Lakehouse
```

---

# Stored Procedure Activity

Runs a SQL Stored Procedure.

Example uses:

- Updating dimension tables
- Running SQL logic
- Loading warehouses

Example:

```sql
EXEC UpdateSalesSummary;
```

---

# Script Activity

Executes SQL statements directly.

Example:

```sql
DELETE FROM Sales
WHERE SalesDate < '2024-01-01';
```

Unlike Stored Procedures, the SQL is written directly in the activity.

---

# Web Activity

Calls REST APIs.

Common use cases:

- Trigger external applications
- Send notifications
- Call Azure Functions
- Integrate third-party systems

---

# Wait Activity

Pauses the pipeline for a specified duration.

Example:

```
Copy Data

↓

Wait 60 seconds

↓

Run Notebook
```

Useful when another system needs time to finish processing.

---

# If Condition Activity

Runs activities only if a condition is true.

Example:

```
Rows > 0 ?

Yes

↓

Run Notebook

No

↓

Stop
```

Useful for validation and decision-making.

---

# Switch Activity

Executes different branches based on a value.

Example:

```
Country

↓

India

↓

Pipeline A

US

↓

Pipeline B

UK

↓

Pipeline C
```

Useful when multiple conditions exist.

---

# ForEach Activity

Repeats an activity for every item in a collection.

Example:

```
Files

↓

January.csv

↓

February.csv

↓

March.csv
```

The same activity executes for each file.

---

# Until Activity

Repeats activities until a condition becomes true.

Example:

```
Is File Available?

↓

No

↓

Wait

↓

Check Again

↓

Yes

↓

Continue
```

Useful when waiting for external systems.

---

# Set Variable Activity

Stores a value in a variable.

Example:

```
Current Date

↓

Store in Variable
```

Variables can later be used by other activities.

---

# Append Variable Activity

Adds values to an array variable.

Example:

```
Error List

↓

Add Failed File Name
```

Useful for logging failures.

---

# Sequential Execution

Activities execute one after another.

Example:

```
Copy Data

↓

Notebook

↓

Warehouse Load
```

Each activity waits for the previous one to finish.

---

# Parallel Execution

Multiple activities execute simultaneously.

Example:

```
Copy Sales

↓

Copy Customers

↓

Copy Products
```

All three run together.

Benefits:

- Faster execution
- Better resource utilization

---

# Activity Dependencies

Activities can depend on previous activities.

Dependency types:

- Success
- Failure
- Completion
- Skip

Example:

```
Copy Data

↓

Success

↓

Run Notebook
```

If Copy Data fails, Notebook does not execute.

---

# Retry Policy

Pipelines can automatically retry failed activities.

Example:

Notebook fails because storage is temporarily unavailable.

Retry:

1

↓

2

↓

3

Pipeline succeeds without manual intervention.

---

# Timeout

Each activity can have a timeout.

Example:

Maximum execution:

30 minutes

If exceeded:

Activity fails.

---

# Disable Activity

Activities can be temporarily disabled.

Useful for:

- Testing
- Development
- Troubleshooting

---

# Typical Fabric Pipeline

```
Copy Sales CSV

↓

Dataflow Gen2

↓

Notebook

↓

Write Silver Table

↓

Stored Procedure

↓

Refresh Semantic Model
```

---

# Choosing the Right Activity

| Requirement | Activity |
|--------------|----------|
| Copy data | Copy Data |
| Run PySpark | Notebook |
| Visual transformation | Dataflow Gen2 |
| Execute SQL procedure | Stored Procedure |
| Execute SQL statements | Script |
| Call API | Web |
| Pause execution | Wait |
| Branch on condition | If |
| Multiple conditions | Switch |
| Repeat for list | ForEach |
| Wait until condition | Until |

---

# Common DP-700 Scenarios

### Scenario 1

Need to ingest data from SQL Server every night.

Answer:

Copy Data Activity.

---

### Scenario 2

Need to transform 500 GB of data using PySpark.

Answer:

Notebook Activity.

---

### Scenario 3

Business analyst needs a visual transformation.

Answer:

Dataflow Gen2.

---

### Scenario 4

Need to execute a SQL stored procedure after loading data.

Answer:

Stored Procedure Activity.

---

### Scenario 5

Need to process 50 CSV files.

Answer:

ForEach Activity.

---

### Scenario 6

Need to call a REST API after loading data.

Answer:

Web Activity.

---

### Scenario 7

Need to stop processing if no data exists.

Answer:

If Condition Activity.

---

# Common Exam Traps

### Trap 1

Pipeline copies data.

Answer:

Copy Activity.

---

### Trap 2

Pipeline executes PySpark.

Answer:

Notebook Activity.

---

### Trap 3

Pipeline performs Power Query transformations.

Answer:

Dataflow Gen2.

---

### Trap 4

Need to repeat an activity.

Answer:

ForEach.

---

### Trap 5

Need to pause execution.

Answer:

Wait Activity.

---

# Memory Tricks

Pipeline

= Workflow

---

Activity

= One task

---

Copy

= Move data

---

Notebook

= Spark

---

Dataflow

= Power Query

---

Stored Procedure

= SQL procedure

---

Script

= SQL statements

---

ForEach

= Loop

---

Wait

= Pause

---

If

= Decision

---

Switch

= Multiple decisions

---

Until

= Repeat until done

---