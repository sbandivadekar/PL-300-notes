# Boolean vs filter()

|Feature|Boolean Filter|FILTER()|
|---|---|---|
|Input type|Column condition|Table|
|Evaluation|Column-level|Row-by-row|
|Performance|🚀 Faster|🐢 Slower|
|Supports measures|❌ No|✅ Yes|
|Complex logic|❌ No|✅ Yes|
|Preferred when|Simple equality|Business logic|

---
# **Filters overwrite v/s intersect**

## 🔹 Filter Overwrite (CALCULATE – Default Behavior)

### 📌 When to use

- When you want to **replace** the existing filter coming from:
    
    - Slicers
    - Page / report filters
    - Visual filters

### 🧠 How it works

- `CALCULATE()` **removes existing filters** on the same column
- Applies the **new filter condition**
- This is the **default behavior** of `CALCULATE`

### ✅ Example
```DAX
Total Sales India =
CALCULATE (
    SUM ( Sales[Amount] ),
    Sales[Region] = "India"
)
```
🔍 If slicer selects:

- USA → ❌ ignored
- India → ✅ applied
- USA + India → ❌ replaced → only India is used

👉 **Slicer filter is overwritten**

---
## 🔹 Filter Intersection (KEEPFILTERS)

### 📌 When to use

- When you want to **add a filter** to the **existing filter context**
- Slicer + measure filter should **work together**

### 🧠 How it works

- `KEEPFILTERS()` **keeps slicer filters**
- Applies **intersection** of:
    - Existing filters
    - New filter condition

### ✅ Example
```DAX
Total Sales India (Respect Slicer) =
CALCULATE (
    SUM ( Sales[Amount] ),
    KEEPFILTERS ( Sales[Region] = "India" )
)
```
🔍 If slicer selects:

- USA → ❌ blank (USA ∩ India = empty)
- India → ✅ India sales
- USA + India → ✅ India sales

👉 **Filters are intersected**

