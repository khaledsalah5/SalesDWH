# Sales Data Warehouse ETL — SSIS

## Overview

This project implements an **SSIS-based ETL pipeline for a Sales Data Warehouse**. It extracts data from a sales OLTP database, loads dimensional tables, and incrementally processes sales facts into an analytics-ready warehouse.

The project demonstrates common Data Engineering and Data Warehousing patterns using the Microsoft data stack.

---

## Architecture

```text
Sales OLTP Database
        │
        ▼
   SSIS ETL Layer
        │
        ├── Customer Dimension
        ├── Product Dimension
        ├── Salesman Dimension
        │
        ▼
 Dimensional Warehouse
        │
        ▼
Incremental Sales Fact Load
```

The repository separates dimension loading from fact processing so dimensions can be prepared before sales facts reference them.

---

## ETL Packages

### `CustomerDim.dtsx`

Loads and transforms customer data into the customer dimension.

### `ProductDim.dtsx`

Loads product information from the source system into the product dimension.

### `SalesmanDim.dtsx`

Loads salesperson / salesman data into the corresponding warehouse dimension.

### `Sales_incremental_Load_fact.dtsx`

Processes the sales fact table using an **incremental load pattern**, avoiding the need to fully reload historical sales data on every execution.

---

## Repository Structure

```text
SalesDWH
│
├── Sales_DWH_ETL.sln
│
└── Sales_DWH_ETL/
    ├── CustomerDim.dtsx
    ├── ProductDim.dtsx
    ├── SalesmanDim.dtsx
    ├── Sales_incremental_Load_fact.dtsx
    │
    ├── KHALED_SQLSERVERDEV.Sales_OLTP.conmgr
    ├── KHALED_SQLSERVERDEV.Sales_Dim.conmgr
    │
    ├── Project.params
    ├── Sales_DWH_ETL.dtproj
    └── Sales_DWH_ETL.database
```

---

## Data Flow

The intended ETL sequence is:

```text
1. Load Customer Dimension
2. Load Product Dimension
3. Load Salesman Dimension
4. Load new Sales Fact records incrementally
```

Loading dimensions first ensures that the warehouse has the required dimension records before fact data is processed.

---

## Tech Stack

- **SQL Server Integration Services (SSIS)**
- **Microsoft SQL Server**
- **T-SQL**
- **Visual Studio / SQL Server Data Tools**
- **Data Warehousing**
- **Dimensional Modeling**
- **Incremental ETL**

---

## Connection Managers

The SSIS project contains separate connection managers for the operational source and dimensional warehouse:

```text
KHALED_SQLSERVERDEV.Sales_OLTP.conmgr
KHALED_SQLSERVERDEV.Sales_Dim.conmgr
```

This keeps the transactional source and analytics destination logically separated.

---

## How to Run

### 1. Clone the repository

```bash
git clone https://github.com/khaledsalah5/SalesDWH.git
cd SalesDWH
```

### 2. Open the solution

Open:

```text
Sales_DWH_ETL.sln
```

in Visual Studio with **SQL Server Integration Services Projects / SSDT** installed.

### 3. Configure SQL Server connections

Update the project connection managers to point to your local or development SQL Server environment:

- Sales OLTP source database
- Sales dimensional warehouse database

### 4. Run dimension packages

Execute the dimension packages before the fact load:

```text
CustomerDim.dtsx
ProductDim.dtsx
SalesmanDim.dtsx
```

### 5. Run the incremental fact load

Execute:

```text
Sales_incremental_Load_fact.dtsx
```

to process new sales records into the fact table.

### 6. Validate the load

After execution, verify:

- dimension row counts;
- fact-table row counts;
- newly inserted sales records;
- key relationships between facts and dimensions.

---

## Data Engineering Concepts Demonstrated

### Dimensional Modeling

The project organizes business entities such as customers, products, and salespeople into dimensions while sales transactions are represented in the fact layer.

### ETL Dependency Management

Dimensions are populated before facts to ensure the required dimension records are available when transactional data is loaded.

### Incremental Loading

Instead of rebuilding the entire fact table every time, the sales fact package focuses on loading new data. This pattern reduces unnecessary processing and is important for scalable production ETL systems.

### Source and Warehouse Separation

Separate connection managers represent the OLTP and analytical environments, reflecting the typical architecture where transactional systems and reporting warehouses serve different workloads.

---

## Project Purpose

This project demonstrates practical warehouse development using SSIS, including:

- extracting data from an operational database;
- transforming data for analytical use;
- populating dimensions;
- loading transactional facts;
- implementing incremental ETL;
- maintaining separation between source and warehouse systems.

It is a compact example of building an analytics-ready data pipeline with SQL Server and SSIS.

---

# 💫 About Me:
🔭 I’m currently working on: Building scalable data pipelines and cloud-based data platforms using Python, PySpark, SQL, dbt, and GCP.<br>
👯 I’m looking to collaborate on: Data Engineering, ETL/ELT, Big Data, Cloud, and open-source data projects.<br>
🤝 I’m looking for help with: Advanced Data Engineering architectures, real-time streaming, and scalable cloud solutions.<br>
🌱 I’m currently learning: Advanced dbt, Databricks, Apache Spark, Kafka, Terraform, and modern DataOps practices.<br>
💬 Ask me about: Python, SQL, PySpark, dbt, BigQuery, GCP, ETL/ELT pipelines, Apache Airflow, and Data Engineering.<br>
⚡ Fun fact: I enjoy turning messy raw data into clean, reliable pipelines—and explaining how they work to others.

## 🌐 Socials:
[![Facebook](https://img.shields.io/badge/Facebook-%231877F2.svg?logo=Facebook&logoColor=white)](https://facebook.com/khaled.salah5148) [![Instagram](https://img.shields.io/badge/Instagram-%23E4405F.svg?logo=Instagram&logoColor=white)](https://instagram.com/khaled_salah5148) [![LinkedIn](https://img.shields.io/badge/LinkedIn-%230077B5.svg?logo=linkedin&logoColor=white)](https://linkedin.com/in/khaled-salah5148) [![email](https://img.shields.io/badge/Email-D14836?logo=gmail&logoColor=white)](mailto:khaled.salah2803@gmail.com)

# 💻 Tech Stack:
![C++](https://img.shields.io/badge/c++-%2300599C.svg?style=for-the-badge&logo=c%2B%2B&logoColor=white) ![Markdown](https://img.shields.io/badge/markdown-%23000000.svg?style=for-the-badge&logo=markdown&logoColor=white) ![PowerShell](https://img.shields.io/badge/PowerShell-%235391FE.svg?style=for-the-badge&logo=powershell&logoColor=white) ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![Google Cloud](https://img.shields.io/badge/GoogleCloud-%234285F4.svg?style=for-the-badge&logo=google-cloud&logoColor=white) ![Azure](https://img.shields.io/badge/azure-%230072C6.svg?style=for-the-badge&logo=microsoftazure&logoColor=white) ![Apache Kafka](https://img.shields.io/badge/Apache%20Kafka-000?style=for-the-badge&logo=apachekafka) ![Apache Spark](https://img.shields.io/badge/Apache%20Spark-FDEE21?style=for-the-badge&logo=apachespark&logoColor=black) ![Apache Hive](https://img.shields.io/badge/Apache%20Hive-FDEE21?style=for-the-badge&logo=apachehive&logoColor=black) ![Apache Hadoop](https://img.shields.io/badge/Apache%20Hadoop-66CCFF?style=for-the-badge&logo=apachehadoop&logoColor=black) ![Jinja](https://img.shields.io/badge/jinja-white.svg?style=for-the-badge&logo=jinja&logoColor=black) ![Snowflake](https://img.shields.io/badge/snowflake-%2329B5E8.svg?style=for-the-badge&logo=snowflake&logoColor=white) ![Apache Airflow](https://img.shields.io/badge/Apache%20Airflow-017CEE?style=for-the-badge&logo=Apache%20Airflow&logoColor=white) ![Jenkins](https://img.shields.io/badge/jenkins-%232C5263.svg?style=for-the-badge&logo=jenkins&logoColor=white) ![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white) ![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=white) ![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=for-the-badge&logo=mongodb&logoColor=white) ![MicrosoftSQLServer](https://img.shields.io/badge/Microsoft%20SQL%20Server-CC2927?style=for-the-badge&logo=microsoft%20sql%20server&logoColor=white) ![Canva](https://img.shields.io/badge/Canva-%2300C4CC.svg?style=for-the-badge&logo=Canva&logoColor=white) ![Figma](https://img.shields.io/badge/figma-%23F24E1E.svg?style=for-the-badge&logo=figma&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white) ![Git](https://img.shields.io/badge/git-%23F05033.svg?style=for-the-badge&logo=git&logoColor=white) ![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white) ![Playwright](https://img.shields.io/badge/-playwright-%232EAD33?style=for-the-badge&logo=playwright&logoColor=white) ![Selenium](https://img.shields.io/badge/-selenium-%43B02A?style=for-the-badge&logo=selenium&logoColor=white) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white) ![Kubernetes](https://img.shields.io/badge/kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white) ![Power Bi](https://img.shields.io/badge/power_bi-F2C811?style=for-the-badge&logo=powerbi&logoColor=black) ![Splunk](https://img.shields.io/badge/splunk-%23000000.svg?style=for-the-badge&logo=splunk&logoColor=white) ![Terraform](https://img.shields.io/badge/terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white)

# 📊 GitHub Stats:
![](https://github-readme-stats.shion.dev/api?username=khaledsalah5&theme=github_dark&hide_border=true&include_all_commits=true&count_private=false)<br/>
![](https://streak-stats.demolab.com/?user=khaledsalah5&theme=github_dark&hide_border=true)<br/>
![](https://github-readme-stats.shion.dev/api/top-langs/?username=khaledsalah5&theme=github_dark&hide_border=true&include_all_commits=true&count_private=false&layout=compact)

### ✍️ Random Dev Quote
![](https://quotes-github-readme.vercel.app/api?type=horizontal&theme=radical)

---
[![](https://komarev.com/ghpvc/?username=khaledsalah5&icon=0&color=0)](https://visitcount.itsvg.in)
