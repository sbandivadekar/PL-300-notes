## What is Data Profiling?

> **Data Profiling** means **understanding the quality, structure, and content of data** before using it in **reports or data models**.


📌 Purpose:

- Identify data issues early
- Improve data quality
- Avoid wrong insights in reports

🧠 **PL-300 Tip**

> Data profiling is **mainly done in Power Query**, not in the model.

---
## Where Data Profiling Happens

- **Power Query Editor*
- View options:
    - Column Quality
    - Column Distribution
    - Column Profile

---
## 1️⃣ Column Quality

### What it shows

Column Quality displays the **health of data** in each column.

### 🔹 Indicators

- 🟢 **Valid (Green)** → Correct values
- 🔴 **Error (Red)** → Data errors (conversion, calculation issues)
- ⚪ **Empty (Gray)** → NULL or missing values

### 📌 Why it is used

- Quickly identify data issues
- Detect missing or error-prone columns
- Decide where cleansing is required

---
## 2️⃣ Column Distribution

### What it shows

- **Distinct count**
- **Unique count**
- **Value frequency (bar chart)**

### 📌 Used to

- Find **duplicates**
- Detect **unexpected values**
- Understand **cardinality** (low vs high)

---
### 🔹 Unique Values

- Values that appear **only once**

**Example**
```
A, A, B, B, C
Unique count = 1   (only C appears once)
```


### 🔹 Distinct Values

- Number of **different values**

**Example**
```
A, A, B, B, C
Distinct count = 3  (A, B, C)
```


### 🔹 Identifying Duplicates

✔ **Duplicate rows formula**
```FORMULA
Duplicate rows = Total rows − Unique rows
```

✔ **Rule**
```RULE
If Distinct Values > Unique Values → Duplicates exist
```

> Column Distribution helps detect **duplicates and cardinality issues**.

---
## 3️⃣ Column Profile

### What it is

Column Profile provides **detailed statistics** for a column.
### 🔹 Includes

- Minimum
- Maximum
- Average
- Standard deviation
- Null count
- Value distribution
### 📌 Used to

- Validate **value ranges**
- Spot **outliers**
- Understand **numerical spread**
- Perform **deep column analysis**

---
## Quick Comparison

|Feature|Purpose|
|---|---|
|Column Quality|Check errors & nulls|
|Column Distribution|Find duplicates & cardinality|
|Column Profile|Statistical analysis|
