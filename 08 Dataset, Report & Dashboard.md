## ✅ What is a Dataset?

A **Dataset** is the **data model behind Power BI reports**  
(It is now officially called a **Semantic Model**).

---
## 🧠 Definition

> A dataset contains all data, relationships, and business logic used to build reports.

---
## 📦 What a Dataset Contains

### 🔹 Tables

- Fact tables
- Dimension tables

### 🔹 Relationships

- 1:* 
- Single or Bi-directional
- Based on keys (e.g., Date, CustomerID)

### 🔹 Measures

- DAX calculations
- Evaluated at **query time**

### 🔹 Calculated Columns

- Row-by-row calculations
- Stored in the model

### 🔹 Data Source Connections

- SQL Server
- Snowflake
- Excel
- APIs, etc.

### 🔹 Refresh Settings

- Scheduled refresh
- Incremental refresh
- Credentials & gateway

---
## 📍 Where Dataset Exists

### 🔹 Power BI Desktop

- Created and designed here
- Data modeling & transformations done here
- Measures & columns authored here

### 🔹 Power BI Service

- Dataset is **published** to Service
- Stored in workspace
- Can be reused across reports

---
## 🔁 One Dataset → Multiple Reports

✔ Same dataset can power **many reports**  
✔ Centralized business logic  
✔ Single version of truth

---
## 🔄 Data Transformation Rules

|Location|What can be done|
|---|---|
|Power BI Desktop|Transform data (Power Query)|
|Power BI Service|❌ No data transformation|
|Both|Create / edit measures|

---
# **Report (Power BI)**

## ✅ What is a Report?

A **Report** is a **collection of interactive pages** built on top of a **Dataset (Semantic Model)**.

> Reports are used to **visualize and analyze data**.

---
## 📦 What a Report Contains

### 🔹 Visuals

- Charts (bar, line, pie, etc.)
- Tables & matrices
- KPIs & cards
- Custom visuals

### 🔹 Pages

- Single-page or multi-page reports
- Each page can have different visuals and filters

### 🔹 Filters & Slicers

- Visual-level filters
- Page-level filters
- Report-level filters
- Slicers for user interaction

### 🔹 Advanced Features

- **Drill-through** pages
- **Bookmarks** (for navigation, storytelling)
- **Tooltips**
- **Buttons & navigation**

### 🔹 Multiple Pages

- Logical separation of analysis
- E.g., Overview, Sales, Finance, Operations

---
## 📍 Where a Report Exists

### 🔹 Power BI Desktop

- Reports are **created and designed**
- Visuals, pages, filters added here
- Connected to a dataset

### 🔹 Power BI Service

- Reports are **published**
- Stored in a workspace
- Can be shared with users

---
## ✏ Editing Reports (Important for PL-300)

|Location|Can Edit Report?|
|---|---|
|Power BI Desktop|✅ Full editing|
|Power BI Service|✅ Edit visuals & pages|
|Power BI Service|❌ Cannot transform data|

---
# **Dashboard (Power BI)**

## ✅ What is a Dashboard?

A **Dashboard** is a **single-page canvas** in **Power BI Service** made by **pinning visuals** from one or more reports.

> Dashboards provide a **high-level overview** of key metrics.

---
## 📍 Where a Dashboard Exists

- ✅ **Only in Power BI Service**
- ❌ Cannot be created in Power BI Desktop

---
## 📦 What a Dashboard Contains

### 🔹 Tiles

- Visual tiles pinned from reports
- KPI tiles
- Text tiles
- Image tiles
- Web content tiles

### 🔹 Data Sources

- Can combine visuals from **multiple datasets**
- Ideal for **executive-level monitoring**

---
## 🚫 What a Dashboard Does NOT Contain

❌ Pages (single page only)  
❌ Filters & slicers  
❌ Drill-through  
❌ Data model or relationships

---
## 🔁 Dashboard vs Report (Important for PL-300)

|Feature|Dashboard|Report|
|---|---|---|
|Pages|❌ Single page|✅ Multiple|
|Created in Desktop|❌ No|✅ Yes|
|Created in Service|✅ Yes|✅ Yes|
|Filters & slicers|❌ No|✅ Yes|
|Drill-through|❌ No|✅ Yes|
|Multiple datasets|✅ Yes|❌ No|

---
## 📌 Interactions

- Clicking a tile opens the **source report**
- Dashboards are **read-only**
- Used mainly for **monitoring & alerts**

---
## ⏰ Alerts (Unique Feature)

✔ Alerts can be set on **dashboard tiles**  
✔ Not available on report visuals

Example:

> Notify me when Sales > 10M


