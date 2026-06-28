# Pipeline Best Practices

## Introduction

Building a pipeline that works is only the first step.

A good Data Engineer builds pipelines that are:

- Reliable
- Reusable
- Scalable
- Easy to maintain
- Easy to monitor
- Easy to troubleshoot

Microsoft Fabric provides many features that help achieve these goals.

---

# Design Small, Modular Pipelines

Avoid creating one massive pipeline that performs every task.

Instead of:

```
Pipeline

↓

50 Activities
```

Break work into logical units.

Example:

```
Pipeline 1

↓

Ingestion

↓

Pipeline 2

↓

Transformation

↓

Pipeline 3

↓

Reporting
```

Benefits:

- Easier debugging
- Easier maintenance
- Better reusability

---

# Keep Activities Focused

Each activity should have one responsibility.

Good:

```
Copy Data
```

↓

```
Notebook
```

↓

```
Refresh Report
```

Avoid activities that attempt to perform many unrelated tasks.

---

# Use Parameters Instead of Hardcoding

Avoid:

```
Sales_January.csv
```

Instead:

```
@pipeline().parameters.FileName
```

Benefits:

- One pipeline for many datasets
- Easier maintenance
- Better scalability

---

# Use Variables Carefully

Variables should store temporary runtime information.

Examples:

- Current file
- Status
- Retry count
- Row count

Avoid using variables for values that never change.

Those belong in parameters.

---

# Choose the Right Activity

| Requirement | Best Activity |
|-------------|---------------|
| Copy data | Copy Activity |
| Spark processing | Notebook |
| Low-code transformation | Dataflow Gen2 |
| SQL procedure | Stored Procedure |
| REST API | Web Activity |
| Wait | Wait Activity |

Choosing the correct activity simplifies the pipeline.

---

# Minimize Pipeline Complexity

Too many nested conditions make pipelines difficult to understand.

Prefer:

Simple

↓

Readable

↓

Maintainable

Instead of deeply nested logic.

---

# Run Independent Activities in Parallel

Instead of:

```
Copy Sales

↓

Copy Customer

↓

Copy Product
```

Run them together.

```
Copy Sales

Copy Customer

Copy Product
```

Advantages:

- Faster execution
- Better resource utilization

Only use parallel execution when activities are independent.

---

# Use Sequential Execution for Dependencies

Example:

```
Copy Data

↓

Notebook

↓

Warehouse Load
```

Each step depends on the previous one.

Sequential execution guarantees correct order.

---

# Validate Inputs

Before processing:

Check:

- File exists
- Correct schema
- Required columns
- File size
- Data quality

Fail early if validation fails.

---

# Handle Errors Gracefully

Never assume every activity succeeds.

Use:

- Retry policies
- Failure paths
- Logging
- Notifications

Example:

```
Notebook

↓

Failure

↓

Retry

↓

Email

↓

Stop Pipeline
```

---

# Configure Retry Policies

Temporary failures happen.

Examples:

- Network interruption
- Storage delay
- Cluster startup delay

Retries often solve these issues automatically.

Avoid excessive retries that may waste resources.

---

# Configure Timeouts

Every long-running activity should have a timeout.

Example:

```
Notebook

Maximum:

30 Minutes
```

If exceeded:

Fail the activity.

This prevents pipelines from hanging indefinitely.

---

# Log Important Information

Record:

- Pipeline start time
- End time
- Rows processed
- Activity duration
- Errors
- Warnings

Good logging makes troubleshooting much easier.

---

# Monitor Pipelines Regularly

Use Fabric monitoring tools to review:

- Running pipelines
- Failed pipelines
- Long-running activities
- Retry attempts
- Performance trends

Monitoring should be continuous, not only after failures.

---

# Avoid Duplicate Data Loads

Design pipelines to support:

- Incremental loading
- Watermarks
- Change detection

Avoid loading the entire dataset unless necessary.

---

# Optimize Data Movement

Only move data when required.

Prefer:

```
Shortcut

↓

Read Directly
```

Instead of repeatedly copying the same data.

---

# Secure Your Pipelines

Apply the principle of least privilege.

Grant only the permissions required.

Protect:

- Connections
- Credentials
- Sensitive data
- Output locations

---

# Use Naming Conventions

Consistent names improve readability.

Examples:

```
PL_LoadSales

NB_CleanSales

DF_SalesTransform
```

Avoid names such as:

```
Pipeline1

Notebook2

Test123
```

---

# Document Your Pipelines

Maintain documentation for:

- Purpose
- Inputs
- Outputs
- Parameters
- Dependencies
- Owner

Documentation helps future maintenance.

---

# Real Fabric Example

Nightly Sales Pipeline

```
Schedule Trigger

↓

Copy Activity

↓

Notebook

↓

Validate Data

↓

Write Silver

↓

Write Gold

↓

Warehouse

↓

Refresh Semantic Model

↓

Send Notification
```

The pipeline is:

- Automated
- Parameterized
- Monitored
- Logged
- Reusable

---

# Choosing the Right Tool

| Requirement | Recommended Tool |
|--------------|------------------|
| Workflow automation | Pipeline |
| Spark transformations | Notebook |
| Low-code ETL | Dataflow Gen2 |
| SQL analytics | Warehouse |
| Large-scale storage | Lakehouse |

Always choose the simplest tool that meets the requirement.

---

# Common DP-700 Scenarios

### Scenario 1

Need one pipeline for every month.

Answer:

Use parameters.

---

### Scenario 2

Need to process three independent datasets.

Answer:

Parallel execution.

---

### Scenario 3

Need notebook execution after data copy.

Answer:

Sequential dependency.

---

### Scenario 4

Need automatic recovery from temporary failures.

Answer:

Retry policy.

---

### Scenario 5

Need to stop activities running indefinitely.

Answer:

Timeout.

---

### Scenario 6

Need easier maintenance.

Answer:

Create modular pipelines.

---

### Scenario 7

Need reusable ETL processes.

Answer:

Parameterized pipelines.

---

# Common Exam Mistakes

❌ Hardcoding file names

✔ Use parameters.

---

❌ Loading full datasets unnecessarily

✔ Use incremental loads.

---

❌ One huge pipeline

✔ Modular pipelines.

---

❌ Ignoring monitoring

✔ Monitor every production pipeline.

---

❌ Running dependent tasks in parallel

✔ Use sequential execution.

---

# Memory Tricks

Pipeline

= Manager

---

Parameter

= Input

---

Variable

= Temporary Memory

---

Retry

= Try Again

---

Timeout

= Stop Limit

---

Parallel

= Faster

---

Sequential

= Dependency

---

Logging

= Evidence

---

Monitoring

= Health Check

---
