## 🔴 Prerequisite (VERY IMPORTANT)

All **time intelligence** functions require a **proper Date table**:

✔ Continuous dates  
✔ Unique date column  
✔ Data type = Date  
✔ Mark as Date Table  
✔ Relationship: Date[Date] → Fact[Date]

If this is missing → results will be **wrong or blank**.


---
## ✅ TOTALYTD()

### 📌 What it does

Calculates **Year-to-Date total** from **Jan 1 → current date**.

### 🧠 Meaning

> “Add all values from the start of the year until today (based on filter context).”

```DAX
Total Sales YTD =
TOTALYTD (
    SUM ( Sales[Amount] ),
    'Date'[Date]
)
```
### 🧠 Example

If today = **15 Aug 2024**,  
→ sums sales from **1 Jan 2024 → 15 Aug 2024**

---
## ✅ TOTALMTD()

### 📌 What it does

Calculates **Month-to-Date total**.

```DAX
Total Sales MTD =
TOTALMTD (
    SUM ( Sales[Amount] ),
    'Date'[Date]
)
```
### 🧠 Example

If today = **15 Aug**  
→ sums sales from **1 Aug → 15 Aug**

---
## ✅ TOTALQTD()

### 📌 What it does

Calculates **Quarter-to-Date total**.

```DAX
Total Sales QTD =
TOTALQTD (
    SUM ( Sales[Amount] ),
    'Date'[Date]
)
```

Starting of the Quarter to current date.

---
## ✅ DATESYTD()

### 📌 What it does

Returns **all dates from start of year to current date**.

```DAX
Sales YTD =
CALCULATE (
    SUM ( Sales[Amount] ),
    DATESYTD ( 'Date'[Date] )
)
```

---
## ✅ DATESMTD()

Returns **all dates from start of month to current date**.

```DAX
Sales MTD =
CALCULATE (
    SUM ( Sales[Amount] ),
    DATESMTD ( 'Date'[Date] )
)
```

---
## ✅ DATESQTD()

```DAX
Sales QTD =
CALCULATE (
    SUM ( Sales[Amount] ),
    DATESQTD ( 'Date'[Date] )
)
```

---
## ✅ DATESINPERIOD()

Returns dates for a **custom rolling period**.

### Syntax
```DAX
DATESINPERIOD (
    'Date'[Date],
    <start_date>,
    <number>,
    <interval>
)
```

🔹 Example: Last 30 Days Sales

```DAX
Sales Last 30 Days =
CALCULATE (
    SUM ( Sales[Amount] ),
    DATESINPERIOD (
        'Date'[Date],
        MAX ( 'Date'[Date] ),
        -30,
        DAY
    )
)
```

We can pass Day/Month/Quarter/Year

---
## ✅ PARALLELPERIOD()

Shifts the **whole period** by N months/quarters/years.

### Syntax
```DAX
PARALLELPERIOD (
    'Date'[Date],
    -1,
    YEAR
)
```

🔹 Example: Previous Year Sales
```DAX
Sales PY =
CALCULATE (
    SUM ( Sales[Amount] ),
    PARALLELPERIOD ( 'Date'[Date], -1, YEAR )
)
```

### ⚠ Important

- Preserves **same shape of period**
- Often replaced by SAMEPERIODLASTYEAR

---
## ✅ SAMEPERIODLASTYEAR()

Returns **exact same date range last year**.

```DAX
Sales LY =
CALCULATE (
    SUM ( Sales[Amount] ),
    SAMEPERIODLASTYEAR ( 'Date'[Date] )
)
```
### 🧠 Example

If current filter = **1–15 Aug 2024**  
→ returns **1–15 Aug 2023**

---
## ✅ DATEADD()

Shift dates **by days, months, or years**
Moves the date **row by row**.

### Syntax
```DAX
DATEADD (
    'Date'[Date],
    -1,
    YEAR
)
```

### 🔹 Example: Previous Year Sales

```DAX
Sales PY (DateAdd) =
CALCULATE (
    SUM ( Sales[Amount] ),
    DATEADD ( 'Date'[Date], -1, YEAR )
)
```

---
## DATEADD vs SAMEPERIODLASTYEAR

|Function|Use|
|---|---|
|SAMEPERIODLASTYEAR|Standard YoY|
|DATEADD|Custom shifts (2 years back, 6 months, etc.)|

---
## Summary Cheat Sheet (PL-300 MUST REMEMBER)

|Function|Purpose|
|---|---|
|TOTALYTD|Quick YTD|
|TOTALMTD|Quick MTD|
|TOTALQTD|Quick QTD|
|DATESYTD|YTD date table|
|DATESINPERIOD|Rolling periods|
|PARALLELPERIOD|Shift full period|
|SAMEPERIODLASTYEAR|YoY comparison|
|DATEADD|Custom date shift|
