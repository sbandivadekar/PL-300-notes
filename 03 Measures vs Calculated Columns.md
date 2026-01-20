## 🔹 Measures

### What it is

- A **dynamic calculation**
- Evaluated **at query time**

```DAX
Total Sales = SUM ( Sales[Amount] )
```

### Key Characteristics

- Uses **Filter Context**
- Calculated **when user interacts** with report
- **Not stored** in model
- Very **memory efficient**

### When to Use Measures

✔ Aggregations (SUM, AVG, COUNT)  
✔ KPIs & business metrics  
✔ Calculations depending on slicers  
✔ Time intelligence  
✔ Anything that must **change dynamically**

---
## 🔹 Calculated Columns

### What it is

- A **DAX expression evaluated row by row**
- Result is **stored in the model**

```DAX
Sales Category =
IF ( Sales[Amount] > 1000, "High", "Low" )
```

### Key Characteristics

- Uses **Row Context**
- Calculated **during data refresh**
- Value is **static until next refresh**
- Occupies **memory**

### When to Use Calculated Columns

✔ Row-level classification (High / Low)  
✔ Create **relationships**  
✔ Use as **Axis / Legend / Slicer**  
✔ Sorting (Sort by column)  
✔ Logic that does **not depend on filters**

---
## 🔄 Comparison Table

|Feature|Calculated Column|Measure|
|---|---|---|
|Evaluation|Data refresh|Query time|
|Context|Row Context|Filter Context|
|Stored in model|✅ Yes|❌ No|
|Uses memory|❌ High|✅ Low|
|Dynamic|❌ No|✅ Yes|
|Used in slicers|✅ Yes|❌ No|
|Used in values|⚠ Limited|✅ Best|
|Performance|Slower for large data|Faster|

---
## 🚀 Performance & Memory (VERY IMPORTANT)

### Calculated Columns

❌ Increase **model size**  
❌ Increase **refresh time**  
❌ Slow with large datasets

### Measures

✅ Calculated only when needed  
✅ Minimal memory usage  
✅ Best for performance

👉 **PL-300 Rule**

> **If it can be a Measure → it SHOULD be a Measure**

