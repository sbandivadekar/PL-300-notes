## ✅ What is RLS?

**Row-Level Security (RLS)** restricts **which rows of data a user can see** in a Power BI report.

> Different users see **different data** using the **same report**.

---
## 🧠 Where RLS Is Defined

- Created in **Power BI Desktop**
- Enforced in **Power BI Service**
- Applied at **dataset (semantic model) level**

---
# 1️⃣ Static RLS

## 📌 What is Static RLS?

**Static RLS** uses **hard-coded filters** inside roles.

> Each role is fixed to a specific filter value.

## Example
```DAX
[Region] = "India"
```

### 🧠 Meaning
Any user assigned to this role sees only India data

Same data for all users in that role

---
## 🎯 Use Static RLS when:

- Small number of users
- Fixed access rules
- Simple scenarios (exam examples)

---
## ✅ Characteristics (Static RLS)

- Simple to implement
- Easy to understand
- Requires **multiple roles** for multiple values
- Manual user assignment

> This is not scalable

---
# 2️⃣ Dynamic RLS

## 📌 What is Dynamic RLS?

**Dynamic RLS** filters data **based on the logged-in user**.

> Filter changes dynamically per user at runtime.

---
## 🧠 How It Works

Uses:

- `USERPRINCIPALNAME()`
- `USERNAME()`

to match the logged-in user to a **security table**.

---
## 📦 Required Table (Security Table)

Example: `UserRegion`

|UserEmail|Region|
|---|---|
|a@company.com|India|
|b@company.com|USA|
RLS Require Mapping table that used to filter the data as per the logged in user

```DAX
UserRegion[UserEmail] = USERPRINCIPALNAME()
```

## 🧠 Meaning

- Power BI detects who logged in
- Filters rows dynamically
- Same role works for all users

---
## ✅ Characteristics (Dynamic RLS)

- Highly scalable
- One role for many users
- Minimal maintenance
- Enterprise-ready

---
# 🔐 USERPRINCIPALNAME() vs USERNAME()

## ✅ Why These Functions Exist

Both functions return **information about the currently logged-in user** and are mainly used for **Dynamic Row-Level Security (RLS)**.

# 1️⃣ USERPRINCIPALNAME()

## 📌 What it Returns

Returns the **user’s login in email (UPN) format**.

```
firstname.lastname@company.com
```

---
## Syntax

```
USERPRINCIPALNAME()
```

---
## 🧠 Example Output

```
john.doe@contoso.com
```

## 🎯 Best Use Case

✔ Dynamic RLS  
✔ Enterprise environments  
✔ When security table stores **email IDs**

---
# 2️⃣ USERNAME()

## 📌 What it Returns

Returns **different values depending on environment**.

---
### 🧠 Output in Power BI Desktop

```
DOMAIN\username
```

### 🧠 Output in Power BI Service

```
username@company.com
```

---
## Syntax

```
USERNAME()
```

---
## ⚠ Key Problem

❌ Output is **not consistent** between Desktop and Service

---
## 🎯 Use Case

✔ Legacy systems  
✔ On-prem Active Directory scenarios  
❌ Not recommended for modern RLS

---
# 🔁 USERPRINCIPALNAME vs USERNAME

|Feature|USERPRINCIPALNAME()|USERNAME()|
|---|---|---|
|Output|Email / UPN|Domain\user OR Email|
|Desktop vs Service|Same|Different|
|Reliability|⭐⭐⭐⭐|⭐⭐|
|Best for RLS|✅ Yes|⚠ Risky|
|Exam answer|✅ Preferred|❌ Avoid|
