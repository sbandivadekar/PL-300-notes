## ✅ What is a Connection Mode?

A **connection mode** defines **how Power BI accesses data** and **where data is stored**.

> It directly impacts **performance, refresh, modeling features, and licensing/gateway needs**.

---
# 1️⃣ **Import Mode** ⭐ (Most Common)

## 📌 What it is

Data is **copied into Power BI’s in-memory model** (VertiPaq).

## 🧠 How it works
```
Data Source → Power BI Desktop → In-memory model
```

## ✅ Pros

- Fastest performance
- Full DAX support
- Works offline after refresh
- Best for complex calculations

## ❌ Cons

- Data can be stale (needs refresh)
- Dataset size limits apply

## 🔁 Refresh

- Manual or scheduled
- Gateway required for **on-prem** sources

## 🎯 Use when

- Data fits in memory
- Performance is critical
- Data doesn’t need real-time updates

---
# 2️⃣ **DirectQuery Mode**

## 📌 What it is

No data is imported. **Queries are sent live** to the source.

## 🧠 How it works
```
User visual → Power BI → Data Source (every time)
```

## ✅ Pros

- Near real-time data
- No dataset size limits
- Source remains the “single source of truth”

## ❌ Cons

- Slower visuals (network + source dependent)
- Limited DAX & modeling features
- Source must handle query load
- Quick measure doesn't work for time intelligence calculation.

## 🔁 Refresh

- ❌ No scheduled refresh
- Data is always live

## 🔌 Gateway

- Required for **on-prem** sources

## 🎯 Use when

- Data is very large
- Near real-time reporting needed
- Source performance is strong

---
# 3️⃣ **Live Connection**

## 📌 What it is

Connects **live to an existing semantic model** (or Analysis Services).

## 🧠 How it works
```
Power BI Report → Existing Semantic Model
```

## ✅ Pros

- Centralized model
- Strong governance
- No duplicate datasets

## ❌ Cons

- Cannot modify the model
- Limited modeling in report

## 🔁 Refresh

- Handled by the **source semantic model**

## 🎯 Use when

- Enterprise/shared datasets
- Certified or governed models
- Thin report scenarios

---
# 4️⃣ **Composite Model** ⭐⭐ (Advanced)

## 📌 What it is

**Mix of Import + DirectQuery** in one model.

## 🧠 Example

- Sales fact → DirectQuery
- Date & Product → Import

## ✅ Pros

- Balance performance + real-time
- Flexible architecture

## ❌ Cons

- More complex design
- Requires careful performance tuning

## 🎯 Use when

- Large fact tables
- Smaller dimensions
- Need both speed and freshness

---
# 🔁 Connection Modes

|Feature|Import|DirectQuery|Live|Composite|
|---|---|---|---|---|
|Data stored in Power BI|✅|❌|❌|✅/❌|
|Performance|🚀 Fast|🐢 Slower|⚡ Depends|⚖ Balanced|
|Real-time|❌|✅|✅|⚠ Partial|
|DAX support|Full|Limited|Limited|Mixed|
|Gateway (on-prem)|✅|✅|✅|✅|

