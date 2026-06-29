# Troubleshooting in Microsoft Fabric

> **📖 DP-700 Skill Area:** Monitor and Optimize an Analytics Solution
>
> **⭐ Exam Priority:** ⭐⭐⭐⭐⭐ (Very High)

---

# 📌 What is Troubleshooting?

Troubleshooting is the systematic process of identifying, diagnosing, and resolving issues that occur in Microsoft Fabric workloads.

Problems may occur in:

- Pipelines
- Notebooks
- Dataflows Gen2
- Lakehouses
- Warehouses
- Eventstreams
- Eventhouses
- Semantic Models
- OneLake Shortcuts

The goal is not just to fix the issue, but also to identify its root cause and prevent it from happening again.

---

# 🏢 Real-World Analogy

Imagine your car doesn't start.

You don't immediately replace the engine.

Instead, you check:

```
Battery

↓

Fuel

↓

Starter

↓

Engine
```

Similarly, in Fabric, troubleshoot one layer at a time instead of guessing.

---

# General Troubleshooting Workflow

```
Issue Reported

↓

Identify the Affected Service

↓

Check Monitoring Hub

↓

Review Logs

↓

Read Error Message

↓

Identify Root Cause

↓

Fix Issue

↓

Test Again

↓

Monitor
```

Never skip directly to implementing a fix without understanding the cause.

---

# Pipeline Failures

Common causes:

- Incorrect parameters
- Authentication failures
- Missing files
- Timeout
- Activity dependency failures

Example:

```
Copy Activity

↓

Fails

↓

Pipeline Stops
```

Investigate:

- Pipeline run history
- Activity output
- Error details

---

# Notebook Failures

Typical causes:

- Syntax errors
- Missing tables
- Missing files
- Spark session issues
- Permission errors
- Out-of-memory exceptions

Useful tools:

- Spark Logs
- Spark UI
- Notebook output

---

# Dataflow Gen2 Errors

Possible causes:

- Invalid transformation
- Broken source connection
- Unsupported data type
- Schema changes
- Authentication issues

Investigate:

- Refresh history
- Error messages
- Source configuration

---

# Eventstream Issues

Possible causes:

- Source not sending events
- Incorrect destination
- Connection failures
- Transformation errors

Check:

- Event throughput
- Destination configuration
- Connection health

---

# Eventhouse Errors

Possible causes:

- Incorrect KQL query
- Missing permissions
- Schema mismatch
- Resource limitations

Review:

- Query results
- Error messages
- Table schema

---

# OneLake Shortcut Errors

Shortcuts may fail because:

- Source location changed
- Deleted source
- Permission denied
- Network issues

Always verify:

- Shortcut target
- Authentication
- Connectivity

---

# Semantic Model Refresh Failures

Common causes:

- Invalid credentials
- Gateway issues
- Schema changes
- Timeout
- Memory limits

Review:

- Refresh history
- Error details
- Source availability

---

# SQL Errors

Common SQL problems include:

### Syntax Errors

Example:

```sql
SELECT FROM Sales;
```

Missing column list.

---

### Missing Object

Example:

```sql
SELECT *
FROM Orders;
```

If the table doesn't exist:

```
Object Not Found
```

---

### Permission Errors

```
Access Denied
```

Check user permissions.

---

### Data Type Mismatch

Example:

Comparing text to numeric values.

Always verify data types.

---

# Spark Errors

Typical issues:

- Executor failures
- Out-of-memory
- Data skew
- Shuffle failures
- Missing libraries

Investigate using:

- Spark UI
- Spark Logs
- Executor information

---

# Authentication Issues

Common causes:

- Expired credentials
- Incorrect password
- Missing permissions
- Revoked access

Authentication answers:

**Who are you?**

---

# Authorization Issues

Authorization determines:

**What are you allowed to do?**

Example:

A Viewer attempts to delete a workspace.

Result:

Permission denied.

---

# Monitoring Hub

Monitoring Hub is the first place to investigate many issues.

It provides:

- Pipeline status
- Notebook runs
- Refresh history
- Activity duration
- Failure details

---

# Error Messages

Never ignore error messages.

Instead:

1. Read the complete message.
2. Identify the failing component.
3. Understand the root cause.
4. Apply the appropriate fix.

Avoid fixing symptoms instead of causes.

---

# Root Cause Analysis

Example:

```
Report Failed

↓

Refresh Failed

↓

Pipeline Failed

↓

SQL Login Failed

↓

Expired Credentials
```

The real issue is not the report.

It is the expired credentials.

Always trace errors back to the original cause.

---

# Troubleshooting Decision Tree

```
Problem

↓

Pipeline?

↓

Notebook?

↓

Warehouse?

↓

Lakehouse?

↓

Eventstream?

↓

Refresh?

↓

Check Logs

↓

Read Error

↓

Find Root Cause

↓

Fix

↓

Retest
```

---

# Best Practices

✔ Read the full error message.

✔ Use Monitoring Hub first.

✔ Review Spark Logs for notebook failures.

✔ Verify permissions before changing code.

✔ Confirm source availability.

✔ Test after applying fixes.

✔ Document recurring issues.

✔ Fix root causes, not symptoms.

---

# DP-700 Exam Tips

⭐ **Very High Priority**

Microsoft frequently asks:

> "A notebook fails with an OutOfMemory exception."

Think:

- Partitioning
- Memory optimization
- Spark optimization

---

> "A pipeline succeeds, but reports still show old data."

Think:

Semantic Model Refresh.

---

> "A OneLake shortcut suddenly fails."

Think:

- Source moved
- Permissions changed
- Authentication issue

---

> "A Dataflow refresh suddenly fails after a database update."

Think:

Schema change.

---

# Common Mistakes

### ❌ Mistake 1

Restarting everything without reading the error.

Always investigate first.

---

### ❌ Mistake 2

Ignoring logs.

Logs usually contain the exact failure reason.

---

### ❌ Mistake 3

Fixing symptoms instead of the root cause.

---

### ❌ Mistake 4

Assuming every failure is caused by code.

Many issues are configuration or permission related.

---

# Interview Questions

### Q1. What is the first step in troubleshooting?

Identify the affected component and review logs.

---

### Q2. Where should notebook failures be investigated?

Spark Logs, Spark UI, and Notebook output.

---

### Q3. What is the difference between authentication and authorization?

Authentication verifies identity.

Authorization determines permissions.

---

### Q4. What is Root Cause Analysis?

The process of identifying the underlying reason for a failure rather than only addressing its symptoms.

---

### Q5. Why is Monitoring Hub important?

It provides centralized monitoring for pipelines, notebooks, refreshes, and other Fabric workloads.

---

# 🧠 Memory Trick

Remember:

**I-L-R-F-T**

```
I → Identify

L → Logs

R → Root Cause

F → Fix

T → Test
```

Whenever troubleshooting, follow:

**Identify → Logs → Root Cause → Fix → Test**

---
