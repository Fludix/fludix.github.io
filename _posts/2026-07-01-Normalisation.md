---
layout: post
title: "Relational Database Normalisation: From 1NF to 5NF"
date: 01-07-2026
categories:
  - IT
tags:
  - sql
  - standard
  - database
  - normalisation
---

The main goal of database normalisation is to reduce data redundancy and prevent **data anomalies** (inconsistencies) during modifications. 

Before we dive into the normal forms, let's look at the three problems we want to avoid:
* **Insertion Anomaly:** You cannot add new data because some required key information is missing.
* **Update Anomaly:** Changing a value in one place doesn't update it everywhere, leading to contradictory data.
* **Deletion Anomaly:** Deleting a record accidentally destroys other, unrelated information that you still need.

## <b>1st Normal Form (1NF): Atomicity</b>
**Rule:** Each column must contain atomic (indivisible) values. No multiple values or hidden structures within a single cell.

### 🚫 Bad Example (Violates 1NF)
| CustomerID | Name | Address |
| :--- | :--- | :--- |
| 1 | Alice Smith | Main St 12, 12345 Berlin |

###  Good Example (1NF)
```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(100),
    Street VARCHAR(100),
    ZipCode VARCHAR(10),
    City VARCHAR(100)
);
```
## <b>2nd Normal Form (2NF): Full Dependency</b>
**Rule:** The table must be in 1NF, and all non-key columns must depend on the **entire** primary key (no partial dependencies on a composite key).

### 🚫 Bad Example (Violates 2NF)
_Key: `(CustomerID, ProductID)`_
- `CustomerName` only depends on `CustomerID`, not on the product. This causes **Update Anomalies**.

### Good Example (2NF)
Split the data into two tables:
```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100)
);

CREATE TABLE OrderItems (
    CustomerID INT,
    ProductID INT,
    Quantity INT,
    PRIMARY KEY (CustomerID, ProductID)
);
```

## <b>3rd Normal Form (3NF): No Transitive Dependencies</b>
**Rule:** The table must be in 2NF, and no non-key column should depend on another non-key column.

### 🚫 Bad Example (Violates 3NF)
- `City` depends on `ZipCode`, which depends on `CustomerID`. If you delete the last customer in Berlin, you lose the information that `12345` belongs to Berlin (**Deletion Anomaly**).

### Good Example (3NF)
Move the ZIP code mapping to its own table:
```sql
CREATE TABLE Cities (
    ZipCode VARCHAR(10) PRIMARY KEY,
    City VARCHAR(100)
);

CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Street VARCHAR(100),
    ZipCode VARCHAR(10)
);
```

## <b>Boyce-Codd Normal Form (BCNF)</b>
**Rule:** A stricter version of 3NF. For every non-trivial functional dependency X -> Y, X must be a superkey (candidate key).
- **Effect:** It eliminates rare anomalies that 3NF allows when a table has multiple overlapping candidate keys.

## <b>Advanced Normal Forms (4NF & 5NF)</b>

### 4th Normal Form (4NF)
**Rule:** No multi-valued dependencies.
- **Example:** If a supplier delivers multiple independent parts and also serves multiple independent countries, do not mix them in one table. Store `(Supplier, Part)` and `(Supplier, Country)` separately.

### 5th Normal Form (5NF / Project-Join)
**Rule:** Reconstructing the original table from smaller tables via `JOIN` must not create "phantom" or incorrect records.
- **When to use:** Only relevant for very complex relationships where data cannot be split further without losing semantic meaning.

## <b>Summary: How far should you go?</b>
In the real world, **3NF or BCNF** is usually the sweet spot for production databases. Going up to 5NF often over-complicates queries and reduces performance due to too many `JOIN` operations.