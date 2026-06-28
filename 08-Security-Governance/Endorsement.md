# Endorsement

> **📖 DP-700 Skill Area:** Configure Security and Governance
>
> **⭐ Exam Priority:** Medium

---

# 📌 What is Endorsement?

Endorsement is a feature in Microsoft Fabric that helps users identify **trusted and reliable data assets**.

In large organizations, hundreds or even thousands of reports, semantic models, and datasets may exist.

Endorsement helps users quickly determine which items they should trust.

Think of it as a **quality badge** for Fabric items.

---

# 🏢 Real-World Analogy

Imagine an online shopping website.

Some products have:

⭐ "Verified Purchase"

Others have:

🏆 "Amazon's Choice"

These badges help customers identify trusted products.

Similarly, Endorsement helps users identify trusted Fabric items.

---

# 🎯 Why Do We Need Endorsement?

Without endorsements:

- Multiple versions of the same report may exist.
- Users may choose outdated datasets.
- Duplicate reports become common.
- Confidence in analytics decreases.

Endorsement improves:

- Trust
- Discoverability
- Collaboration
- Data governance
- Self-service analytics

---

# Types of Endorsement

Microsoft Fabric supports two endorsement levels.

```
Endorsement

├── Promoted
└── Certified
```

---

# 1️⃣ Promoted

A **Promoted** item is recommended for use.

It indicates:

- Useful
- Well maintained
- Frequently used
- Recommended by its owner or team

Promoted does **not** mean the item has undergone formal organizational validation.

### Example

A Sales team creates a report used by all regional managers.

The team marks it as **Promoted**.

Other users know it is recommended.

---

# 2️⃣ Certified

A **Certified** item has been officially reviewed and approved by an organization's governance or data administration team.

Certified items represent the organization's **trusted source of truth**.

### Example

The Finance department publishes an official quarterly revenue dataset.

After validation, the governance team marks it as **Certified**.

Employees should use this dataset instead of creating their own copies.

---

# Promoted vs Certified

| Promoted | Certified |
|----------|-----------|
| Recommended by owner or team | Officially approved by governance/admin team |
| Team-level trust | Organization-wide trust |
| Informal recommendation | Formal validation |
| Good for collaboration | Best for enterprise reporting |

---

# Where Can Endorsement Be Applied?

Endorsement can be applied to several Fabric items, such as:

- Semantic Models
- Reports
- Dashboards
- Lakehouses (where supported)
- Other supported Fabric assets

The goal is to guide users toward trusted content.

---

# Benefits of Endorsement

✔ Helps users find trusted assets.

✔ Encourages reuse instead of duplication.

✔ Improves consistency across reports.

✔ Supports self-service analytics.

✔ Reduces confusion when multiple datasets exist.

✔ Strengthens data governance.

---

# Endorsement in a Real Business Scenario

A company has three sales datasets.

```
Sales_Q1_Final

Sales_Q1_New

Sales_Q1_Official
```

Without endorsement, users might choose the wrong dataset.

The governance team marks:

```
Sales_Q1_Official

↓

Certified
```

Now employees immediately know which dataset to use.

---

# Relationship with Data Governance

Endorsement is one part of a broader governance strategy.

Other governance features include:

- Microsoft Purview
- Sensitivity Labels
- Audit Logs
- Workspace Security
- RLS
- CLS
- OLS
- Dynamic Data Masking

Together, these features improve trust, security, and compliance.

---

# Endorsement vs Sensitivity Labels

| Endorsement | Sensitivity Labels |
|--------------|-------------------|
| Indicates trust and quality | Indicates confidentiality |
| Helps users choose reliable assets | Helps protect sensitive data |
| Governance and discoverability | Security and compliance |

Example:

A dataset can be:

- **Certified** (trusted)
- **Confidential** (sensitive)

These features complement each other.

---

# Endorsement vs Workspace Roles

| Endorsement | Workspace Roles |
|-------------|-----------------|
| Indicates trust | Controls permissions |
| Does not grant access | Determines who can access and manage items |

A user still needs permission to access an endorsed item.

---

# Best Practices

✔ Certify official enterprise datasets.

✔ Promote useful team-level assets.

✔ Review endorsements regularly.

✔ Avoid certifying outdated or duplicate datasets.

✔ Educate users to prefer Certified assets whenever possible.

✔ Combine endorsement with governance policies.

---

# DP-700 Exam Tips

⭐ **Medium Priority**

Remember:

- **Promoted = Recommended**
- **Certified = Officially Approved**

If Microsoft asks:

> "Which dataset should employees trust?"

Look for the **Certified** dataset.

---

# Common Mistakes

### ❌ Mistake 1

Thinking endorsement grants access.

Reality:

Endorsement does **not** change permissions.

Workspace Roles and security settings still control access.

---

### ❌ Mistake 2

Thinking Promoted and Certified are the same.

Reality:

Certified has formal organizational approval.

Promoted is simply recommended.

---

### ❌ Mistake 3

Certifying every dataset.

Only authoritative, validated datasets should be Certified.

---

# Interview Questions

### Q1. What is Endorsement in Microsoft Fabric?

A feature that helps users identify trusted and recommended data assets.

---

### Q2. What is the difference between Promoted and Certified?

Promoted is recommended by a team or owner.

Certified is officially approved by the organization's governance or administration team.

---

### Q3. Does Endorsement control access?

No.

Permissions are managed through Workspace Roles and other security mechanisms.

---

### Q4. Why is Certification important?

It identifies the organization's official and trusted source of truth.

---

### Q5. Can a dataset be both Certified and Confidential?

Yes.

Certification indicates trust, while a Sensitivity Label indicates confidentiality.

---

# 🧠 Memory Trick

```
Promoted

↓

Recommended

----------------

Certified

↓

Company Approved
```

Or simply remember:

**P = Preferred**

**C = Company Approved**

---

# 🚨 DP-700 Exam Alert

Microsoft commonly asks:

> "Users need to identify the organization's official dataset."

Answer:

✅ Certified

---

> "A team wants to recommend a useful report."

Answer:

✅ Promoted

---

> "Restrict access to confidential data."

Answer:

❌ Not Endorsement

Use Workspace Roles, RLS, CLS, OLS, DDM, or Sensitivity Labels depending on the scenario.

---

# ⚡ Quick Revision

- Endorsement helps users identify trusted Fabric items.
- Two endorsement levels exist: Promoted and Certified.
- Promoted means recommended by a team or owner.
- Certified means officially approved by the organization's governance team.
- Endorsement improves discoverability and reduces duplicate datasets.
- It does not control permissions or security.
- Certified datasets are typically considered the organization's "single source of truth."
- Endorsement complements governance features such as Purview and Sensitivity Labels.
- Encourage users to consume Certified assets whenever available.
- Remember: **Promoted = Recommended, Certified = Officially Trusted.**