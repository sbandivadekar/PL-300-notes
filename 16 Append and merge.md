## What is **Append**?

**Append = combine tables by adding rows (one below another).**  
It does **NOT** add columns.

---
## 🔹 Real Example (Step-by-Step)

### 🎯 Scenario

You receive **monthly sales files** with the **same structure**.

### 🔹 January Sales

|OrderID|Date|Amount|Region|
|---|---|---|---|
|101|2024-01-05|1000|India|
|102|2024-01-10|1500|India|

### 🔹 February Sales

|OrderID|Date|Amount|Region|
|---|---|---|---|
|201|2024-02-03|1200|USA|
|202|2024-02-15|1800|USA|

---

### 🔹 After **Append**

|OrderID|Date|Amount|Region|
|---|---|---|---|
|101|2024-01-05|1000|India|
|102|2024-01-10|1500|India|
|201|2024-02-03|1200|USA|
|202|2024-02-15|1800|USA|

✔ Rows increased  
✔ Columns stayed same

---
## IMP

- Nulls are kept
- Columns Names should be same in both 
- If the some columns names are not matching then new columns is created.
- contain duplicates.

---
## What is **Merge**?

**Merge = combine tables by adding columns using a common key**  
It is the **Power Query version of SQL JOIN**.

## 🔹 Real Example (Step-by-Step)

### 🎯 Scenario

You want to **enrich sales data** with customer details.

---

### 🔹 Sales Table (Fact)

|OrderID|CustomerID|Amount|
|---|---|---|
|101|C01|1000|
|102|C02|1500|

### 🔹 Customer Table (Dimension)

|CustomerID|CustomerName|City|
|---|---|---|
|C01|Amit|Pune|
|C02|Sara|NYC|

---

### 🔹 Merge Result (Left Outer Join)

|OrderID|CustomerID|Amount|CustomerName|City|
|---|---|---|---|---|
|101|C01|1000|Amit|Pune|
|102|C02|1500|Sara|NYC|

✔ Rows remain from **Sales**  
✔ Columns added from **Customer**

## IMP

- NULL never matches
- Duplicate Multiply
- Unique values = Safe
- Fact + Dim (merge) = OK
- Fact + Fact (merge) = Danger 

---

## 🔹 APPEND vs MERGE (Big Picture)
| Concept        | APPEND                 | MERGE                                |
| -------------- | ---------------------- | ------------------------------------ |
| SQL Equivalent | `UNION ALL`            | `JOIN`                               |
| Direction      | Vertical (rows)        | Horizontal (columns)                 |
| Row count      | Increases              | Usually same or may increase (joins) |
| Columns        | Same structure         | Different tables combined            |
| Use case       | Combine same-type data | Enrich data using keys               |

---
# Query Folding
## What is **Query Folding**?

**Query folding** means:

> **Power Query converts your transformation steps into a single native query (like SQL) and pushes it back to the data source to execute there.**

> In simple all the transformation steps are send to source, so that all the transformation should be done in source and not in power BI.

📌 Instead of:

- Loading all data into Power BI
- Then transforming locally

👉 Power BI says:

> “Hey database, YOU do the work.”


---
## Why Query Folding Matters

✔ Faster refresh  
✔ Less data transfer  
✔ Uses source engine power (SQL, Snowflake, SQL Server)  
✔ Lower memory usage in Power BI

> More query folding = better performance

---

## connection mode
### **Import Mode**

- Data is **copied into Power BI**
- Query folding is used **during data refresh**
- Purpose:  
    👉 Push filters, column selection, joins to the **source**
- Result:  
    ✔ Faster refresh  
    ✔ Less data transferred

### **DirectQuery Mode**

- Data **stays in the source**
- Every visual sends a **query back to the source**
- Query folding is **critical** here

👉 Without folding:

- Power BI can’t translate logic
- Queries become inefficient or fail
    

📌 **PL-300 line**

> DirectQuery **relies heavily on query folding** for performance.

---
## Live connection **does not support query folding**


