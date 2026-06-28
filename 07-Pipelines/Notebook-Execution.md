# Notebook Execution in Microsoft Fabric Pipelines

## Introduction

Microsoft Fabric allows Spark notebooks to be executed automatically using Pipelines.

Instead of manually opening a notebook and clicking **Run**, a Pipeline can execute the notebook as part of an automated workflow.

Example:

```
Copy Data

↓

Run Notebook

↓

Load Lakehouse

↓

Refresh Semantic Model
```

This enables fully automated ETL and ELT workflows.

---

# Why Execute Notebooks from Pipelines?

Running notebooks inside pipelines provides several benefits:

- Automation
- Repeatability
- Scheduling
- Error handling
- Monitoring
- Integration with other Fabric items

Instead of running notebooks manually every day, a pipeline executes them automatically.

---

# What is a Notebook Activity?

A **Notebook Activity** is a pipeline activity that executes a Microsoft Fabric Spark Notebook.

The notebook can contain:

- PySpark
- Spark SQL
- Python
- DataFrame operations
- Delta Lake operations

The pipeline simply tells Fabric **when** the notebook should run.

---

# Typical Workflow

```
CSV File

↓

Copy Activity

↓

Notebook Activity

↓

Clean Data

↓

Silver Table

↓

Gold Table

↓

Warehouse

↓

Power BI Refresh
```

The Notebook Activity performs the transformation stage.

---

# Notebook Lifecycle

A notebook generally follows these steps:

```
Receive Parameters

↓

Read Data

↓

Transform Data

↓

Validate Data

↓

Write Results

↓

Return Status
```

The pipeline monitors each stage.

---

# Passing Parameters to a Notebook

Pipelines can pass values into notebooks at runtime.

Examples:

- File Name
- Year
- Month
- Table Name
- Environment

Example:

Pipeline Parameter:

```
Year = 2026
```

↓

Notebook receives:

```
2026
```

↓

Notebook processes only 2026 data.

This allows the same notebook to be reused.

---

# Common Parameters

| Parameter | Example |
|------------|----------|
| FileName | Sales.csv |
| Year | 2026 |
| Month | June |
| Country | India |
| TableName | Sales |

---

# Why Use Parameters?

Without parameters:

Notebook A

↓

January

Notebook B

↓

February

Notebook C

↓

March

Many notebooks are required.

With parameters:

One notebook

↓

Receives Month

↓

Processes any month.

---

# Notebook Outputs

A notebook can produce:

- Delta Tables
- DataFrames
- Files
- Logs
- Metrics

Example:

```
Raw Data

↓

Notebook

↓

Silver Table
```

The next activity can continue processing.

---

# Notebook Success

If the notebook finishes successfully:

```
Notebook

↓

Success

↓

Next Activity
```

The pipeline continues.

---

# Notebook Failure

If the notebook fails:

```
Notebook

↓

Failure

↓

Retry

↓

Still Fails

↓

Stop Pipeline
```

Fabric records the failure for troubleshooting.

---

# Retry Policies

Temporary issues may occur due to:

- Network failures
- Storage delays
- Cluster startup delays

Instead of failing immediately:

Notebook

↓

Retry

↓

Retry Again

↓

Success

This increases reliability.

---

# Timeout

Each Notebook Activity can have a timeout.

Example:

Maximum Runtime

```
45 Minutes
```

If exceeded:

Activity fails.

This prevents notebooks from running forever.

---

# Chaining Multiple Notebooks

Large projects often divide processing into multiple notebooks.

Example:

```
Notebook 1

↓

Ingest Data

↓

Notebook 2

↓

Clean Data

↓

Notebook 3

↓

Business Transformations

↓

Notebook 4

↓

Load Gold Tables
```

Advantages:

- Easier maintenance
- Better debugging
- Reusability

---

# Sequential Notebook Execution

```
Notebook A

↓

Notebook B

↓

Notebook C
```

Each notebook waits for the previous notebook to finish.

Use when notebooks depend on previous results.

---

# Parallel Notebook Execution

```
              Pipeline

        ↙       ↓       ↘

Notebook A  Notebook B  Notebook C

        ↘       ↓       ↙

      Merge Results
```

Advantages:

- Faster execution
- Better cluster utilization

Use only when notebooks are independent.

---

# Notebook Dependencies

Notebook execution can depend on:

- Success
- Failure
- Completion

Example:

```
Copy Data

↓

Notebook

↓

Warehouse Load
```

Notebook starts only after data is copied successfully.

---

# Monitoring Notebook Execution

Fabric allows monitoring of:

- Running notebooks
- Completed notebooks
- Failed notebooks
- Execution duration
- Retry attempts
- Logs

Monitoring helps identify bottlenecks and failures.

---

# Logging

Good notebooks should record:

- Start time
- End time
- Rows processed
- Errors
- Warnings
- Execution status

Logging simplifies troubleshooting.

---

# Best Practices

✔ Keep notebooks focused on one responsibility.

✔ Pass values using parameters instead of hardcoding.

✔ Use retries for temporary failures.

✔ Log important information.

✔ Split very large notebooks into smaller notebooks.

✔ Monitor notebook execution regularly.

✔ Validate data before writing output.

---

# Real Fabric Example

Daily Sales Pipeline:

```
Schedule Trigger

↓

Copy Activity

↓

Notebook

↓

Read Bronze

↓

Clean Data

↓

Write Silver

↓

Create Gold

↓

Warehouse

↓

Semantic Model Refresh

↓

Email Notification
```

The notebook performs the transformation while the pipeline orchestrates the overall workflow.

---

# Notebook vs Pipeline

| Notebook | Pipeline |
|-----------|----------|
| Processes data | Orchestrates workflow |
| Runs Spark code | Runs activities |
| Contains transformation logic | Coordinates execution |
| Executes SQL/PySpark | Executes notebooks, copy activities, dataflows, etc. |

Think:

Pipeline = Manager

Notebook = Worker

---

# Common DP-700 Scenarios

### Scenario 1

Need to execute PySpark automatically every night.

**Answer:**

Notebook Activity inside a scheduled pipeline.

---

### Scenario 2

Need to process different monthly files using one notebook.

**Answer:**

Pass the month as a parameter.

---

### Scenario 3

Need notebook B to start only after notebook A finishes.

**Answer:**

Sequential dependency.

---

### Scenario 4

Need three independent notebooks to run simultaneously.

**Answer:**

Parallel execution.

---

### Scenario 5

Notebook occasionally fails due to temporary storage issues.

**Answer:**

Configure retry policies.

---

### Scenario 6

Need to prevent a notebook from running indefinitely.

**Answer:**

Configure a timeout.

---

### Scenario 7

Need to investigate why a notebook failed.

**Answer:**

Use monitoring logs and execution history.

---

# Common Exam Traps

### Trap 1

Question:

Does a pipeline execute Spark code directly?

Answer:

No.

It executes a Notebook Activity, which runs the Spark code.

---

### Trap 2

Question:

How do you reuse one notebook for different inputs?

Answer:

Pass parameters.

---

### Trap 3

Question:

Can multiple notebooks run simultaneously?

Answer:

Yes, if they are independent.

---

### Trap 4

Question:

What controls notebook execution order?

Answer:

Dependencies.

---

### Trap 5

Question:

What should you configure for temporary failures?

Answer:

Retry Policy.

---

# Memory Tricks

Pipeline

= Manager

---

Notebook

= Worker

---

Parameter

= Input

---

Retry

= Try Again

---

Timeout

= Stop After Limit

---

Sequential

= One after another

---

Parallel

= Same time

---

Dependency

= Wait for previous task

---
