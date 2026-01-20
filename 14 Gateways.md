## ✅ What is a Gateway?

A **Power BI Gateway** is a **bridge** that allows **Power BI Service (cloud)** to securely access **on-premises data sources**.

> Power BI Service **cannot directly access on-prem data** — the gateway makes it possible.

---
## 🧠 Simple Mental Model

```
Power BI Service (Cloud)
        ⬇
     Gateway
        ⬇
On-Prem Data (SQL, File, SAP, etc.)
```

- Gateway is installed **inside your network**
- It **pushes data out** to Power BI Service
- No inbound firewall ports required

---
## 📍 Where Gateway Is Installed

- On a **Windows machine**
- Inside the **same network** as the data source
- Can be:
    - Physical server
    - Virtual machine
    - Always-on desktop (not recommended for prod)

---
# Why Gateway Is Needed

You need a gateway when:

- Data source is **on-premises**
- Using **Scheduled Refresh**
- Using **DirectQuery / Live connection**
- Using **Dataflows with on-prem sources**

### You do **NOT** need a gateway when:

- Data source is **cloud-based** (Azure SQL, Snowflake, BigQuery, etc.)
- Importing from public web sources

---
# 🔄 Gateway & Refresh

## 🔹 Scheduled Refresh

- Power BI Service triggers refresh
- Gateway pulls data from on-prem source
- Data loaded into dataset

## 🔹 DirectQuery / Live

- Queries run **in real time**
- Gateway stays active
- Performance depends on:
    - Network
    - Data source
    - Gateway machine

