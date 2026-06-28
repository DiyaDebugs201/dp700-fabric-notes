# Sensitivity Labels

> **📖 DP-700 Skill Area:** Configure Security and Governance
>
> **⭐ Exam Priority:** HIGH

---

# 📌 What are Sensitivity Labels?

Sensitivity Labels classify data based on its level of confidentiality and help organizations protect sensitive information.

Instead of treating every dataset equally, Microsoft Fabric allows you to label data according to its sensitivity.

Common examples:

- Public
- General
- Confidential
- Highly Confidential

These labels help users understand how data should be handled and enable additional protection mechanisms such as encryption and access restrictions.

---

# 🏢 Real-World Analogy

Imagine a company's physical documents.

Some documents have stamps like:

```
PUBLIC
```

Others are marked:

```
CONFIDENTIAL
```

Or even:

```
TOP SECRET
```

Employees immediately know how carefully each document must be handled.

Sensitivity Labels work the same way for digital data.

---

# 🎯 Why Do We Need Sensitivity Labels?

Organizations store many types of information.

Examples:

- Employee records
- Financial reports
- Customer information
- Product designs
- Source code
- Medical records

Not all data needs the same level of protection.

Sensitivity Labels help:

- Classify data
- Protect confidential information
- Support regulatory compliance
- Reduce accidental data exposure
- Improve governance

---

# How Sensitivity Labels Work

```
Create Data

↓

Classify Data

↓

Apply Label

↓

Protection Rules Applied

↓

Users Access Data
```

The label travels with the item and informs users (and Microsoft services) how that data should be handled.

---

# Common Label Hierarchy

Although organizations can customize labels, a common hierarchy is:

| Label | Description |
|--------|-------------|
| Public | Safe to share with anyone |
| General | Internal business information |
| Confidential | Sensitive business information |
| Highly Confidential | Critical or regulated information |

---

# Public

Examples:

- Marketing brochures
- Public documentation
- Company website content

Restrictions:

Minimal or none.

---

# General

Examples:

- Internal meeting notes
- Team documentation
- Standard reports

Shared only within the organization.

---

# Confidential

Examples:

- Customer databases
- Financial statements
- Sales forecasts
- Internal business strategies

Requires controlled access.

---

# Highly Confidential

Examples:

- Payroll
- Medical records
- Legal documents
- Government-regulated information
- Intellectual property

Receives the strongest protection.

---

# Where Can Labels Be Applied?

Sensitivity Labels can be applied to many Fabric and Microsoft data assets, including:

- Power BI Reports
- Semantic Models
- Lakehouses
- Warehouses
- Dashboards
- Microsoft Fabric items
- Microsoft 365 documents (through Microsoft Purview)

---

# Automatic vs Manual Labeling

## Manual

A user chooses the appropriate label.

Example:

```
Sales Report

↓

Confidential
```

---

## Automatic

Policies automatically apply labels when sensitive data is detected.

Example:

```
Contains Credit Card Numbers

↓

Automatically Label

↓

Highly Confidential
```

This helps reduce human error.

---

# What Happens After a Label Is Applied?

Depending on organizational policies, a sensitivity label can trigger actions such as:

- Displaying visual markings (headers, footers, watermarks)
- Restricting who can open the content
- Encrypting the content
- Preventing unauthorized sharing
- Supporting compliance and auditing

> The exact protections depend on how your organization configures Microsoft Purview Information Protection.

---

# Integration with Microsoft Purview

Sensitivity Labels are managed through **Microsoft Purview Information Protection**.

Purview allows organizations to:

- Create labels
- Publish labels
- Define protection rules
- Monitor classified data
- Enforce compliance policies

Microsoft Fabric integrates with these labels.

---

# Real Business Example

A healthcare organization stores:

```
Hospital Workspace

├── Patient Records
├── Staff Directory
├── Public Health Report
└── Payroll
```

Labels:

| Item | Label |
|------|-------|
| Public Health Report | Public |
| Staff Directory | General |
| Patient Records | Highly Confidential |
| Payroll | Confidential |

Employees immediately understand the sensitivity of each dataset.

---

# Sensitivity Labels vs Workspace Roles

| Sensitivity Labels | Workspace Roles |
|--------------------|-----------------|
| Classify and protect data | Control workspace permissions |
| Focus on data confidentiality | Focus on user permissions |
| Travel with the data | Apply only within the workspace |

---

# Sensitivity Labels vs RLS

| Sensitivity Labels | RLS |
|--------------------|-----|
| Describe and protect data | Filter visible rows |
| Classification | Data filtering |

A report can be:

- Labeled **Confidential**
- Protected by **RLS**

These are complementary features.

---

# Best Practices

✔ Create a clear labeling policy.

✔ Use automatic labeling where possible.

✔ Apply labels consistently.

✔ Review labels regularly.

✔ Train users on label meanings.

✔ Combine labels with RLS, CLS, OLS, and DDM for layered security.

---

# DP-700 Exam Tips

⭐ **High Priority**

Remember:

Sensitivity Labels answer:

> **"How sensitive is this data?"**

They do **not** decide which rows, columns, or tables users can access.

Microsoft often combines Sensitivity Labels with Microsoft Purview in exam scenarios.

---

# Common Mistakes

### ❌ Mistake 1

Thinking Sensitivity Labels replace security.

Reality:

Labels classify and can trigger protection policies, but they do not replace Workspace Roles, RLS, CLS, or OLS.

---

### ❌ Mistake 2

Using only manual labeling.

Better approach:

Use automatic labeling where practical to reduce mistakes.

---

### ❌ Mistake 3

Applying the same label to every dataset.

Choose labels based on business sensitivity and compliance requirements.

---

# Interview Questions

### Q1. What are Sensitivity Labels?

They classify and help protect data based on its level of sensitivity.

---

### Q2. Who manages Sensitivity Labels?

Microsoft Purview Information Protection.

---

### Q3. Can Sensitivity Labels automatically be applied?

Yes.

Organizations can configure automatic labeling policies.

---

### Q4. Do Sensitivity Labels replace Row-Level Security?

No.

Labels classify data, while RLS filters the data users can see.

---

### Q5. What are common sensitivity levels?

- Public
- General
- Confidential
- Highly Confidential

---

# 🧠 Memory Trick

```
Public

↓

General

↓

Confidential

↓

Highly Confidential
```

Think:

As you move downward, the need for protection increases.

---

# 🚨 DP-700 Exam Alert

Microsoft frequently asks:

> "A dataset contains personally identifiable information (PII). How should it be classified?"

Answer:

✅ Apply an appropriate **Sensitivity Label** (for example, Confidential or Highly Confidential, depending on the organization's policy).

---

> "Managers should only see employees in their department."

Answer:

✅ Row-Level Security

---

> "Hide the Salary column."

Answer:

✅ Column-Level Security

---

> "Classify payroll data according to its confidentiality."

Answer:

✅ Sensitivity Labels

---

# ⚡ Quick Revision

- Sensitivity Labels classify data based on confidentiality.
- Common labels are Public, General, Confidential, and Highly Confidential.
- Labels can trigger protections such as encryption and sharing restrictions.
- Labels are managed through Microsoft Purview Information Protection.
- Labels complement—not replace—Workspace Roles, RLS, CLS, OLS, and DDM.
- Labels can be applied manually or automatically.
- Use consistent labeling across the organization.
- Combine classification with access controls for stronger governance.
- Labels help meet compliance and regulatory requirements.
- Remember: **Sensitivity Labels classify data; security features control access to it.**