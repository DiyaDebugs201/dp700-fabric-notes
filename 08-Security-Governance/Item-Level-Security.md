# Item-Level Security

> **📖 DP-700 Skill Area:** Configure Security and Governance
>
> **⭐ Exam Priority:** HIGH

---

# 📌 What is Item-Level Security?

Item-Level Security allows you to control access to **individual Fabric items** instead of the entire workspace.

Examples of Fabric items include:

- Lakehouse
- Warehouse
- Notebook
- Pipeline
- Semantic Model
- Dataflow Gen2
- Power BI Report
- Dashboard

Instead of giving someone access to everything in a workspace, you can grant access to only the specific item they need.

---

# 🏢 Real-World Analogy

Imagine a company has one workspace called **Sales Analytics**.

Inside it:

```
Sales Workspace

├── Sales Lakehouse
├── Sales Pipeline
├── Executive Dashboard
├── Revenue Report
└── Finance Notebook
```

Suppose a sales manager only needs the **Executive Dashboard**.

There is no reason to give access to the Pipeline, Notebook, or Lakehouse.

Instead, grant access only to the **Dashboard**.

This is Item-Level Security.

---

# 🎯 Why Do We Need Item-Level Security?

Without Item-Level Security:

- Users may see items they shouldn't.
- Sensitive notebooks may be exposed.
- Pipelines could be modified accidentally.
- Reports may reveal confidential business information.

Benefits include:

- Fine-grained access control
- Better security
- Reduced risk
- Easier collaboration across teams

---

# Workspace Roles vs Item-Level Security

This is one of the most important DP-700 comparisons.

| Workspace Role | Item-Level Security |
|----------------|---------------------|
| Applies to the entire workspace | Applies to one specific item |
| Broad permissions | Granular permissions |
| Best for team management | Best for exceptions |
| Configured once per workspace | Configured per item |

Example:

A Data Engineer is a **Contributor** in the Engineering workspace.

The Finance team shares only one Warehouse with them.

That Warehouse permission is Item-Level Security.

---

# What Can Be Secured?

Many Fabric items support individual permissions.

Examples include:

- Lakehouse
- Warehouse
- Notebook
- Semantic Model
- Reports
- Dashboards
- Dataflow Gen2
- Pipeline

Each item can have its own sharing settings.

---

# Common Permission Types

Depending on the item, permissions may include:

- View
- Read
- Build
- Share
- Modify
- Manage

Not every item supports every permission, but the principle is the same: grant only the permissions required.

---

# Sharing an Item

Typical process:

```
Select Item

↓

Manage Permissions

↓

Choose User or Group

↓

Assign Permission

↓

Save
```

Only that item is shared.

---

# Example 1 – Report Sharing

Workspace:

```
Finance Workspace

├── Revenue Report
├── Payroll Report
├── Finance Notebook
```

The CEO only needs:

```
Revenue Report
```

Grant access only to the Revenue Report.

The CEO cannot access the Notebook or Payroll Report unless those items are also shared.

---

# Example 2 – Notebook Access

A Data Scientist needs a Notebook for experimentation.

They do **not** need access to:

- Warehouse
- Reports
- Pipelines

Grant access only to the Notebook.

---

# Example 3 – Warehouse Access

A BI Developer needs to query a Warehouse.

Grant permission to:

```
Sales Warehouse
```

No access is required to:

- Engineering Lakehouse
- Data Science Notebook
- Marketing Pipeline

---

# Item-Level Permissions vs Row-Level Security (RLS)

Many beginners confuse these.

| Item-Level Security | Row-Level Security |
|---------------------|-------------------|
| Controls access to an item | Controls which rows of data are visible |
| User may or may not open the item | User can open the item but sees limited data |
| Security at the item level | Security inside the data |

Example:

A manager can open the Sales Report but only sees data for the South Region.

This is **RLS**, not Item-Level Security.

---

# Item-Level Permissions vs Workspace Roles

Example:

Sarah is a **Viewer** in the workspace.

She is also given **Build** permission on one Semantic Model.

Result:

- Viewer rights remain for the workspace.
- Additional permission applies only to that Semantic Model.

This allows exceptions without changing workspace-wide permissions.

---

# Best Practices

✔ Grant the minimum permissions required.

✔ Prefer security groups instead of assigning permissions to individual users.

✔ Review permissions regularly.

✔ Remove unused access.

✔ Document who has access to sensitive items.

---

# Principle of Least Privilege

Always ask:

> "What is the minimum access this user needs?"

Example:

❌ Give a business analyst Contributor access to the whole workspace.

✅ Give them View access to a single report.

---

# Real-World Scenario

A retail company has one Fabric workspace.

```
Retail Workspace

├── Sales Lakehouse
├── Inventory Warehouse
├── Executive Dashboard
├── Sales Pipeline
└── Marketing Notebook
```

Permissions:

| User | Access |
|------|--------|
| Data Engineer | Workspace Contributor |
| BI Developer | Workspace Member |
| CEO | Executive Dashboard only |
| Marketing Team | Marketing Notebook only |

Item-Level Security allows these targeted permissions without exposing unnecessary resources.

---

# DP-700 Exam Tips

⭐ **High Priority**

Remember:

- Workspace Roles = Workspace-wide permissions.
- Item-Level Security = Permissions on a specific Fabric item.
- RLS = Limits rows within data.
- OneLake Security = Controls file and folder access in OneLake.

When a question asks:

> "A user should access only one report."

The answer is:

✅ **Item-Level Security**

---

# Common Mistakes

### ❌ Mistake 1

Giving Workspace Admin rights just so someone can view one report.

**Correct Approach:**

Use Item-Level Security.

---

### ❌ Mistake 2

Confusing Item-Level Security with RLS.

Remember:

- Item-Level Security controls **access to the object**.
- RLS controls **access to the data inside the object**.

---

### ❌ Mistake 3

Assigning permissions directly to every employee.

Best practice:

Use Microsoft Entra ID groups where possible.

---

# Interview Questions

### Q1. What is Item-Level Security?

It controls access to individual Fabric items such as Lakehouses, Warehouses, Reports, or Pipelines.

---

### Q2. When should Item-Level Security be used instead of Workspace Roles?

When a user needs access to only one or a few specific items instead of the entire workspace.

---

### Q3. How is Item-Level Security different from Row-Level Security?

Item-Level Security determines whether a user can access an item.

Row-Level Security determines which rows of data they can see after accessing it.

---

### Q4. Why should organizations follow the Principle of Least Privilege?

To reduce security risks by granting only the permissions users need.

---

### Q5. Can Item-Level Security override Workspace Roles?

No. It complements Workspace Roles by providing more granular access where needed.

---

# 🧠 Memory Trick

```
Workspace Role

↓

Whole Building

--------------------

Item-Level Security

↓

One Room

--------------------

Row-Level Security

↓

One Drawer Inside the Room
```

Think:

- Workspace Role → Entire workspace
- Item-Level Security → Specific item
- RLS → Specific rows of data

---

# 🚨 DP-700 Exam Alert

Microsoft loves scenario questions like:

> "A manager should only access one report."

Answer:

✅ Item-Level Security

---

> "A user should only see customers from their own region."

Answer:

✅ Row-Level Security (RLS)

---

> "A developer should create notebooks and pipelines across the workspace."

Answer:

✅ Workspace Role (Contributor or Member)

---

# ⚡ Quick Revision

- Item-Level Security secures individual Fabric items.
- It provides granular access without exposing the whole workspace.
- Common secured items include Lakehouses, Warehouses, Reports, Pipelines, and Notebooks.
- Use Item-Level Security when users need access to only specific resources.
- It complements Workspace Roles rather than replacing them.
- Do not confuse Item-Level Security with RLS.
- Follow the Principle of Least Privilege.
- Prefer Microsoft Entra ID groups over individual assignments.
- Review permissions regularly.
- Microsoft frequently tests Workspace Roles vs Item-Level Security vs RLS in scenario-based questions.