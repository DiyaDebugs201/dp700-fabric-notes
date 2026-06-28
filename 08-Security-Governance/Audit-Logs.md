# Microsoft Fabric Audit Logs

> **📖 DP-700 Skill Area:** Configure Security and Governance
>
> **⭐ Exam Priority:** HIGH

---

# 📌 What are Audit Logs?

Audit Logs are records of activities performed by users and services in Microsoft Fabric.

They answer questions such as:

- Who performed an action?
- What action was performed?
- When did it happen?
- Which item was affected?
- Was the action successful?

Think of Audit Logs as the **security camera** of your Microsoft Fabric environment.

---

# 🏢 Real-World Analogy

Imagine an office building.

Every employee entering or leaving the building is recorded.

```
Employee

↓

Entry Card

↓

Time Recorded

↓

Door Recorded
```

If something goes wrong, security reviews the entry logs.

Audit Logs work the same way for Microsoft Fabric.

---

# 🎯 Why Do We Need Audit Logs?

Organizations need to:

- Investigate incidents
- Detect unauthorized access
- Troubleshoot issues
- Meet compliance requirements
- Track user activity
- Support security audits

Without Audit Logs, it is difficult to determine what happened in an environment.

---

# What Information is Recorded?

Typical audit records include:

- User who performed the action
- Timestamp
- Operation performed
- Fabric item affected
- Workspace name
- Result (Success or Failure)

Example:

| User | Action | Item | Time | Status |
|------|--------|------|------|--------|
| Alice | Deleted | Pipeline | 10:45 AM | Success |
| Bob | Created | Lakehouse | 2:15 PM | Success |
| Chris | Failed Login | Workspace | 4:30 PM | Failed |

---

# Common Audited Activities

Microsoft Fabric can log many actions, including:

- Creating a workspace
- Deleting a workspace
- Creating a Lakehouse
- Running a Pipeline
- Editing a Notebook
- Refreshing a Semantic Model
- Sharing a Report
- Updating permissions
- Publishing reports
- Accessing Fabric items

---

# How Audit Logs Work

```
User Performs Action

↓

Fabric Records Event

↓

Audit Log Entry Created

↓

Administrators Review Logs
```

Audit logging happens automatically for supported events.

---

# Where Are Audit Logs Used?

Audit Logs support:

- Security investigations
- Compliance reporting
- Internal audits
- Operational troubleshooting
- Governance reviews

They help answer:

> "What happened?"

---

# Integration with Microsoft Purview

Audit Logs work together with Microsoft Purview.

Purview helps:

- Analyze audit activity
- Support compliance investigations
- Generate governance reports
- Track organizational events

Fabric generates activity.

Purview helps govern and review it.

---

# Common Investigation Scenarios

## Scenario 1

A Pipeline disappeared.

Question:

Who deleted it?

Solution:

Review Audit Logs.

---

## Scenario 2

A confidential report was shared externally.

Question:

Who shared it?

Solution:

Review Audit Logs.

---

## Scenario 3

A Semantic Model refresh failed repeatedly.

Question:

When did failures start?

Solution:

Review Audit Logs together with monitoring information.

---

## Scenario 4

Unexpected permissions were added to a workspace.

Question:

Who modified the permissions?

Solution:

Audit Logs.

---

# Audit Logs vs Monitoring

A common exam comparison.

| Audit Logs | Monitoring |
|------------|------------|
| Focus on user and system activities | Focus on operational health and performance |
| Answers "Who did what?" | Answers "How is the system performing?" |
| Security and compliance | Reliability and operations |

Example:

Pipeline failed.

Monitoring:

- Shows execution failure.

Audit Logs:

- Show who modified the pipeline before it failed.

---

# Audit Logs vs Data Lineage

| Audit Logs | Data Lineage |
|------------|--------------|
| Tracks user actions | Tracks data movement |
| Security investigation | Data flow understanding |

Audit Logs answer:

> Who changed it?

Lineage answers:

> Where did the data come from?

---

# Best Practices

✔ Review Audit Logs regularly.

✔ Retain logs according to organizational policies.

✔ Monitor privileged accounts closely.

✔ Investigate unexpected permission changes.

✔ Combine Audit Logs with monitoring dashboards.

✔ Protect audit information from unauthorized access.

---

# DP-700 Exam Tips

⭐ **High Priority**

Remember these keywords:

- Who?
- What?
- When?
- Success?
- Failure?

These almost always indicate **Audit Logs**.

If the question asks:

> "Identify who deleted a Lakehouse."

Answer:

✅ Audit Logs.

---

# Common Mistakes

### ❌ Mistake 1

Using Audit Logs to monitor performance.

Reality:

Audit Logs record activities.

Performance monitoring measures system health.

---

### ❌ Mistake 2

Thinking Audit Logs replace monitoring.

Reality:

They complement each other.

Monitoring tracks operations.

Audit Logs track activities.

---

### ❌ Mistake 3

Ignoring failed operations.

Failed log entries are often valuable during investigations.

---

# Interview Questions

### Q1. What are Microsoft Fabric Audit Logs?

Records of user and system activities performed within Microsoft Fabric.

---

### Q2. What information is stored in an Audit Log?

Typical information includes:

- User
- Action
- Timestamp
- Target item
- Result

---

### Q3. Why are Audit Logs important?

They support security investigations, compliance, governance, and troubleshooting.

---

### Q4. How are Audit Logs different from Monitoring?

Monitoring measures operational health.

Audit Logs record activities and user actions.

---

### Q5. Can Audit Logs help determine who deleted a Fabric item?

Yes.

They record the user who performed the action.

---

# 🧠 Memory Trick

```
Audit

↓

A

Action

↓

U

User

↓

T

Time

↓

I

Item

↓

T

Tracking
```

Think:

Audit Logs always answer:

**Who did what, when, and to which item?**

---

# 🚨 DP-700 Exam Alert

Microsoft commonly asks:

> "An administrator needs to determine who modified workspace permissions."

✅ Audit Logs

---

> "Investigate who deleted a Pipeline."

✅ Audit Logs

---

> "Understand why a report shows incorrect numbers."

✅ Data Lineage (if tracing data flow) or Monitoring (if refresh/performance), depending on the scenario—not Audit Logs alone.

---

> "Track suspicious user activity."

✅ Audit Logs

---

# ⚡ Quick Revision

- Audit Logs record user and system activities in Microsoft Fabric.
- They capture who performed an action, what happened, when it happened, and the outcome.
- Audit Logs are essential for investigations, compliance, and governance.
- They differ from Monitoring, which focuses on system performance and health.
- They complement Microsoft Purview for governance and compliance.
- Common events include creating, deleting, modifying, sharing, and refreshing Fabric items.
- Review logs regularly and monitor privileged users.
- Failed events are just as important as successful ones.
- Use Audit Logs to answer "Who did what?"
- Remember: **Audit Logs = Activity History; Monitoring = System Health.**