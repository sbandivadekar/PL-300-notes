## 🔹 RELATED()

### What it does

`RELATED()` **fetches a value from a related table** using an **existing relationship**.

```DAX
Product Category =
RELATED ( Products[Category] )
```

✔ Pulls data from **lookup (dimension) table**  
✔ Works only when a **relationship exists**  
✔ Commonly used in **calculated columns**

---
## 🔹 Why RELATED Works Only in Row Context

### Key Rule (EXAM FAVORITE)

> **RELATED requires Row Context**

Why?

- Row context means **“current row”**
- For each row, DAX:
    1. Takes the key value (e.g., ProductID)
    2. Follows the relationship
    3. Fetches the matching value from the related table
### Where Row Context Exists

✔ Calculated Columns  
✔ Iterators (`SUMX`, `FILTER`, `ADDCOLUMNS`)

### Where It Does NOT Exist

❌ Measures (by default)

---
## 🔹 Why RELATED Does NOT Work in Measures

Measures:

- Have **filter context**
- Do **not** have row context

❌ This fails:
```DAX
Category = RELATED ( Products[Category] )
```

---
## 🔹 Why Slicers Don’t Affect RELATED

### Important Concept

> `RELATED()` is evaluated **at data refresh time**, not at query time

Because
- Calculated columns are **static**
- Slicers change **filter context**
- Filter context affects **measures**, not calculated columns

### Example
```DAX
Country Name = RELATED ( Geography[Country] )
```

---
## 🔹 RELATEDTABLE()

## What is RELATEDTABLE()?

`RELATEDTABLE()` **returns a table of related rows** from another table **based on an existing relationship**.

👉 Think of it as:

> **“From this current row, give me all matching rows from the other table.”**

## Basic Syntax

```DAx
RELATEDTABLE ( TableName )
```
- Returns a **table**, not a single value
- Must be used **inside an aggregation or iterator**

---
## Simple Model Example

### Tables

- **Customers** (1)
    - CustomerID

- **Sales** (Many)
    - CustomerID
    - Amount

Relationship:  
`Customers[CustomerID] → Sales[CustomerID]`

---
## Example 1: Total Sales per Customer (Calculated Column)

```DAX
Customer Total Sales =
SUMX (
    RELATEDTABLE ( Sales ),
    Sales[Amount]
)
```

### What happens internally

1. Row context exists on **Customers**
2. RELATEDTABLE fetches **all Sales rows for that customer**
3. `SUMX` iterates and sums them

### Where it works

✔ Calculated Columns  
✔ Measures (because filter context exists)  
✔ Iterators

---
## RELATEDTABLE in Measures

```DAX
Customer Sales =
SUMX (
    RELATEDTABLE ( Sales ),
    Sales[Amount]
)
```
✔ Works because:

- Measure has **filter context**
- Visual filters the current customer
- RELATEDTABLE returns only related sales

---
# RELATEDTABLE vs RELATED

| Feature     | RELATED       | RELATEDTABLE          |
| ----------- | ------------- | --------------------- |
| Returns     | Single value  | Table                 |
| Used in     | Row context   | Filter or row context |
| Typical use | Lookup column | Aggregation           |
| Direction   | Many → One    | One → Many            |

---
### Memory Trick

- **RELATED → lookup**
- **RELATEDTABLE → collect rows**

---
## Why Slicers DO Affect RELATEDTABLE (Unlike RELATED)

### Key Difference

- RELATED → calculated column → static
- RELATEDTABLE → often used in measures → dynamic

