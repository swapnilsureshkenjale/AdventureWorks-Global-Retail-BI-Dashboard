# 🚴 AdventureWorks Global Retail Business Intelligence Dashboard

## 📌 Project Overview
This project delivers a comprehensive Business Intelligence solution designed to track, analyze, and optimize the global sales operations of **AdventureWorks**, a multinational manufacturing company specializing in cycling equipment, accessories, and apparel. Utilizing multi-year transaction data (2015–2017), this solution transforms complex transactional ecosystems into an interactive asset to support supply chain management, regional market expansions, and product lifecycle strategies.

---

<img width="1385" height="781" alt="image" src="https://github.com/user-attachments/assets/14ff4c11-143b-4059-91b0-b2090493f0e1" />

---

## 🛠️ Tools & Technologies
* **BI Platform:** Microsoft Power BI / Excel
* **Data Modeling:** Extended Star Schema (Snowflake elements for Product Hierarchies)
* **Calculations & Metrics:** Advanced DAX (Time Intelligence, Profit Margins, Return Rates)
* **Data Transformation:** Power Query ETL (Data type normalization, multi-table consolidation)
* **Documentation:** Markdown

## 🏗️ Data Architecture & Relationship Model

The structural backbone of this AdventureWorks BI solution relies on an optimized relational database design that blends elements of **Star Schema** and **Snowflake Schema** methodologies. Fact tables hold numeric transaction variables, while dimension tables radiate outwards to supply descriptive context, ensuring clear filter propagation and minimized data redundancy.

### 👥 Data Relationships & Structural Cardinality

The relationship flow moves seamlessly from lookups (Dimension Tables) down into operational facts (Fact Tables) through strict **Many-to-One (*:1)** configurations:

| Upstream / Dimension Table | Downstream / Fact or Sub-Dim Table | Cardinality | Join Key / Common Attribute | Filter Direction |
| :--- | :--- | :--- | :--- | :--- |
| **AdventureWorks_Calendar** | **AdventureWorks_Sales** | `1:*` | `Date` ➡️ `OrderDate` | Single (Calendar filters Sales) |
| **AdventureWorks_Customers** | **AdventureWorks_Sales** | `1:*` | `CustomerKey` | Single (Customers filters Sales) |
| **AdventureWorks_Territories** | **AdventureWorks_Sales** | `1:*` | `SalesTerritoryKey` ➡️ `TerritoryKey` | Single (Territories filters Sales) |
| **AdventureWorks_Products** | **AdventureWorks_Sales** | `1:*` | `ProductKey` | Single (Products filters Sales) |
| **AdventureWorks_Territories** | **AdventureWorks_Returns** | `1:*` | `SalesTerritoryKey` ➡️ `TerritoryKey` | Single (Territories filters Returns) |
| **AdventureWorks_Products** | **AdventureWorks_Returns** | `1:*` | `ProductKey` | Single (Products filters Returns) |
| **Product_Categories** | **Product_Subcategories** | `1:*` | `ProductCategoryKey` | Single (Categories filters Subcategories) |
| **Product_Subcategories** | **AdventureWorks_Products** | `1:*` | `ProductSubcategoryKey` | Single (Subcategories filters Products) |

### ⚡ Architectural Optimization Highlights

* **Snowflaked Product Hierarchy:** Product definitions are normalized through a cascading schema sequence (`Product_Categories` ➡️ `Product_Subcategories` ➡️ `AdventureWorks_Products`). This structure guarantees normalized data integrity while minimizing the storage footprint of data lookups.
* **Bi-Trifurcated Sales Fact Architecture:** The transactional ledger consists of independent year-by-year splits (2015, 2016, 2017) seamlessly handled by Power BI's structural model layer, connecting uniform join keys back to primary dimension blocks.
* **Dual-Fact Integration:** The architecture bridges two distinct metrics systems—**Sales** (for commercial health) and **Returns** (for quality and risk monitoring)—without introducing complex cross-filtering ambiguity.
* **Strict Unidirectional Filter Flow:** All filtering paths move exclusively in a one-way path down from context dimensions into transactional values. This ensures predictable DAX engine computation profiles and explicitly eliminates circular or ambiguous querying paths.

---

## 📈 High-Impact Business Metrics (Derived)

Through full integration of the relational schema, the business performance across the active lifecycle yields the following key baselines:

### 💰 Core Financial Performance
* **Total Sales Revenue:** `$24,914,586.82`
* **Total Production Cost:** `$14,456,871.39`
* **Net Profit generated:** `$10,457,715.43` (~41.9% Gross Margin)
* **Total Product Quantity Distributed:** `84,174 units` across `25,164 unique consumer orders`

### 📦 Product Category Dominance
* **Bikes:** The primary revenue engine of AdventureWorks, generating a staggering **$23.64M**.
* **Accessories:** High transaction velocity volume generating **$906.6K**.
* **Clothing:** An emerging segment contributing **$365.4K**.

### 🌍 Regional Market Performance
* **North America:** The **United States** leads as the single largest market with **$7.93M** in revenue, followed closely by **Canada ($1.76M)**.
* **Asia-Pacific:** **Australia** represents a major high-performing region, contributing **$7.41M** in total revenue.
* **Europe:** Driven collectively by the **United Kingdom ($2.90M)**, **Germany ($2.52M)**, and **France ($2.36M)**.

---

## 🔍 Core Visual & Analytical Features

### 1. Executive Sales Performance Page
* **Time-Intelligence Trajectories:** Analyzes sales momentum from January 1, 2015, through December 6, 2017, tracking year-over-year (YoY) revenue and margin trends.
* **Geographical Mapping:** Tracks performance across regions, allowing executives to filter operations by Continents (North America, Europe, Pacific).

### 2. Product Quality & Reverse Logistics Page
* **Defect & Return Tracking:** Monitors the global **Return Rate of 2.17%** (1,828 total units returned).
* **Risk Management:** Isolates specific high-return product subcategories or territories to flag supply chain issues or design flaws.

### 3. Customer Demographics Deep-Dive
* **Income & Profession Alignment:** Segments order quantity and product affinity by occupational classes (Professional, Management, Skilled Manual) and annual income brackets to optimize targeting for premium bicycle categories.

---
