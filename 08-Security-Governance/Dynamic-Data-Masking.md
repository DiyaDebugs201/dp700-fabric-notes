# Dynamic Data Masking (DDM)

> **📖 DP-700 Skill Area:** Configure Security and Governance
>
> **⭐ Exam Priority:** HIGH

---

# 📌 What is Dynamic Data Masking?

Dynamic Data Masking (DDM) hides sensitive data from unauthorized users **without changing the actual data stored in the database**.

The original values remain unchanged.

Only the displayed value changes depending on the user's permissions.

Think of DDM as placing a **mask** over sensitive information.

---

# 🏢 Real-World Analogy

Imagine a hospital database.

```
Patient Name

Phone Number

Email

Medical ID
```

A receptionist needs to verify patients but does **not** need to see their complete phone number.

Instead of:

```
9876543210
```

They see:

```
98XXXX3210
```

The actual value is still stored securely.

Only the displayed value is masked.

---

# 🎯 Why Do We Need DDM?

Many users need access to records but not to every piece of sensitive information.

Examples:

- Customer support agents
- Receptionists
- Call center employees
- Junior analysts
- Temporary staff

DDM allows them to work while protecting confidential data.

---

# How Dynamic Data Masking Works

```
User Requests Data

↓

Authentication

↓

Permission Check

↓

Mask Applied (if required)

↓

Data Returned
```

Users with sufficient privileges see the real value.

Other users see the masked version.

---

# Common Data That Is Masked

Organizations often mask:

- Phone Numbers
- Email Addresses
- Aadhaar Numbers
- PAN Numbers
- Passport Numbers
- Credit Card Numbers
- Bank Account Numbers
- Customer IDs
- Employee IDs

---

# Example

Employee Table

| Name | Email | Salary |
|------|-------|---------|
| Alice | alice@company.com | 90000 |

### HR Manager

| Name | Email | Salary |
|------|-------|---------|
| Alice | alice@company.com | 90000 |

### HR Intern

| Name | Email | Salary |
|------|-------|---------|
| Alice | aXXXX@company.com | XXXXX |

The data is the same.

Only the displayed values differ.

---

# Common Masking Functions

Microsoft SQL-based systems commonly support several masking functions.

## 1. Default Mask

Replaces most of the value with generic masking characters.

Example:

```
9876543210

↓

XXXXXXXXXX
```

---

## 2. Partial Mask

Shows part of the original value.

Example:

```
9876543210

↓

98XXXX3210
```

Useful for phone numbers and IDs.

---

## 3. Email Mask

Masks email addresses.

Example:

```
alice@company.com

↓

aXXXX@company.com
```

---

## 4. Random Mask

Returns a random value within a specified range instead of the real value.

Useful for numeric fields in development or testing environments.

---

# Dynamic Data Masking vs Column-Level Security

This is one of the most common DP-700 comparisons.

| Dynamic Data Masking | Column-Level Security |
|----------------------|----------------------|
| User can access the column | User cannot access the column |
| Value is masked | Column is hidden |
| Data still exists | Column access is blocked |
| Best for partial visibility | Best for complete restriction |

---

# Dynamic Data Masking vs Row-Level Security

| Dynamic Data Masking | Row-Level Security |
|----------------------|-------------------|
| Masks values | Filters rows |
| Same rows remain visible | Rows disappear |
| Protects sensitive values | Protects subsets of data |

---

# Dynamic Data Masking vs Object-Level Security

| Dynamic Data Masking | Object-Level Security |
|----------------------|----------------------|
| Masks values inside a table | Hides the entire table or object |
| User opens the table | User may not even know the object exists |

---

# Real Business Scenario

A bank stores customer information.

```
Customer Table

Name

Phone

Account Number

Balance
```

### Customer Support Agent

Can see:

- Customer Name
- Partially masked phone number
- Masked account number

### Bank Manager

Can see:

- Complete phone number
- Complete account number
- Full balance

The same table serves different users with different levels of visibility.

---

# Best Practices

✔ Mask only sensitive fields.

✔ Combine DDM with RLS and CLS when appropriate.

✔ Grant unmasked access only to authorized users.

✔ Test masking with different user accounts.

✔ Document masking policies for compliance.

---

# DP-700 Exam Tips

⭐ **High Priority**

Remember:

- **DDM masks values.**
- **CLS hides columns.**
- **RLS hides rows.**
- **OLS hides objects.**

If the requirement says:

> "Users should see part of a phone number."

Answer:

✅ Dynamic Data Masking

---

# Common Mistakes

### ❌ Mistake 1

Thinking DDM encrypts data.

Reality:

DDM only changes how data is displayed.

The underlying data remains unchanged.

---

### ❌ Mistake 2

Using CLS when users still need to identify records.

Correct solution:

Use DDM.

---

### ❌ Mistake 3

Using DDM instead of RLS.

Remember:

DDM masks values.

RLS filters rows.

---

# Interview Questions

### Q1. What is Dynamic Data Masking?

It hides sensitive values from unauthorized users while keeping the original data unchanged.

---

### Q2. Does DDM modify stored data?

No.

Only the displayed value changes.

---

### Q3. When should DDM be used?

When users need access to records but should not see complete sensitive values.

---

### Q4. What is the difference between DDM and CLS?

DDM masks the value.

CLS hides the entire column.

---

### Q5. Can DDM be combined with other security mechanisms?

Yes.

It is commonly used together with RLS, CLS, and OLS.

---

# 🧠 Memory Trick

```
DDM

↓

Display

↓

Disguise
```

Think:

**Dynamic Data Masking = Disguised Display**

The data is still there—it just looks different to unauthorized users.

---

# 🚨 DP-700 Exam Alert

Microsoft often asks:

> "Users should verify customers but must not see complete credit card numbers."

✅ Dynamic Data Masking

---

> "Hide the Salary column completely."

✅ Column-Level Security

---

> "Show only the South Region."

✅ Row-Level Security

---

> "Hide the Payroll table."

✅ Object-Level Security

---

# ⚡ Quick Revision

- Dynamic Data Masking hides sensitive values without changing stored data.
- Authorized users see real values; others see masked values.
- Common masking types include Default, Partial, Email, and Random.
- DDM protects values, not rows or columns.
- DDM is different from CLS, RLS, and OLS.
- Use DDM when users need partial visibility.
- DDM does not encrypt or permanently modify data.
- Combine DDM with other security mechanisms for layered protection.
- Test masking using different user roles.
- Remember: **DDM = Mask Values, CLS = Hide Columns, RLS = Filter Rows, OLS = Hide Objects.**