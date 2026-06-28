# Microsoft Fabric Pipelines

## What is a Pipeline?

A **Pipeline** is an orchestration service in Microsoft Fabric that automates and coordinates multiple data engineering tasks.

Instead of manually running every step in a data workflow, a pipeline executes them automatically in the correct order.

Think of a pipeline as a **workflow manager**.

Example:

```
Extract Data

↓

Transform Data

↓

Load into Lakehouse

↓

Refresh Semantic Model

↓

Send Notification
```

Each step is executed automatically.

---

# Why Do We Need Pipelines?

In a real-world organization, data engineering involves many repetitive tasks:

- Importing files
- Running notebooks
- Cleaning data
- Loading warehouses
- Refreshing reports
- Sending notifications

Without pipelines, each task would have to be started manually.

Pipelines automate these operations, improving reliability and reducing manual effort.

Benefits include:

- Automation
- Scheduling
- Monitoring
- Error handling
- Reusability
- Integration with multiple Fabric services

---

# What is Orchestration?

**Orchestration** is the process of coordinating multiple tasks so they execute in the correct sequence and at the correct time.

Think of an orchestra:

- Every musician has a role.
- The conductor decides **when** each musician plays.

Similarly:

- Activities perform individual tasks.
- The pipeline controls when each activity runs.

Pipeline = Conductor

Activities = Musicians

---

# Pipeline Architecture

A typical pipeline contains:

```
Pipeline

├── Activities
├── Parameters
├── Variables
├── Triggers
├── Dependencies
├── Monitoring
└── Error Handling
```

Each component has a specific responsibility.

---

# Pipeline Lifecycle

A pipeline generally follows this lifecycle:

```
Design

↓

Configure Activities

↓

Validate

↓

Publish

↓

Trigger

↓

Execute

↓

Monitor

↓

Complete
```

---

# Pipeline Components

## Activities

Activities perform the actual work.

Examples:

- Copy Data
- Notebook
- Dataflow Gen2
- Stored Procedure
- Script
- Web Activity

A pipeline can contain one or many activities.

---

## Parameters

Parameters allow pipelines to receive values at runtime.

Instead of hardcoding values, the same pipeline can process different datasets.

Example:

```
Pipeline Parameter

↓

Input File Name

↓

January.csv

or

February.csv

or

March.csv
```

This improves reusability.

---

## Variables

Variables store values during pipeline execution.

Example:

```
Row Count

↓

Store Value

↓

Use Later
```

Variables are useful for conditions, loops, and logging.

---

## Triggers

Triggers determine **when** a pipeline starts.

Examples:

- Scheduled every night
- Every hour
- When a file arrives
- Manual execution

---

## Dependencies

Dependencies define the relationship between activities.

Example:

```
Copy Data

↓

Success

↓

Run Notebook
```

Notebook starts only after Copy Data succeeds.

---

# Sequential Execution

Activities run one after another.

Example:

```
Copy Data

↓

Notebook

↓

Warehouse Load

↓

Refresh Report
```

Advantages:

- Simple execution
- Easier debugging

Disadvantages:

- Slower if tasks are independent.

---

# Parallel Execution

Independent activities execute simultaneously.

Example:

```
            Pipeline

      ↙       ↓       ↘

Copy Sales  Copy Customer  Copy Product

      ↘       ↓       ↙

      Merge Results
```

Advantages:

- Faster execution
- Better resource utilization

---

# Pipeline Execution Flow

A typical Fabric pipeline:

```
Read CSV

↓

Copy Data

↓

Notebook

↓

Clean Data

↓

Write Delta Table

↓

Stored Procedure

↓

Refresh Semantic Model

↓

Success Notification
```

---

# Publishing a Pipeline

Before a pipeline can be executed by others, it should be published.

Publishing:

- Saves the latest version.
- Makes changes available.
- Enables scheduled execution.

---

# Validation

Fabric validates a pipeline before execution.

Validation checks:

- Missing connections
- Invalid expressions
- Missing parameters
- Activity configuration
- Dependency errors

---

# Pipeline Monitoring

Fabric provides monitoring capabilities for:

- Running pipelines
- Completed pipelines
- Failed activities
- Execution duration
- Retry attempts

Monitoring helps identify issues quickly.

---

# Error Handling

Pipelines should handle failures gracefully.

Common techniques include:

- Retry policies
- Timeout settings
- Failure dependencies
- Logging
- Notifications

Example:

```
Notebook Fails

↓

Retry

↓

Still Fails

↓

Send Email

↓

Stop Pipeline
```

---

# Retry Policies

Transient failures may occur because of:

- Network interruptions
- Temporary storage issues
- Service unavailability

Retry policies automatically rerun failed activities before marking them as failed.

---

# Timeouts

Each activity can define a maximum execution time.

Example:

```
Notebook

↓

Maximum Time

30 Minutes

↓

Stop if exceeded
```

This prevents endless execution.

---

# Manual vs Triggered Execution

## Manual

Started by a user.

Useful for:

- Testing
- Development
- Debugging

---

## Triggered

Started automatically.

Examples:

- Every night
- Every hour
- File uploaded
- Event received

Used in production environments.

---

# Pipeline vs Notebook vs Dataflow Gen2

| Feature | Pipeline | Notebook | Dataflow Gen2 |
|----------|-----------|-----------|----------------|
| Purpose | Orchestration | Data Processing | Visual Transformation |
| Uses Spark | No | Yes | No |
| Visual Interface | Yes | Code | Yes |
| Best For | Workflow Automation | Complex Logic | Low-Code ETL |

---

# Real Fabric Example

Imagine an online shopping company.

Every night:

```
Sales Database

↓

Copy Activity

↓

Lakehouse

↓

Notebook

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

↓

Email Notification
```

Everything runs automatically through one pipeline.

---

# Common DP-700 Scenarios

### Scenario 1

Need to automate an end-to-end ETL process.

**Answer:**

Pipeline.

---

### Scenario 2

Need to run Spark code.

**Answer:**

Notebook Activity inside a Pipeline.

---

### Scenario 3

Need visual transformations.

**Answer:**

Dataflow Gen2.

---

### Scenario 4

Need multiple tasks to run every night.

**Answer:**

Pipeline with a Schedule Trigger.

---

### Scenario 5

Need independent copy operations to run simultaneously.

**Answer:**

Parallel Activities.

---

### Scenario 6

Need one activity to start only after another succeeds.

**Answer:**

Activity Dependency.

---

# Common Exam Traps

### Trap 1

Question:

Does a Pipeline transform data?

Answer:

Not directly.

Activities inside the pipeline perform the transformations.

---

### Trap 2

Question:

Which component orchestrates workflows?

Answer:

Pipeline.

---

### Trap 3

Question:

Which component performs Spark transformations?

Answer:

Notebook.

---

### Trap 4

Question:

Can activities run in parallel?

Answer:

Yes.

If they are independent.

---

### Trap 5

Question:

What starts a pipeline automatically?

Answer:

Trigger.

---

# Memory Tricks

Pipeline

= Project Manager

---

Activity

= Individual Task

---

Trigger

= Start Button

---

Parameter

= User Input

---

Variable

= Temporary Memory

---

Dependency

= Wait for Previous Task

---

Retry

= Try Again

---

Monitor

= Dashboard

---