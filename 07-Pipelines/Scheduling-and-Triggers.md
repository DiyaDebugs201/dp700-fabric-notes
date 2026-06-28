# Scheduling and Triggers

## Introduction

Imagine a company that receives sales data every night at **2:00 AM**.

The company wants to:

- Copy the data
- Clean the data
- Load the Lakehouse
- Refresh reports

Doing this manually every night is inefficient.

Microsoft Fabric solves this problem using **Triggers**.

A **Trigger** automatically starts a pipeline when a specific condition is met.

---

# What is a Trigger?

A Trigger is an event or schedule that starts a pipeline execution.

Think of it as the **Start button** for a pipeline.

Without a trigger:

Pipeline waits.

With a trigger:

Pipeline starts automatically.

---

# Why are Triggers Important?

Triggers enable:

- Automation
- Scheduled execution
- Event-driven processing
- Reduced manual work
- Reliable production workflows

---

# Types of Triggers

Microsoft Fabric primarily supports:

- Manual Trigger
- Schedule Trigger
- Event-Based Trigger

Each trigger serves a different purpose.

---

# Manual Trigger

A user starts the pipeline manually.

Example:

```
Click

↓

Run Pipeline
```

Used for:

- Testing
- Development
- Debugging
- One-time executions

Advantages:

- Full control
- Easy to test

Disadvantages:

- Requires user intervention

---

# Schedule Trigger

Runs a pipeline at a predefined time.

Example:

```
Every Day

↓

2:00 AM

↓

Run Pipeline
```

Common schedules:

- Every hour
- Daily
- Weekly
- Monthly

Typical use cases:

- Nightly ETL
- Daily reports
- Weekly backups
- Monthly billing

---

# Event-Based Trigger

Starts a pipeline when an event occurs.

Example:

```
CSV Uploaded

↓

Trigger Fires

↓

Pipeline Starts
```

Common events:

- File arrives
- Blob created
- Data received
- External system event

Benefits:

- Real-time automation
- No polling required
- Faster processing

---

# Trigger Flow

Example:

```
Schedule

↓

Pipeline

↓

Copy Activity

↓

Notebook

↓

Lakehouse

↓

Warehouse

↓

Refresh Semantic Model
```

Everything begins because the trigger starts the pipeline.

---

# Scheduling Options

A schedule trigger can specify:

- Start Date
- Start Time
- Time Zone
- Frequency
- Interval

Example:

```
Start:

1 July 2026

↓

Every Day

↓

2:00 AM

↓

Asia/Kolkata
```

---

# Frequency

Common frequencies:

- Once
- Hourly
- Daily
- Weekly
- Monthly

Choose the frequency based on business requirements.

---

# Time Zones

Always configure the correct time zone.

Example:

```
UTC

or

Asia/Kolkata

or

US Eastern Time
```

Incorrect time zones can cause pipelines to run at unexpected times.

---

# Event-Driven Architecture

Instead of checking every minute whether a file exists:

```
Check

↓

No File

↓

Check Again

↓

No File

↓

Check Again
```

Use an event trigger:

```
File Arrives

↓

Pipeline Starts
```

This is more efficient.

---

# Scheduling vs Event-Based Trigger

| Schedule Trigger | Event Trigger |
|------------------|---------------|
| Time-based | Event-based |
| Predictable | Reactive |
| Daily reports | File uploads |
| Nightly ETL | Streaming scenarios |

---

# Trigger Dependencies

Multiple pipelines can work together.

Example:

```
Pipeline A

↓

Completes

↓

Pipeline B Starts
```

Useful for large ETL workflows.

---

# Pipeline Chaining

Large organizations often split work into multiple pipelines.

Example:

```
Pipeline 1

↓

Ingest Data

↓

Pipeline 2

↓

Transform Data

↓

Pipeline 3

↓

Refresh Reports
```

This approach improves maintainability.

---

# Orchestration Pattern

A pipeline can coordinate multiple services.

Example:

```
Copy Data

↓

Notebook

↓

Dataflow Gen2

↓

Warehouse

↓

Semantic Model Refresh
```

The pipeline orchestrates every step.

---

# Scheduling Incremental Loads

Example:

```
Daily

↓

Read Yesterday's Records

↓

Append New Data
```

This avoids loading the full dataset every day.

---

# Monitoring Trigger Runs

Fabric allows monitoring of:

- Trigger status
- Pipeline status
- Start time
- End time
- Duration
- Success
- Failure

Monitoring ensures scheduled jobs execute correctly.

---

# Retry with Scheduled Pipelines

Suppose a pipeline starts at 2:00 AM.

The database is temporarily unavailable.

Pipeline:

Fails

↓

Retry

↓

Succeeds

No manual intervention is required.

---

# Disable Triggers

Triggers can be temporarily disabled.

Useful during:

- Maintenance
- Development
- Testing
- Deployment

The pipeline remains available but will not start automatically.

---

# Best Practices

Use Schedule Triggers for:

- Daily ETL
- Weekly Reports
- Monthly Data Loads
- Regular Warehouse Refresh

Use Event Triggers for:

- File uploads
- Streaming data
- Near real-time ingestion
- External events

---

# Real Fabric Example

Every night:

```
2:00 AM

↓

Schedule Trigger

↓

Copy SQL Data

↓

Notebook

↓

Silver Table

↓

Gold Table

↓

Warehouse

↓

Power BI Refresh

↓

Success Email
```

Everything executes automatically.

---

# Common DP-700 Scenarios

### Scenario 1

Need a pipeline to run every night.

Answer:

Schedule Trigger.

---

### Scenario 2

Need a pipeline to start when a CSV file arrives.

Answer:

Event-Based Trigger.

---

### Scenario 3

Need to test a pipeline.

Answer:

Manual Trigger.

---

### Scenario 4

Need to automate weekly reports.

Answer:

Schedule Trigger.

---

### Scenario 5

Need near real-time processing.

Answer:

Event-Based Trigger.

---

### Scenario 6

Need to stop automatic execution during maintenance.

Answer:

Disable Trigger.

---

### Scenario 7

Need Pipeline B to execute only after Pipeline A finishes.

Answer:

Pipeline Chaining (or dependency/orchestration).

---

# Common Exam Traps

### Trap 1

Question:

Which trigger starts based on time?

Answer:

Schedule Trigger.

---

### Trap 2

Question:

Which trigger reacts to file uploads?

Answer:

Event-Based Trigger.

---

### Trap 3

Question:

Which trigger is best for testing?

Answer:

Manual Trigger.

---

### Trap 4

Question:

Can triggers be disabled?

Answer:

Yes.

---

### Trap 5

Question:

Which trigger minimizes unnecessary polling?

Answer:

Event-Based Trigger.

---

# Memory Tricks

Trigger

= Start Button

---

Manual

= Click

---

Schedule

= Calendar

---

Event

= Something Happens

---

Pipeline

= Workflow

---

Schedule

= Time

---

Event

= Action

---