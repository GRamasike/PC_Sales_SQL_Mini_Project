# 💻 PC Sales End-to-End Data Engineering Project

![SQL](https://img.shields.io/badge/SQL-Server-blue?style=flat&logo=microsoftsqlserver) ![Excel](https://img.shields.io/badge/Data%20Source-CSV-green?style=flat) ![DrawIO](https://img.shields.io/badge/Data%20Modelling-Draw.io-orange?style=flat) ![Status](https://img.shields.io/badge/Status-In%20Progress-yellow) ![Domain](https://img.shields.io/badge/Domain-Retail%20Sales-purple)

---

## 📌 Project Overview

This project is something I am genuinely proud of. It goes beyond writing SQL queries and steps into real data engineering territory. The dataset is a simulated PC Sales file containing **10,000 records** from a retail business that operates across multiple continents, countries, and sales channels.

What makes this project different from my others is that I did not just query the data. I designed a proper data model from scratch, built out a full star schema in SQL Server, created stored procedures to load the data, and I am working towards automating the entire pipeline in the future.

> 🔮 **Future goal:** Automate the full ingestion and transformation pipeline so that no manual steps are required.

---

## 🏗️ Pipeline Architecture

```
[ Raw Data ]     [ Staging Layer ]          [ Data Warehouse ]      [ Analysis ]
  CSV File  →    computerstg database   →    computerdwh database →  ETL + Queries
               (Dim Tables, Stored           (Production ready,       (Coming soon)
                Procedures, Data             clean, validated data)
                Cleaning)
```

---

## 📐 Data Model

Before writing a single line of SQL, I analysed the raw CSV file and separated the data into related subject areas. I used **Draw.io** to design the schema visually, which gave me a clear picture of how the tables would relate to each other before I started building.

The result is a **Star Schema** made up of **10 dimension tables** and **1 central fact table**.

### Dimension Tables

| Table | Description |
|---|---|
| `dim_location` | Stores the continent, country or state, and province or city of each sale |
| `dim_shop` | Contains the shop name and how long the shop has been operating |
| `dim_pc` | Holds the PC manufacturer and model information |
| `dim_specifications` | Covers the storage type, RAM, and storage capacity of each PC |
| `dim_customer` | Stores customer details including name, contact number, and email address |
| `dim_salesperson` | Contains the salesperson name and their department |
| `dim_payment_method` | Records the payment method used for each transaction |
| `dim_date` | Stores the purchase date and ship date for each sale |
| `dim_channel` | Identifies whether the sale was made Online or Offline |
| `dim_priority` | Records the fulfilment priority level assigned to each order |

### Fact Table

| Table | Description |
|---|---|
| `fact_pcsales` | The central fact table that links all 10 dimensions together. It stores the measurable values for each sale including cost price, sale price, discount amount, finance amount, credit score, cost of repairs, total sales per employee, and the PC market price |

> 📝 Every dimension table includes a `LoadDate` column so that I can track exactly when each batch of data was loaded into the table.

---

## 📁 Database Setup

This project uses two separate databases to reflect a professional data engineering environment:

```sql
-- Staging Database (active)
IF DB_ID('computerstg') IS NULL
BEGIN
    CREATE DATABASE computerstg;
END
GO
USE computerstg;
GO

-- Data Warehouse Database (coming soon)
IF DB_ID('computerdwh') IS NULL
BEGIN
    CREATE DATABASE computerdwh;
END
GO
USE computerdwh;
GO
```

**computerstg** is the staging database where all the groundwork is being done. This is where the raw CSV data is loaded, the dimension tables are built, and the stored procedures run. It is also where the data cleaning and transformation work is being carried out to ensure the data is clean and consistent before it moves any further.

**computerdwh** is the data warehouse database that will serve as the production environment. It will only receive data once the ETL pipeline is ready and the data has been properly validated in the staging layer. This separation ensures that no raw or inconsistent data ever reaches production.

---

## 📂 Repository Structure

```
💻 PC-Sales-Data-Engineering
│
├── 📄 README.md
├── 📊 star_schema_drawio.pdf
│
├── 📁 dim_tables/
│   ├── dim_location.sql
│   ├── dim_shop.sql
│   ├── dim_pc.sql
│   ├── dim_specifications.sql
│   ├── dim_customer.sql
│   ├── dim_salesperson.sql
│   ├── dim_payment_method.sql
│   ├── dim_date.sql
│   ├── dim_channel.sql
│   └── dim_priority.sql
│
├── 📁 stored_procedures/
│   ├── sp_load_dim_location.sql
│   ├── sp_load_dim_shop.sql
│   ├── sp_load_dim_pc.sql
│   ├── sp_load_dim_specifications.sql
│   ├── sp_load_dim_customer.sql
│   ├── sp_load_dim_salesperson.sql
│   ├── sp_load_dim_payment_method.sql
│   ├── sp_load_dim_date.sql
│   ├── sp_load_dim_channel.sql
│   └── sp_load_dim_priority.sql
│
├── 📄 exec_procedures.sql
├── 📄 drop_procedures.sql
│
├── 📁 fact_table/
│   └── fact_pcsales.sql
│
```

---

## 🔍 Key Data Engineering Concepts Demonstrated

**Star Schema Design** sits at the heart of this project. Rather than working with a single flat table, I separated the raw data into facts and dimensions to create a structure that is easier to query, maintain, and scale.

**Dimensional Modelling** was applied across all 10 dimension tables, each with its own surrogate primary key that links back to the central fact table.

**Data Modelling with Draw.io** meant that the entire schema was planned visually before any code was written. This is a habit I picked up from studying project management and it makes a real difference when building anything complex.

**Stored Procedures** were written for each dimension table to handle the data loading process in a consistent and repeatable way. A separate script executes all procedures and another script drops them when needed, keeping the codebase clean and organised.

**LoadDate Tracking** was added to every dimension table so that each data load can be identified and traced back if needed.

---

## 🔮 Future Enhancements

- [ ] Complete data cleaning and transformation in the staging layer
- [x] Build and populate the `fact_pcsales` table
- [ ] Build and deploy the ETL pipeline from `computerstg` to `computerdwh`
- [ ] Automate the CSV ingestion pipeline
- [ ] Set up a scheduled data refresh
- [ ] Connect to a reporting or visualisation tool

---

## 🧠 Why We Code It This Way

One of the goals of this project is not just to write code that works, but to write code that is safe, repeatable, and production ready. Below are some of the key patterns used in this project and the reasoning behind them.

---

### Checking if a Database Exists Before Creating It

```sql
IF DB_ID('computerstg') IS NULL
BEGIN
    CREATE DATABASE computerstg;
END
GO
```

Rather than simply running `CREATE DATABASE`, this pattern first checks whether the database already exists using `DB_ID()`. If the database is found, `DB_ID()` returns its internal ID. If it does not exist, it returns NULL and the `CREATE DATABASE` statement runs safely inside the `BEGIN...END` block. This means the script can be run multiple times without throwing an error, which is important in a professional environment where scripts are often re-executed.

---

### Auto Generating Surrogate Primary Keys with IDENTITY

```sql
[LocationId] [INT] IDENTITY(1,1) PRIMARY KEY
```

Instead of manually assigning ID values, `IDENTITY(1,1)` tells SQL Server to automatically generate a unique integer for each new row, starting at 1 and incrementing by 1. This ensures every record has a unique identifier without any manual input, which is a standard practice in dimensional modelling and data warehousing.

---

### Using DISTINCT When Loading from Raw Data

```sql
SELECT DISTINCT
    [Continent],
    [Country_or_State],
    [Province_or_City]
FROM [computerstg].[dbo].[raw_data]
```

Raw data files often contain duplicate rows. Using `DISTINCT` ensures that only unique combinations of values are loaded into the dimension table, keeping the data clean and avoiding unnecessary repetition in the warehouse.

---

### Automatically Stamping the Load Date

```sql
[LoadDate] DATETIME DEFAULT GETDATE()
```

Every dimension table includes a `LoadDate` column that automatically records the date and time the data was loaded using `GETDATE()`. This is useful for auditing, troubleshooting, and tracking data freshness. In a production environment, knowing when data was last loaded is essential for maintaining trust in the data.

---

> 📝 **Ongoing Lesson:** As this project progresses, the table creation scripts will be updated to check whether a table already exists before attempting to drop it. This follows the same safe and repeatable philosophy applied to the database creation scripts above.

---

### Avoiding Data Explosion When Building the Fact Table

One of the most important lessons from building the `fact_pcsales` table was understanding how joins can cause data to multiply unexpectedly. When joining multiple dimension tables back to the raw data, an incorrectly written join can match one row in the raw data to many rows in a dimension table, causing the same record to appear multiple times in the fact table. This is known as a data explosion.

The solution was to carefully structure each join to ensure that every dimension key matched back to exactly one row, keeping the grain of the fact table consistent and the record count accurate. This is a fundamental concept in dimensional modelling and one that every data engineer encounters when building their first fact table.

---



## 🛠️ Tools Used

**CSV** was the starting point, providing the raw simulated sales data for the project.

**Draw.io** was used to design the star schema and visualise the relationships between tables before any code was written.

**SQL Server** was used to build the database, create the dimension tables, and write the stored procedures.

**SSMS (SQL Server Management Studio)** was used throughout for script development and testing.

---

## 👤 About Me

I am a **BSc IT Graduate** with 6 years of professional experience as a **Batch Processing Administrator** at a credit bureau, where I worked extensively with large volumes of sensitive financial data in a production environment.

With a solid academic foundation in **Database Management, Mathematics for Computer Science, and Project Management**, combined with hands-on industry experience in data operations, I am now transitioning into **SQL Development and Data Engineering** and building on skills I have spent years applying professionally.

This project is part of a growing portfolio designed to demonstrate my technical capabilities in database design, querying, and data analysis.

📫 Feel free to connect with me on [(https://www.linkedin.com/in/gomolemo-ramasike/)](#) or explore my other projects here on GitHub!
This project is part of a growing portfolio designed to demonstrate my technical capabilities in database design, querying, and data analysis.

