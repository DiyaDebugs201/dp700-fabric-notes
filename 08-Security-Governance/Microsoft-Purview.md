# Microsoft Purview

> **📖 DP-700 Skill Area:** Configure Security and Governance
>
> **⭐ Exam Priority:** HIGH

---

# 📌 What is Microsoft Purview?

Microsoft Purview is Microsoft's unified **data governance, compliance, security, and risk management** solution.

It helps organizations:

- Discover data
- Classify data
- Protect sensitive information
- Track data movement
- Monitor compliance
- Govern data across Microsoft Fabric and other data sources

Think of Purview as the **governor** of your organization's data.

---

# 🏢 Real-World Analogy

Imagine a large company with thousands of documents.

Without management:

- Nobody knows where files are.
- Sensitive files are shared accidentally.
- Data ownership is unclear.
- Compliance becomes difficult.

Now imagine a librarian who:

- Knows where every file is
- Labels sensitive documents
- Tracks who accesses them
- Records every change
- Enforces company rules

That librarian is Microsoft Purview.

---

# 🎯 Why Do We Need Purview?

Modern organizations store data in:

- Microsoft Fabric
- Azure Storage
- SQL Databases
- Power BI
- Microsoft 365
- Amazon S3
- Google Cloud Storage
- On-premises systems

Without governance:

- Duplicate data appears.
- Sensitive information is exposed.
- Compliance becomes difficult.
- Nobody knows which dataset is trusted.

Purview solves these governance challenges.

---

# Core Capabilities

Microsoft Purview provides several major capabilities.

```
Microsoft Purview

├── Data Catalog
├── Data Lineage
├── Sensitivity Labels
├── Information Protection
├── Compliance
├── Data Discovery
├── Audit
└── Data Loss Prevention (DLP)
```

---

# Data Catalog

## What is it?

A centralized inventory of organizational data assets.

Instead of searching multiple systems, users can search the catalog.

Example:

```
Search:

Customer Sales

↓

Lakehouse

Warehouse

Power BI Report
```

Benefits:

- Easier discovery
- Reduced duplication
- Better collaboration

---

# Data Lineage

## What is Lineage?

Lineage shows how data moves through the organization.

Example:

```
SQL Database

↓

Pipeline

↓

Lakehouse

↓

Notebook

↓

Warehouse

↓

Semantic Model

↓

Power BI Report
```

Lineage helps answer:

- Where did this data come from?
- Which reports depend on this dataset?
- What breaks if this pipeline fails?

---

# Information Protection

Purview manages:

- Sensitivity Labels
- Encryption policies
- Access restrictions
- Classification policies

This ensures sensitive information is handled appropriately.

---

# Data Discovery

Purview continuously discovers data across connected systems.

It identifies:

- Databases
- Files
- Tables
- Reports
- Warehouses
- Lakehouses

This provides visibility into the organization's data landscape.

---

# Data Classification

Purview can classify data automatically.

Examples:

- Email addresses
- Credit card numbers
- Passport numbers
- Aadhaar numbers
- PAN numbers
- Phone numbers

These classifications can trigger governance policies.

---

# Data Loss Prevention (DLP)

DLP policies help prevent sensitive information from being shared inappropriately.

Example:

```
Highly Confidential Payroll Report

↓

Attempt to Share Externally

↓

Blocked
```

DLP reduces accidental or unauthorized data exposure.

---

# Compliance

Many industries must follow regulations such as:

- GDPR
- HIPAA
- ISO standards
- Financial regulations

Purview helps organizations demonstrate compliance by:

- Tracking data
- Applying labels
- Maintaining audit trails
- Enforcing policies

---

# Audit Integration

Purview works with Microsoft auditing capabilities.

Organizations can track:

- Who accessed data
- Who modified data
- When changes occurred
- What actions were performed

This supports investigations and compliance reporting.

---

# Integration with Microsoft Fabric

Purview integrates closely with Fabric.

Examples:

- Sensitivity Labels applied to Fabric items
- Data Lineage across Pipelines and Lakehouses
- Governance policies
- Metadata discovery
- Compliance monitoring

Fabric and Purview work together to provide secure and governed analytics.

---

# Real Business Scenario

A multinational bank stores data in Microsoft Fabric.

Purview helps by:

- Cataloging all datasets
- Labeling customer data as Confidential
- Tracking data movement from SQL to Power BI
- Blocking external sharing of payroll reports
- Recording audit events
- Supporting GDPR compliance

Without Purview, managing thousands of datasets would be difficult.

---

# Microsoft Purview vs Microsoft Fabric

| Microsoft Fabric | Microsoft Purview |
|------------------|------------------|
| Analytics platform | Governance platform |
| Stores and processes data | Governs and protects data |
| Pipelines, Lakehouses, Warehouses | Catalog, Lineage, Compliance, Labels |
| Focuses on analytics | Focuses on governance |

They complement each other.

---

# Purview and Sensitivity Labels

Purview creates and manages Sensitivity Labels.

Example:

```
Customer Data

↓

Purview

↓

Apply Confidential Label

↓

Fabric Report Displays Label
```

Purview defines the policy.

Fabric applies and respects it.

---

# Purview and Data Lineage

One of the most valuable Purview features.

Example:

```
Azure SQL

↓

Pipeline

↓

Lakehouse

↓

Notebook

↓

Warehouse

↓

Power BI Report
```

If the SQL source changes, engineers immediately know which downstream assets are affected.

---

# Best Practices

✔ Classify sensitive data.

✔ Apply Sensitivity Labels consistently.

✔ Review Data Lineage regularly.

✔ Monitor compliance reports.

✔ Use DLP for highly confidential information.

✔ Document data ownership.

✔ Periodically review governance policies.

---

# DP-700 Exam Tips

⭐ **High Priority**

Remember what Purview provides:

- Data Catalog
- Data Lineage
- Data Classification
- Sensitivity Labels
- Information Protection
- Compliance
- Audit
- Data Loss Prevention

If a question mentions:

- Governance
- Compliance
- Data Catalog
- Lineage
- Classification

Think:

✅ Microsoft Purview

---

# Common Mistakes

### ❌ Mistake 1

Thinking Purview stores data.

Reality:

Fabric stores data.

Purview governs it.

---

### ❌ Mistake 2

Thinking Purview replaces Workspace Roles.

Reality:

Workspace Roles manage permissions.

Purview manages governance and compliance.

---

### ❌ Mistake 3

Ignoring Data Lineage.

Lineage is essential for understanding data flow and impact analysis.

---

# Interview Questions

### Q1. What is Microsoft Purview?

A unified data governance, compliance, and information protection platform.

---

### Q2. What is Data Lineage?

A visual representation of how data moves between systems and transformations.

---

### Q3. What is the purpose of a Data Catalog?

To help users discover and understand available data assets.

---

### Q4. Does Microsoft Purview replace Microsoft Fabric?

No.

Fabric is the analytics platform.

Purview is the governance platform.

---

### Q5. What is Data Loss Prevention (DLP)?

Policies that help prevent sensitive data from being shared or exposed improperly.

---

# 🧠 Memory Trick

```
Purview

↓

P

Protect

U

Understand

R

Regulate

V

Visualize

I

Inventory

E

Enforce

W

Watch
```

Think of Purview as the organization watching over all data.

---

# 🚨 DP-700 Exam Alert

Microsoft commonly asks:

> "An organization wants to classify data and apply confidentiality labels."

✅ Microsoft Purview

---

> "Users want to trace how data moves from SQL to Power BI."

✅ Data Lineage (Microsoft Purview)

---

> "Analysts need a searchable inventory of datasets."

✅ Data Catalog (Microsoft Purview)

---

> "Prevent confidential reports from being shared externally."

✅ Data Loss Prevention (DLP)

---

# ⚡ Quick Revision

- Microsoft Purview is Microsoft's unified data governance platform.
- It provides Data Catalog, Data Lineage, Data Classification, Sensitivity Labels, Information Protection, DLP, Audit, and Compliance.
- Fabric processes and stores data; Purview governs and protects it.
- Data Lineage helps trace data movement across systems.
- Data Catalog provides a searchable inventory of data assets.
- DLP prevents unauthorized sharing of sensitive information.
- Purview integrates with Microsoft Fabric to enforce governance.
- Sensitivity Labels are created and managed through Purview.
- Purview supports regulatory compliance and risk management.
- Remember: **Fabric builds analytics, Purview governs analytics.**
