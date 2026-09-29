# Sales OLTP to Data Warehouse — SSIS

## Overview

This project implements an **SSIS ETL pipeline from a Sales OLTP database into a dimensional Sales Data Warehouse**.

The pipeline loads Customer, Product, and Salesman dimensions, applies Slowly Changing Dimension logic, resolves warehouse keys using lookups, and incrementally loads sales facts.

```text
Sales_OLTP
    │
    ▼
  SSIS ETL
    │
    ├── Customer Dimension
    ├── Product Dimension
    └── Salesman Dimension
    │
    ▼
  Sales_Dim
    │
    ▼
Incremental Sales Fact Load
```

---

## Why This Project Is Different

This repository focuses on a custom **Sales OLTP → Data Warehouse** design.

Unlike the AdventureWorks project, it emphasizes:

- Customer, Product, and Salesman dimensions;
- SCD processing across all three business dimensions;
- incremental sales fact loading;
- lookup-based resolution of warehouse surrogate keys.

---

## ETL Packages

### `CustomerDim.dtsx`
Loads customer records into the warehouse and contains SSIS Slowly Changing Dimension logic for customer changes.

### `ProductDim.dtsx`
Loads product data and uses SCD processing to manage changes to product attributes.

### `SalesmanDim.dtsx`
Loads salesman / salesperson data and applies SCD handling to changing salesperson attributes.

### `Sales_incremental_Load_fact.dtsx`
Incrementally loads sales facts and uses lookup transformations to resolve warehouse keys such as Product and Date keys before writing fact rows.

---

## Repository Structure

```text
SalesDWH/
│
├── Sales_DWH_ETL.sln
├── README.md
│
└── Sales_DWH_ETL/
    ├── CustomerDim.dtsx
    ├── ProductDim.dtsx
    ├── SalesmanDim.dtsx
    ├── Sales_incremental_Load_fact.dtsx
    ├── KHALED_SQLSERVERDEV.Sales_OLTP.conmgr
    ├── KHALED_SQLSERVERDEV.Sales_Dim.conmgr
    ├── Project.params
    └── Sales_DWH_ETL.dtproj
```

---

## Source and Destination Separation

The project contains dedicated SSIS connection managers for the operational and analytical databases:

```text
KHALED_SQLSERVERDEV.Sales_OLTP.conmgr
KHALED_SQLSERVERDEV.Sales_Dim.conmgr
```

This models a common warehouse architecture where the transactional source and reporting warehouse are separate systems.

---

## Slowly Changing Dimensions

The three dimension packages contain SSIS **Slowly Changing Dimension** components:

```text
CustomerDim
ProductDim
SalesmanDim
```

The SCD transformation uses lookup behavior to identify existing dimension records and determine how changes should be handled.

This demonstrates change management in dimensions rather than treating every ETL run as a complete reload.

---

## Fact Loading

The sales fact package is incremental rather than a full-reload package.

Its processing pattern is roughly:

```text
New Sales Records
       │
       ▼
Dimension Lookups
       │
       ├── Product warehouse key
       ├── Date warehouse key
       └── Other dimensional keys
       │
       ▼
Sales Fact Table
```

Resolving dimensional keys before loading the fact table keeps the warehouse relationships consistent and separates operational identifiers from analytical surrogate keys.

---

## Recommended Execution Order

```text
1. CustomerDim.dtsx
2. ProductDim.dtsx
3. SalesmanDim.dtsx
4. Sales_incremental_Load_fact.dtsx
```

Dimensions should be prepared before facts so the incremental fact process can resolve the required dimension records.

---

## Tech Stack

- SQL Server Integration Services (SSIS)
- Microsoft SQL Server
- T-SQL
- Visual Studio / SQL Server Data Tools
- Dimensional Modeling
- Slowly Changing Dimensions
- Lookup Transformations
- Incremental ETL

---

## How to Run

1. Open `Sales_DWH_ETL.sln` in Visual Studio with SSIS / SSDT installed.
2. Configure the Sales OLTP source connection.
3. Configure the Sales dimensional warehouse destination connection.
4. Run the three dimension packages.
5. Run `Sales_incremental_Load_fact.dtsx`.
6. Validate:
   - dimension row counts;
   - fact row counts;
   - newly inserted records;
   - dimension-key relationships;
   - SCD behavior for changed dimension records.

---

## Data Engineering Concepts Demonstrated

- OLTP-to-DWH integration;
- dimensional modeling;
- SCD processing;
- surrogate-key lookup patterns;
- fact/dimension dependency ordering;
- incremental ETL;
- separate source and destination connections;
- analytics-ready relational modeling.

---

## Related Project

This repository is different from **sales_data_DW**.

- **SalesDWH** → Sales OLTP → DWH with Customer, Product, Salesman, SCD processing, and incremental fact loading.
- **sales_data_DW** → AdventureWorks warehouse with Customer, Product, Territory, Date, and both full + incremental fact loading.

The two projects demonstrate similar SSIS fundamentals using different dimensional models and loading strategies.

---

---

## Author

**Khaled Salah — Data Engineer**  
[LinkedIn](https://www.linkedin.com/in/khaled-salah5148/) · [Portfolio](https://khaledsalah5.github.io/Portfolio/) · [GitHub](https://github.com/khaledsalah5) · [Email](mailto:khaled.salah2803@gmail.com)
