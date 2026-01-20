# CALCULATE()

- **Evaluates an expression in a modified filter context**
- **Changes the existing filter context before evaluating the expression**
- It is the **most important function in DAX**

### How `CALCULATE()` works

### 1️⃣ Modify Filter Context

`CALCULATE()` can:
- **Add filters**
- **Replace existing filters**
- **Remove filters**

Using:
- Boolean filters (`Column = Value`)
- Table filters (`FILTER()`)
- Filter modifiers (`ALL`, `REMOVEFILTERS`, `KEEPFILTERS`, `USERELATIONSHIP`)

### 2️⃣ Trigger Context Transition

- Converts **row context → filter context**
- Happens **only if row context exists**
- Common in:
    - Calculated columns
    - Iterators (`SUMX`, `FILTER`) with `CALCULATE()`

### Syntax
```DAX
CALCULATE (
    <expression>,
    <filter1>,
    <filter2>,
    ...
)
```

## Evaluation Order inside `CALCULATE()`

1. **Existing filters**  
    (Visual filters, slicers, page/report filters)
    
2. **`CALCULATE()` filter arguments applied**
    - Override or modify existing filters
    
3. **Expression is evaluated**
    - `SUM`, `COUNT`, etc.


### Example: `CALCULATE()` overriding slicer
```DAX
Sales India =
CALCULATE (
    SUM ( Sales[Amount] ),
    Sales[Region] = "India"
)
```


## One-line PL-300 Memory 🧠

> **CALCULATE = Change filters first, then calculate**

---
# `CALCULATE()` Filter Modifiers

Filter modifiers **change how existing filters behave** inside `CALCULATE()`.

### 1️⃣ `ALL()`

### What it does
- **Removes filters** from a table or column
- Ignores slicers and visual filters
- return table.

### Example
```DAX
Total Sales (All Regions) =
CALCULATE (
    SUM ( Sales[Amount] ),
    ALL ( Sales[Region] )
)
```
Shows total sales for **all regions**, even if slicer filters one.

### 2️⃣ `REMOVEFILTERS()`

### What it does

- Removes filters (same purpose as `ALL`)
- **Preferred in modern DAX** (more readable)
- doesn't return table.
### Example
```DAX
Total Sales (Ignore Region) =
CALCULATE (
    SUM ( Sales[Amount] ),
    REMOVEFILTERS ( Sales[Region] )
)
```
Cleaner alternative to `ALL()`.

### 3️⃣ `KEEPFILTERS()`

### What it does

- **Preserves existing filters**
- Intersects slicer filter + CALCULATE filter
- Add filter instead of replacing them
### Example
```DAX
Sales India (Keep Slicer) =
CALCULATE (
    SUM ( Sales[Amount] ),
    KEEPFILTERS ( Sales[Region] = "India" )
)
```

If the slicer region  = USA and Calculated filter = INDIA then power will intersect the filter
rows where Region is USA and INDIA 

Meaning in single value of region should have both india and usa if there is not such value then it return blank.

### 4️⃣ `USERELATIONSHIP()`

### What it does

- Activates an **inactive relationship** temporarily
- Only works inside `CALCULATE()`
    
### Example
```DAX
Sales by Ship Date =
CALCULATE (
    SUM ( Sales[Amount] ),
    USERELATIONSHIP ( Sales[ShipDate], Date[Date] )
)
```
Uses **Ship Date** instead of Order Date.

### 5️⃣ `CROSSFILTER()`

### What it does

- Changes **filter direction** between tables
- Can enable or disable cross-filtering

### Example
```DAX
Sales (Both Directions) =
CALCULATE (
    SUM ( Sales[Amount] ),
    CROSSFILTER ( Sales[ProductID], Product[ProductID], BOTH )
)
```
🔹 Temporarily changes relationship direction.

### 6️⃣ `ALLSELECTED()`

### What it does

- Removes **visual-level filters**
- Keeps slicers and page/report filters
### Example
```DAX
Sales % of Selection =
DIVIDE (
    SUM ( Sales[Amount] ),
    CALCULATE ( SUM ( Sales[Amount] ), ALLSELECTED ( Sales ) )
)
```
🔹 Used for **% of total within selection**.

### 7️⃣`ALLEXCEPT()` 

- **Removes all filters from a table _except_ the specified columns**
- Commonly used to **keep one grouping** (like Category or Year) while ignoring others

### Example
```DAX
Sales by Category (Ignore Others) =
CALCULATE (
    SUM ( Sales[Amount] ),
    ALLEXCEPT ( Sales, Sales[Category] )
)
```
### What happens

- Keeps filter on **Category**
- Removes filters on **Region, Date, Product**, etc.
- Result = sales **per category**, unaffected by other slicers

---
# ALL() v/s REMOVEFILTERS()

|Feature|`ALL()`|`REMOVEFILTERS()`|
|---|---|---|
|Removes filters|✅|✅|
|Returns a table|✅|❌|
|Used outside `CALCULATE()`|✅|❌|
|Readability|Medium|⭐ High|
|Recommended by Microsoft|❌|✅|

## When to use which?

### Use `REMOVEFILTERS()` when:

- You **only want to clear filters**
- Writing clean, readable measures

### Use `ALL()` when:

- You need an **unfiltered table**
- Creating **% of total** logic
- Used inside iterators (`SUMX`, `FILTER`)

> REMOVEFILTERS() is better than ALL() when it comes to performance.

