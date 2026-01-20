>**DAX (Data Analysis Expressions)** is a **formula language** used to create **calculations and logic** in data models.

>It helps you calculate numbers like **totals, averages, percentages, rankings, and time-based metrics** on top of your data.

---
# Row Context

Means Dax is evaluating one row at a time.
It is like iterating rows in table.

Power BI say - 
"I am currently on this row - calculate using only this row value".

Row context is creating by 
- Calculated columns.
- Iterators (SUMX, FILTER, AVERAGEX)

---
# Filter Context 

**Filter context** means **which data is currently selected** when a DAX measure runs.

👉 It’s created by:
- **Filters pane**
- **Slicers**
- **Rows/columns in a visual** (like Year, Region)
- **Page & report filters**

**Simple example**  
You have **Total Sales**.  
If you select **Year = 2024** and **Region = India**, the measure calculates sales **only for 2024 + India**.

**Key point for exam**

- Measures **always respect filter context**
- `CALCULATE()` can **change** filter context

---
# Context Transition

Row context is converted into filter context
This happens **when you use `CALCULATE()`**.

### Simple explanation

- **Row context** → happens in calculated columns / iterators (`SUMX`, `FILTER`)
- **Filter context** → what data is filtered (slicer, visual, etc.)
- **`CALCULATE()`** changes **row context → filter context**

> Calculate() only works with filter context it only touch row context during context transition

❌ Without context transition
```DAX
Customer Sales (Wrong) =
SUM ( Sales[Amount] )
```

✅ With context transition
```DAX
Customer Sales (Correct) =
CALCULATE ( SUM ( Sales[Amount] ) )
```

---
# Evaluation Order

Order in which power bi apply Filter and DAX.

### 1️⃣ Model Context (Applied First)

- **Active relationships only**
- **Row-Level Security (RLS)**
- Automatically applied before any report interaction

### 2️⃣ Report Context

- **Slicers**
- **Page-level filters**
- **Report-level filters**
- **Visual-level filters**
- **Cross-filtering / Cross-highlighting**

### 3️⃣ Row Context

- Created by:
    - **Calculated columns**
    - **Iterators** (`SUMX`, `FILTER`, `AVERAGEX`, etc.)
- **Row context alone does NOT filter data**
- Exists only for the **current row**

### 4️⃣ Context Transition

- Triggered by **`CALCULATE()`**    
- Converts **row context → filter context**
- Occurs mainly in:
    - Calculated columns
    - Iterators with `CALCULATE()`

### 5️⃣ `CALCULATE()` Filter Arguments

Applied **inside `CALCULATE()`** in this order:

a) Boolean filters
```DAX
Sales[Region] = "India"
```

b) Table filters
```DAX
FILTER ( Sales, Sales[Amount] > 1000 )
```

#### c) Filter modifiers

- `ALL()`
- `REMOVEFILTERS()`
- `KEEPFILTERS()`
- `USERELATIONSHIP()`

> These filters can **override or modify existing slicer filters**

### 6️⃣ Measure Evaluation (Final Step)

- Aggregations executed:
    
    - `SUM`
    - `COUNT`
    - `DISTINCTCOUNT`
    - `AVERAGE`
- Final value returned to the visual

> Trick
> MODEL -> SLICERS -> TRANSITION -> CALCULATED -> AGGREGATE.

---
# Filter Priority

**Highest priority → Lowest priority**

1. **Calculated filters** (`CALCULATE()` filters)
2. **Visual / Page / Report filters & Slicers**
3. **Row context**

```
By default, CALCULATE() filters override slicer filters
if they target the same column.
```

## One-line Final Summary

> **Power BI first applies model & report filters, then converts row context (if needed), applies CALCULATE filters, and finally aggregates.**

---

> NOTE
> 1. Slicers create the initial _filter context_
> 2. **Measure evaluation begins** using that filter context
> 3. `CALCULATE()` filters are applied next
> 	- If they target the **same column**, they **override slicer filters**
> 4. **The measure is finally computed** using the **modified filter context**

## EXAMPLE

```DAX
Total Sales :=
CALCULATE (
    SUM ( Sales[Amount] ),
    Sales[Region] = "India"
)
```

### Step-by-step evaluation

#### 1️⃣ Slicer creates initial filter context
User selects:
- **Region = USA**

👉 Initial filter context:
```DAX
Sales[Region] = "USA"
```

2️⃣ Measure evaluation begins
Power BI starts evaluating **`Total Sales`** using:
```
Region = USA
```
Like Total Sales will be calculated for USA Region

3️⃣ `CALCULATE()` filters are applied
Inside the measure:

```DAX
Sales[Region] = "India"
```

- Targets the **same column** as the slicer
- **Overrides** slicer filter

👉 New filter context becomes:

```DAX
Sales[Region] = "India"
```

4️⃣ Measure is finally computed

✔ Result = **Sales for India**,
❌ Slicer selection (USA) is ignored

