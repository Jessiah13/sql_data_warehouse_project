# Define Project Naming Conventions

Checkbox: Yes
DWH Epics: Project Initialization (https://www.notion.so/Project-Initialization-18daffe57688800b8218f7c61b90ce73?pvs=21)

This document outlines the naming conventions used for schemas, tables, views, columns, and other objects in the data warehouse.

---

## Table of Content

---

1. [General Principles](https://www.notion.so/Define-Project-Naming-Conventions-18daffe5768880cead86de32981fc29c?pvs=21) 
2. [Table Naming Conventions](https://www.notion.so/Define-Project-Naming-Conventions-18daffe5768880cead86de32981fc29c?pvs=21)
    1. [Bonze Rules](https://www.notion.so/Define-Project-Naming-Conventions-18daffe5768880cead86de32981fc29c?pvs=21)
    2. [Silver Rules](https://www.notion.so/Define-Project-Naming-Conventions-18daffe5768880cead86de32981fc29c?pvs=21)
    3. [Gold Rules](https://www.notion.so/Define-Project-Naming-Conventions-18daffe5768880cead86de32981fc29c?pvs=21)
3. [Column Naming Conventions](https://www.notion.so/Define-Project-Naming-Conventions-18daffe5768880cead86de32981fc29c?pvs=21)
    1. [Surrogate Keys](https://www.notion.so/Define-Project-Naming-Conventions-18daffe5768880cead86de32981fc29c?pvs=21)
    2. [Technical Columns](https://www.notion.so/Define-Project-Naming-Conventions-18daffe5768880cead86de32981fc29c?pvs=21)
4. [Stored Procedures](https://www.notion.so/Define-Project-Naming-Conventions-18daffe5768880cead86de32981fc29c?pvs=21)

---

### General Principles

---

- **Naming Conventions:** Use snake_case, with lowercase letter and underscores (_) to separate words.
- **Language:** Use English for all names.
- **Avoid Reserved Words:** Do not use SQL reserved works as object names.

### Table Naming Conventions

---

**Bronze Rules**

- All names must start with the source system name, and tables names must match their original names without renaming
    - `<**sourcesystem**>_<**entity**>`
        - `<**sourcesystem**>`: Name of the source system (e.g, crm, erp).
        - `<**entity**>`: Exact table name from the source system.
        - Example: **`crm_customer_info`** - Customer information from the CRM system.

**Silver Rules**

- All names must start with the source system name, and tables names must match their original names without renaming
    - `<**sourcesystem**>_<**entity**>`
        - `<**sourcesystem**>`: Name of the source system (e.g, crm, erp).
        - `<**entity**>`: Exact table name from the source system.
        - Example: **`crm_customer_info`** - Customer information from the CRM system.

**Gold Rules**

- All names must use meaningful, business-aligned names for tables, starting with the category prefix.
    - `<**category**>_<**entity**>`
        - `<**category**>`: Describes the role of the table, such as `dim` (dimension) or `fact` (fact table).
        - `<entity>`: Descriptive name of the table, aligned with the business domain (e.g., **`customers`**, **`products`**, **`sales`**).
        - Example:
            - **`dim_customers`** → Dimension table for customer data.
            - **`fact_sales`** → Fact table containing sales transactions.

### **Glossary of Category Patterns**

| Pattern | Meaning | **Example** |
| --- | --- | --- |
| **`dim_`** | Dimension table | **`dim_customer`**, **`dim_product`** |
| **`fact_`** | Fact table | **`fact_sales`** |
| **`report_`** | Report table | **`report_customers`** ,**`report_sales_monthly`**  |

### Column Naming Conventions

---

**Surrogate Keys**

- All primary keys in dimension tables must use the suffix `_key.`
- **`<table_name>_<key>`**
    - **`<table_name>`**: Refers to the name of the table or entity the key belongs to.
    - **`_<key>`:** A suffix indicating that this column is a surrogate key.
    - Example: **`<customer_key>`** - Surrogate key in the **`<dim_customers>`** table.

**Technical Columns**

- All technical columns must start with the prefix of `dwh_`, followed by a descriptive name indicating the column’s purpose.
- **`<dwh_<column_name>`**
    - **`dwh`:** Prefix exclusively for system-generated meta-data.
    - **`<column_name>`:** Descriptive name indicating the columns purpose.
    - Example: **`dwh_load_date` -** System-generated column used to store the date when the record was loaded.

### Stored Procedures

---

- All stored procedures used for loading data must follow the naming pattern:
- **`load_<layer>`:**
    - **`<layer>`:** Represents the layer being loaded, such as ,**`bronze`** ,**`silver`** or **`gold`**.
    - Example:
        - **`load_bronze`:**  - Stored procedure for loading data into the Bronze layer.
        - **`load_silver`:**  - Stored procedure for loading data into the Silver layer.