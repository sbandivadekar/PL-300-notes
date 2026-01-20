## 🔹 What VAR Does

`VAR` allows you to:

- Store the **result of a DAX expression**
- Reuse it multiple times in the same expression
- Make DAX **clearer, safer, and faster**
- Works like a **constant** → cannot be redefined
-  **Always requires a `RETURN` statement**

```DAX
VAR TotalSales = SUM ( Sales[Amount] )
RETURN
TotalSales * 0.1
```

✔ Improves readability  
✔ Avoids repeated calculations  
✔ Reduces errors

### Key Rules (Exam Important)

- `VAR` **respects slicers and filters**
- Evaluated **once per filter context**
- Scope is **only within the measure**
- Cannot change value after assignment

---
## 🔹 Performance Benefits

### Without VAR (Bad Practice)

```DAX
Profit % =
DIVIDE (
    SUM ( Sales[Profit] ),
    SUM ( Sales[SalesAmount] )
)
```

### With VAR (Best Practice)

```DAX
Profit % =
VAR Profit = SUM ( Sales[Profit] )
VAR Sales  = SUM ( Sales[SalesAmount] )
RETURN
DIVIDE ( Profit, Sales )
```
### Why VAR is Faster

- Expression evaluated **once**
- Reduced CPU usage
- Optimized query plan
- Cleaner execution

✔ Especially important on **large datasets**
