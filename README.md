# 💻 PC Sales SQL Project
---

## 📌 Project Overview

This project focuses on exploring and analysing a **PC Sales dataset** using SQL Server. The dataset contains sales records from a retail PC business operating across multiple continents, countries, and sales channels.

The goal of this project is to answer **30 analytical business questions** using SQL — progressing from basic data exploration through to advanced window functions and profitability analysis.

---

## 📁 Dataset

The dataset contains the following fields:

| Field | Description |
|---|---|
| Purchase Date & Ship Date | Transaction and fulfilment dates |
| Shop Name | Retail location of the sale |
| Sales Person Name & Department | Employee and team responsible for the sale |
| PC Make, Model & Storage | Product specifications |
| RAM & Storage Type | Hardware configuration details |
| Sale Price & Cost Price | Revenue and cost per transaction |
| PC Market Price | Recommended retail price for comparison |
| Discount Amount | Discount applied to the sale |
| Finance Amount | Finance issued to the customer |
| Payment Method | How the customer paid |
| Channel | Online vs Offline sales |
| Priority Level | Order fulfilment priority |
| Credit Score | Customer credit profile |
| Cost of Repairs | Post-sale repair costs |
| Continent & Country/State | Geographic location of the sale |

---

## 📁 Database Setup

```sql
CREATE DATABASE PC_Sales;
USE PC_Sales;
```

**Main table:** `pc_data` — 10,000 rows of PC sales records

---

## 📂 Repository Structure

The 30 queries are split across three files, organised by difficulty level to show progression in SQL complexity:

| File | Level | Description |
|---|---|---|
| `PCSales_Foundations.sql` | 🟢 Beginner | Basic SELECT, COUNT, and filtering queries |
| `PCSales_Exploration.sql` | 🟡 Intermediate | Revenue, profit, and aggregation by category |
| `PCSales_Analysis.sql` | 🔴 Advanced | Profit margins, rankings, date functions, and window functions |

---

## 🎯 Project Objective

Use **SQL queries** to explore, filter, and analyse the dataset. This project focuses on:

- Extracting meaningful business insights from retail sales data
- Translating business questions into structured SQL queries
- Demonstrating progression from foundational to advanced SQL concepts

---

## 🔍 Key SQL Skills Demonstrated

- Basic `SELECT` queries & column aliasing
- `WHERE` filtering & multi-condition logic
- `COUNT`, `SUM`, `AVG`, `MAX`, `MIN` aggregations
- `GROUP BY` for grouped analysis
- Calculated fields — profit, profit margin, days to ship
- `DATEDIFF` and `TRY_CONVERT` for date calculations
- `TOP` for ranking results
- **Window functions** — `RANK()` for ranking sales performance

---

## 📊 Key Findings

| # | Insight |
|---|---|
| 🌍 | Coming soon |
| 💰 | Coming soon |
| 🏆 | Coming soon |
| 📦 | Coming soon |
| 📈 | Coming soon |

---

## 🛠️ Tools Used

- **SQL Server** — database creation and querying
- **SSMS (SQL Server Management Studio)** — query development and testing

---

## 👤 About Me

I am a **BSc IT Graduate** with 6 years of professional experience as a **Batch Processing Administrator** at a credit bureau, where I worked extensively with large volumes of sensitive financial data in a production environment.

With a solid academic foundation in **Database Management, Mathematics for Computer Science, and Project Management**, combined with hands-on industry experience in data operations, I am now transitioning into **SQL Development and Data Engineering** — building on skills I have spent years applying professionally.

This project is part of a growing portfolio designed to demonstrate my technical capabilities in database design, querying, and data analysis.

📫 Feel free to connect with me on (https://www.linkedin.com/in/gomolemo-ramasike/)(#) or explore my other projects here on GitHub!
