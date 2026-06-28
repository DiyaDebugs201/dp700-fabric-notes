# Row-Level Security (RLS), Column-Level Security (CLS) & Object-Level Security (OLS)

> **📖 DP-700 Skill Area:** Configure Security and Governance
>
> **⭐ Exam Priority:** ⭐⭐⭐⭐⭐ (Very High)

---

# 📌 Why Do We Need Data-Level Security?

Not every user should see the same data.

Consider a multinational company:

```
Company

├── India Sales
├── USA Sales
├── UK Sales
└── HR Payroll
```

Questions:

- Should an India manager see USA sales?
- Should interns see employee salaries?
- Should the Finance table even be visible to Marketing?

The answer is **No**.

Microsoft Fabric provides three levels of data protection:

- **RLS (Row-Level Security)** → Hide rows
- **CLS (Column-Level Security)** → Hide columns
- **OLS (Object-Level Security)** → Hide entire objects

---

# Security Hierarchy

```
Workspace
      │
      ▼
Item
      │
      ▼
Object
      │
      ▼
Column
      │
      ▼
Row
```

Each level adds more granular control.

---

# 1️⃣ Row-Level Security (RLS)

## 📌 What is RLS?

RLS filters **rows of data** based on the identity or role of the user.

The user opens the report or table normally, but only sees rows they are authorized to view.

---

## Example

Sales Table

| Employee | Region | Sales |
|----------|--------|-------|
| Alice | India | 25000 |
| Bob | USA | 32000 |
| Chris | UK | 28000 |

India Manager logs in.

Visible:

| Employee | Region | Sales |
|----------|--------|-------|
| Alice | India | 25000 |

USA and UK rows are automatically filtered out.

---

## How RLS Works

```
User Logs In

↓

Identity Verified

↓

RLS Rule Applied

↓

Filtered Data Returned
```

The original data is **not changed**.

Only the visible rows change.

---

## Static RLS

Static rules are fixed.

Example:

```
Region = 'India'
```

Anyone assigned to this role always sees India data.

---

## Dynamic RLS

Dynamic rules use the logged-in user's identity.

Example:

```
USERPRINCIPALNAME()
```

The report automatically filters data based on the current user.

Example:

```
diya@company.com

↓

Region = India
```

No separate role is required for every employee.

---

## Common RLS Scenarios

- Regional sales managers
- Branch-wise banking data
- Hospital departments
- Country-specific dashboards
- Territory-based reporting

---

# 2️⃣ Column-Level Security (CLS)

## 📌 What is CLS?

CLS hides **specific columns** while allowing access to the rest of the table.

The user can open the table but cannot view protected columns.

---

## Example

Employee Table

| Name | Department | Salary | PAN Number |
|------|------------|---------|------------|

An HR intern should see:

| Name | Department |
|------|------------|

Hidden:

- Salary
- PAN Number

The rows remain visible.

Only selected columns are hidden.

---

## Common CLS Use Cases

- Salary
- Aadhaar Number
- PAN Number
- Credit Card Number
- Medical Information
- Customer Email

---

# 3️⃣ Object-Level Security (OLS)

## 📌 What is OLS?

OLS hides **entire database objects**.

Objects include:

- Tables
- Views
- Measures
- Hierarchies

Users don't just lose access—they often don't even know the object exists.

---

## Example

Warehouse

```
Sales

Customers

Products

Payroll
```

Marketing Team:

Visible:

```
Sales

Customers

Products
```

Hidden:

```
Payroll
```

Payroll is invisible.

---

## Common OLS Scenarios

- Payroll tables
- Audit tables
- Financial models
- Executive-only measures
- Confidential datasets

---

# Comparison

| Feature | RLS | CLS | OLS |
|----------|-----|-----|-----|
| Protects | Rows | Columns | Objects |
| User opens table? | ✅ Yes | ✅ Yes | ❌ Sometimes No |
| Filters data | ✅ | ❌ | ❌ |
| Hides columns | ❌ | ✅ | ❌ |
| Hides tables | ❌ | ❌ | ✅ |
| Typical Example | Region | Salary | Payroll Table |

---

# Real Business Example

Retail Company

```
Sales Table

Region

Employee

Revenue

Profit

Salary
```

### Sales Manager

Can see:

Only South Region

(RLS)

---

### HR Intern

Cannot see:

Salary Column

(CLS)

---

### Marketing Team

Cannot access:

Payroll Table

(OLS)

---

Three different security mechanisms solve three different problems.

---

# Dynamic Security

Dynamic security automatically adapts to the logged-in user.

Example:

```
USERPRINCIPALNAME()
```

Instead of creating:

India Role

USA Role

UK Role

One dynamic rule determines what each user should see.

Benefits:

- Easier administration
- Better scalability
- Less maintenance

---

# Best Practices

✔ Apply the Principle of Least Privilege.

✔ Use Dynamic RLS when possible.

✔ Hide sensitive columns with CLS.

✔ Hide confidential tables with OLS.

✔ Test security using different user accounts.

✔ Keep security rules documented.

---

# DP-700 Exam Tips

⭐ **Very High Priority**

Remember the keywords:

**Rows** → RLS

**Columns** → CLS

**Objects** → OLS

Microsoft often changes only one word in the scenario.

Example:

> "Hide Salary"

CLS

---

> "Hide Payroll Table"

OLS

---

> "Show only South Region"

RLS

---

# Common Mistakes

### ❌ Mistake 1

Thinking RLS removes rows.

Reality:

Rows remain in the database.

Only visibility changes.

---

### ❌ Mistake 2

Using CLS to hide a table.

Correct solution:

OLS.

---

### ❌ Mistake 3

Using Workspace Roles for data filtering.

Workspace Roles manage access to resources.

RLS filters data.

---

### ❌ Mistake 4

Creating hundreds of static RLS roles.

Better:

Dynamic RLS using user identity.

---

# Interview Questions

### Q1. What is Row-Level Security?

It restricts which rows of data a user can see based on security rules.

---

### Q2. What is Column-Level Security?

It hides specific columns while allowing access to the remaining data.

---

### Q3. What is Object-Level Security?

It restricts access to entire database objects such as tables, views, or measures.

---

### Q4. What is Dynamic RLS?

Dynamic RLS automatically filters data using the logged-in user's identity instead of predefined static roles.

---

### Q5. Which security mechanism should be used to hide salary information?

CLS.

---

### Q6. Which mechanism hides an entire Payroll table?

OLS.

---

### Q7. Which mechanism lets regional managers see only their own region?

RLS.

---

# 🧠 Memory Trick

```
R

↓

Rows

-------------------

C

↓

Columns

-------------------

O

↓

Objects
```

Or remember:

**RCO**

- **R** → Rows
- **C** → Columns
- **O** → Objects

---

# 🚨 DP-700 Exam Alert

Microsoft commonly asks:

> "Managers should only see their own sales region."

✅ RLS

---

> "Hide the Salary column."

✅ CLS

---

> "Prevent access to the Payroll table."

✅ OLS

---

> "Automatically filter based on the logged-in user."

✅ Dynamic RLS

---

# ⚡ Quick Revision

- RLS filters rows without changing the underlying data.
- Static RLS uses fixed rules; Dynamic RLS uses the logged-in user's identity.
- CLS hides selected columns while leaving rows visible.
- OLS hides entire objects such as tables, views, measures, or hierarchies.
- RLS, CLS, and OLS solve different security problems and are often used together.
- Use Dynamic RLS for scalable enterprise solutions.
- Follow the Principle of Least Privilege.
- Test security with different user accounts before deployment.
- Don't confuse Workspace Roles with RLS.
- Remember: **Rows → RLS, Columns → CLS, Objects → OLS.**