**Aggregation functions** summarize data across rows and always return a **single value (scalar)**.  
They are mostly used in **MEASURES** and are **filter-context aware**.

---
## ✅ SUM

Adds all **numeric values in a single column**.

```DAX
Total Sales = SUM ( Sales[Amount] )
```

**Key Points**

- Evaluated in **filter context**
- Column must be **numeric**
- **Fastest** aggregation

✔ Most commonly used  
❌ Cannot evaluate expressions  
❌ Cannot reference multiple columns

## ✅ SUMX (Iterator)

Evaluates an **expression row by row** and then sums the results.

```DAX
Total Revenue =
SUMX (
    Sales,
    Sales[Quantity] * Sales[Price]
)
```

**Key Points**

- Creates **row context**
- Expression evaluated **per row**
- Slower than `SUM` on large tables

✔ Use when calculation is required  
❌ Avoid if simple column aggregation is possible

🧠 **PL-300 Rule**

> **Simple column → `SUM`**  
> **Expression → `SUMX`**

---
# 🔹 2. AVERAGE Family

## ✅ AVERAGE

Returns the **mean of a numeric column**.

`Average Sales = AVERAGE ( Sales[Amount] )`

**Key Points**

- Ignores blanks
- Uses **filter context**
- Column only (no expressions)

---
## ✅ AVERAGEX

Evaluates an **expression per row** and averages the results.

```DAX
Average Revenue =
AVERAGEX (
    Sales,
    Sales[Quantity] * Sales[Price]
)
```
✔ Use when average requires calculation  
❌ Slower than `AVERAGE`

---
# 🔹 3. COUNT Family (EXAM FAVORITE)

## ✅ COUNT

Counts **non-blank numeric values** in a column.

```DAX
Order Count = COUNT ( Sales[OrderID] )
```

**Key Points**

- Counts **numbers only**
- Ignores blanks
- Uses **filter context**

---
## ✅ COUNTROWS (VERY IMPORTANT)

Counts the **number of rows in a table**.

```DAX
Total Orders = COUNTROWS ( Sales )
```

**Key Points**

- Works on **tables**, not columns
- Counts **all rows** (including blank columns)
- Respects **filter context**
- Commonly used with `FILTER()`

```DAX
High Value Orders =
COUNTROWS (
    FILTER ( Sales, Sales[Amount] > 1000 )
)
```

---
## ✅ DISTINCTCOUNT (VERY IMPORTANT)

Counts **unique, non-blank values**.

```DAX
Unique Customers = DISTINCTCOUNT ( Sales[CustomerID] )
```

**Key Points**

- Very common in PL-300
- Used for Customers, Products, Orders
- Respects filter context

---
# 🔹 4. MIN / MAX Family

## ✅ MIN

Returns the **smallest value** in a column.

```DAX
Min Sale = MIN ( Sales[Amount] )
```

---

## ✅ MAX

Returns the **largest value** in a column.

```DAX
Max Sale = MAX ( Sales[Amount] )
```

---
## ✅ MINX / MAXX

Evaluate an **expression row by row** and return min/max result.

```DAX
Max Revenue =
MAXX (
    Sales,
    Sales[Quantity] * Sales[Price]
)
```

---
## 🧠 Aggregation vs Iterator

|Function|Type|Row Context|Filter Context|
|---|---|---|---|
|SUM|Aggregation|❌ No|✅ Yes|
|SUMX|Iterator|✅ Yes|✅ Yes|
|COUNT|Aggregation|❌ No|✅ Yes|
|COUNTROWS|Aggregation|❌ No|✅ Yes|
|AVERAGEX|Iterator|✅ Yes|✅ Yes|

# ⚠ PL-300 Exam Traps

❌ Using `COUNT` for text columns  
❌ Using `SUMX` when `SUM` is enough  
❌ Forgetting `DISTINCTCOUNT` for uniqueness  
❌ Assuming COUNTROWS uses row context

