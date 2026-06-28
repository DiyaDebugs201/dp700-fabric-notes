# OneLake Security

> **📖 DP-700 Skill Area:** Configure Security and Governance
>
> **⭐ Exam Priority:** HIGH

---

# 📌 What is OneLake Security?

**OneLake Security** controls who can access data stored inside Microsoft Fabric's unified storage layer.

Unlike Workspace Roles, which control access to Fabric resources, OneLake Security protects the **actual files and folders** stored in OneLake.

Think of it as securing the storage itself.

---

# 🏢 Real-World Analogy

Imagine OneLake is a large digital warehouse.

```
OneLake

├── Sales/
│   ├── sales.csv
│   └── customers.csv
│
├── Finance/
│   ├── payroll.csv
│   └── budget.csv
│
└── HR/
    └── employees.csv
```

The Finance team should only access the **Finance** folder.

The HR team should only access the **HR** folder.

Even though everything is stored in one physical location, access is restricted.

That is the purpose of OneLake Security.

---

# 🎯 Why Do We Need OneLake Security?

Without OneLake Security:

- Sensitive files could be exposed.
- Confidential departments could access each other's data.
- Compliance requirements may be violated.

Benefits include:

- Folder-level protection
- File-level protection
- Secure collaboration
- Centralized storage security
- Better governance

---

# OneLake Security Model

```
Microsoft Entra ID

↓

Workspace Permissions

↓

OneLake Permissions

↓

Files & Folders
```

Identity is verified first.

Permissions are then evaluated before access is granted.

---

# What Can Be Protected?

OneLake Security applies to data stored inside OneLake, including:

- Files
- Folders
- Delta Tables
- Lakehouse data
- Shortcut locations

It focuses on the storage layer rather than reports or pipelines.

---

# Folder-Level Security

Permissions can be applied to an entire folder.

Example:

```
Sales/

├── Orders.csv
├── Products.csv
└── Customers.csv
```

Granting access to the **Sales** folder allows users to access its contents according to the assigned permissions.

---

# File-Level Security

Sometimes only one file should be protected.

Example:

```
Finance/

├── Budget.csv
├── Payroll.csv
└── Audit.csv
```

Only Finance Managers receive access to:

```
Payroll.csv
```

Other Finance employees cannot access that file.

---

# Permission Inheritance

Permissions often flow from parent to child.

Example:

```
Sales/

├── 2025/
│
└── 2026/
```

If a user has Read permission on **Sales**, they typically inherit access to subfolders unless inheritance is changed.

Inheritance simplifies permission management.

---

# Microsoft Entra ID Integration

OneLake Security integrates with **Microsoft Entra ID** (formerly Azure Active Directory).

Authentication:

```
User

↓

Microsoft Entra ID

↓

Verify Identity

↓

OneLake Permissions

↓

Grant or Deny Access
```

Identity management is centralized across Microsoft Fabric.

---

# Security Groups

Instead of assigning permissions individually:

❌ Alice

❌ Bob

❌ Charlie

Use a security group.

Example:

```
Finance Team

↓

Read Permission
```

Every member of the group automatically receives the correct access.

This is Microsoft's recommended approach.

---

# OneLake Shortcuts and Security

A **OneLake Shortcut** points to data stored elsewhere without copying it.

Example:

```
Lakehouse

↓

Shortcut

↓

Amazon S3
```

Important:

A shortcut **does not bypass security**.

Users must still have permission to access the underlying data source.

---

# Workspace Security vs OneLake Security

| Workspace Security | OneLake Security |
|--------------------|------------------|
| Controls Fabric resources | Controls storage access |
| Applies to the workspace | Applies to files and folders |
| Workspace Roles | Storage permissions |
| Manages who can work in the workspace | Manages who can access stored data |

---

# OneLake Security vs Row-Level Security

Another common exam comparison.

| OneLake Security | Row-Level Security |
|------------------|-------------------|
| Controls storage access | Controls visible data rows |
| User may not open the file | User opens the file but sees filtered data |
| File and folder protection | Data filtering |

Example:

A Sales Manager opens Sales.csv.

RLS hides the North Region.

OneLake Security determined whether they could open the file in the first place.

---

# Real-World Scenario

A company stores all departments in OneLake.

```
OneLake

├── Finance
├── Sales
├── HR
└── Marketing
```

Permissions:

| Team | Accessible Folder |
|------|-------------------|
| Finance | Finance |
| HR | HR |
| Marketing | Marketing |
| Sales | Sales |

No department can browse another department's folder.

---

# Best Practices

✔ Follow the Principle of Least Privilege.

✔ Use Microsoft Entra ID groups instead of assigning permissions to individual users.

✔ Protect sensitive folders separately.

✔ Review permissions regularly.

✔ Avoid unnecessary duplicate permissions.

✔ Document security policies.

---

# DP-700 Exam Tips

⭐ **High Priority**

Remember:

- Workspace Roles → Entire workspace.
- Item-Level Security → Individual Fabric items.
- OneLake Security → Files and folders.
- RLS → Rows inside the data.

When a question asks:

> "Who can access a folder stored in OneLake?"

Answer:

✅ OneLake Security.

---

# Common Mistakes

### ❌ Mistake 1

Assuming Workspace Roles automatically protect storage.

**Reality:**

Workspace Roles manage collaboration.

OneLake Security protects stored files and folders.

---

### ❌ Mistake 2

Thinking OneLake Shortcuts ignore permissions.

**Reality:**

Shortcuts respect the security of the source data.

---

### ❌ Mistake 3

Assigning permissions to every employee individually.

**Best Practice:**

Use Microsoft Entra ID security groups.

---

# Interview Questions

### Q1. What is OneLake Security?

It controls access to files and folders stored in Microsoft Fabric's OneLake.

---

### Q2. How is OneLake Security different from Workspace Roles?

Workspace Roles control permissions within a workspace.

OneLake Security controls access to the underlying stored data.

---

### Q3. Does a OneLake Shortcut bypass security?

No.

Users must still have permission to access the underlying data source.

---

### Q4. Why should organizations use Microsoft Entra ID groups?

They simplify permission management and improve scalability.

---

### Q5. What is permission inheritance?

Permissions assigned to a parent folder are typically inherited by child folders unless inheritance is changed.

---

# 🧠 Memory Trick

```
Workspace

↓

Items

↓

OneLake

↓

Files

↓

Rows
```

Think:

- Workspace → Workspace Roles
- Items → Item-Level Security
- Files → OneLake Security
- Rows → RLS

This is the complete security hierarchy in Fabric.

---

# 🚨 DP-700 Exam Alert

Microsoft often asks:

> "Users should access only files inside the Finance folder."

Answer:

✅ OneLake Security

---

> "Users should access only the Sales report."

Answer:

✅ Item-Level Security

---

> "Users should only see rows for their own region."

Answer:

✅ Row-Level Security

---

> "Users should collaborate across an entire workspace."

Answer:

✅ Workspace Roles

---

# ⚡ Quick Revision

- OneLake Security protects files and folders stored in OneLake.
- It complements Workspace Roles and Item-Level Security.
- Folder-level and file-level permissions can be applied.
- Permissions are commonly inherited from parent folders.
- Microsoft Entra ID provides authentication.
- Security groups simplify permission management.
- OneLake Shortcuts do not bypass source security.
- Follow the Principle of Least Privilege.
- Use OneLake Security for storage protection and RLS for data filtering.
- Microsoft frequently tests the differences between Workspace Roles, Item-Level Security, OneLake Security, and RLS.