# SugaRie Sweets Database Management System 🍪📊

A robust relational database management system developed. This system is designed to digitalize, streamline, and scale the operations of **SugaRie Sweets**, a specialized pastry shop founded in 2018, by migrating manual order handling into a structured database architecture. 
[SugaRie Sweets instagram account:] (https://www.instagram.com/sugariecookie/)

---

## 🌟 Core System Objectives
* **Order Automation:** Efficiently record and organize high volumes of customer purchase details.
* **Logistics Integration:** Facilitate seamless customer profile transmission to delivery application infrastructures.
* **Inventory Tracking:** Monitor remaining resource batch levels and live pastry stock counts to avoid shortages.
* **Data Security & Integrity:** Eliminate double entries, reduce structural data redundancy, and enhance operational data security.

---

## 🛠️ System Architecture & Schema

The application is built around a structured relational schema consisting of four core tables connected through definitive relational dependencies.

### Entity Relationship Diagram (ERD) Overview
* **Customer** `(Primary Key: cus_ID)` ─── *One-to-Many* ───> **Order** `(Primary Key: Order_ID)`
* **Product** `(Primary Key: Product_Id)` ─── *One-to-Many* ───> **Order**
* **Employee** `(Primary Key: EMP_ID)` ─── *One-to-Many* ───> **Order**

### Data Dictionary Specifications

| Table | Attribute | Data Type / Format | Constraints | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Customer** | `cus_ID` <br> `cus_Name` <br> `cus_Phone` <br> `cus_Address` | VARCHAR2(50) <br> VARCHAR2(50) <br> NUMBER(11) <br> VARCHAR2(50) | **PRIMARY KEY** <br> NOT NULL <br> UNIQUE <br> NOT NULL | Unique customer serial code <br> Client name <br> Contact number <br> Drop-off address |
| **Product** | `Product_Id` <br> `pro_Name` <br> `PriceOfProduct` <br> `ProductValue` <br> `QTY` | VARCHAR2(20) <br> VARCHAR2(50) <br> NUMBER <br> NUMBER <br> NUMBER | **PRIMARY KEY** <br> NOT NULL <br> NOT NULL <br> NOT NULL <br> NOT NULL | Stock Keeping Unit (SKU) <br> Pastry name <br> Unit retail price <br> Computed batch value <br> Remaining stock level |
| **Employee** | `EMP_ID` <br> `EMP_Name` <br> `EMP_Email` <br> `EMP_Salary` | VARCHAR2(20) <br> VARCHAR2(50) <br> VARCHAR2(50) <br> NUMBER | **PRIMARY KEY** <br> NOT NULL <br> UNIQUE <br> CHECK (salary > 0) | Internal staff ID <br> Staff full name <br> Company email <br> Monthly base pay |
| **Order** | `Order_ID` <br> `cus_ID` <br> `Product_Id` <br> `QTY` <br> `DateOfOrder` | VARCHAR2(20) <br> NUMBER <br> NUMBER <br> NUMBER <br> VARCHAR2(50) | **PRIMARY KEY** <br> **FOREIGN KEY** <br> **FOREIGN KEY** <br> NOT NULL <br> NOT NULL | Invoice transaction ID <br> References Customer table <br> References Product table <br> Purchased quantity <br> Transaction timestamp |

---

## 🖥️ Role-Based Interface Features

The application UI implements role-based access management to separate distinct business permissions:

### 1. Management View Dashboard
* Full control to **View, Add, Edit, and Delete** employee profiles and salaries.
* Full catalog access to **Add/Remove Products**, adjust unit prices, and manage active bakery inventory tiers.
* Contextual **Search bar filtering** optimized to locate employee records rapidly using ID and Name parameters.

### 2. Employee Operations Panel
* Active **Customer Register:** Allows frontline staff to quickly input client names, delivery directions, and contact tags.
* Live **Order Processing:** Interface to log active purchases, modify transaction counts, or remove orders from the queue.
* Internal **Reporting Engine:** Includes a distinct **Print View** function that instantly compiles transaction lists, calculates total checkout invoices, displays active shop profit metrics, and exports layout-ready summaries.

---

## 💾 SQL Implementation Samples

### Table Constraints Setup
```sql
CREATE TABLE Customer (
    cus_ID      VARCHAR2(50) CONSTRAINT Customer_cus_ID_pk PRIMARY KEY,
    cus_Name    VARCHAR2(50) CONSTRAINT CUSTOMER_cusName_nn NOT NULL,
    cus_Phone   NUMBER(12)   CONSTRAINT CUSTOMER_cus_Phone_uk UNIQUE,
    cus_Address VARCHAR2(50) CONSTRAINT CUSTOMER_cus_Address_nn NOT NULL
);

CREATE TABLE Employee (
    EMP_ID     VARCHAR2(20) CONSTRAINT Employee_EMP_ID_pk PRIMARY KEY,
    EMP_Name   VARCHAR2(50) CONSTRAINT Employee_EMP_Name_nn NOT NULL,
    EMP_Email  VARCHAR2(50) CONSTRAINT Employee_EMP_Email_uk UNIQUE,
    EMP_Salary NUMBER       CONSTRAINT Employee_EMP_Salary_check CHECK (EMP_Salary > 0)
);
