# 📊 Power BI Analytics Dashboard (`Pr1-Dashboard.pbix`)

An interactive, end-to-end Power BI report engineered to transform complex operational data into clear, actionable executive insights, cross-dimensional performance metrics, and granular operational drill-downs.

---

## 📑 Table of Contents

* [Overview](#-overview)
* [Video Walkthrough](#-video-walkthrough)
* [Dashboard Screenshots](#-dashboard-screenshots)
  * [Page 1: Executive KPI & Overview](#1-executive-kpi--performance-overview)
  * [Page 2: Detailed Trend & Breakdown Analysis](#2-detailed-trend--breakdown-analysis)
  * [Data Model Star Schema View](#3-data-model-star-schema-view)
  * [How to Add Your Screenshots](#-quick-guide-how-to-add-your-screenshots)
* [Dataset & Data Architecture](#-dataset--data-architecture)
  * [Star Schema Overview](#star-schema-overview)
  * [Data Dictionary & Tables](#data-dictionary--tables)
  * [Entity Relationship Details](#entity-relationship-details)
* [Dashboard Pages & Visual Breakdown](#-dashboard-pages--visual-breakdown)
  * [Page 1: Executive KPI & Overview](#page-1-executive-kpi--performance-overview)
  * [Page 2: Detailed Trend & Breakdown Analysis](#page-2-detailed-trend--breakdown-analysis)
* [Summary of Visualizations Used](#-summary-of-visualizations-used)
* [Theme & Visual System](#-theme--visual-system)
* [How to Set Up and Run](#-how-to-set-up-and-run)
* [Key Insights Delivered](#-key-insights-delivered)
* [Feedback & Contributing](#-feedback--contributing)

---

## 🌟 Overview

The **Pr1-Dashboard** project organizes raw operational records into high-impact visuals that guide strategic decision-making. Built using modern Power BI design standards, it incorporates:

* **Star Schema Data Modeling** for high-efficiency tabular performance.
* **Dynamic Time Intelligence** (YTD, Prior Year comparisons, MoM changes).
* **Microsoft Fluent 2 Visual Language** for cohesive spacing, clean typography, and high contrast.
* **Bi-directional cross-filtering and drill-down hierarchies** across dimensions.

---

## 🎥 Video Walkthrough

Watch a walkthrough demonstrating the data model, interactive slicers, cross-filtering, and dashboard insights:

[![Watch Video Walkthrough](https://drive.google.com/file/d/1CULv2lOwkPEyXK1ZZQWfD2Q4UB9RrDQs/view?usp=sharing)](https://youtube.com)

## 📸 Dashboard Screenshots

### 1. Executive KPI & Performance Overview
*High-level business health, core revenue KPIs, and periodic growth rates.*

<p align="center">
  <img width="950" alt="Executive KPI & Performance" src="https://github.com/user-attachments/assets/c23e15f8-b3f2-48a7-8d2b-789d449c024d" />
</p>

---

### 2. Detailed Trend & Breakdown Analysis
*Deep-dive analysis across product hierarchies, regional splits, and customer segments.*

<p align="center">
  <img width="950" alt="image" src="https://github.com/user-attachments/assets/ab12c232-fc15-447a-90f1-fb4313f73da6" />
</p>

---

### 3. Data Model (Star Schema View)
*Clean relationships connecting fact tables to date, customer, product, and territory dimensions.*

<p align="center">
  <img width="950" alt="image" src="https://github.com/user-attachments/assets/e6927411-e1b5-42e4-bf74-b412e2d6ddcf" />
</p>

## 🗄 Dataset & Data Architecture

### Star Schema Overview

The semantic model in `Pr1-Dashboard.pbix` is optimized using a **Star Schema** comprising central transactional facts surrounded by dimension lookup tables:

```text
                  ┌──────────────────────┐
                  │      DateTable       │
                  │   (Calendar Master)  │
                  └──────────┬───────────┘
                             │ 1
                             │
                             │ *
┌────────────────┐ *       ┌─┴──────────────┐       * ┌────────────────┐
│  DimCustomer   ├───1────>│   SalesFact    │<────1───┤   DimProduct   │
│ (Demographics) │         │ (Transactions) │         │  (Catalog/SKU) │
└────────────────┘         └─┬──────────────┘         └────────────────┘
                             │ *
                             │
                             │ 1
                  ┌──────────┴───────────┐
                  │     DimTerritory     │
                  │ (Regions/Geography)  │
                  └──────────────────────┘
```

---

### Data Dictionary & Tables

#### 1. Fact Table: `SalesFact` / `Transactions`
Stores measurable transactional events recorded across operations:

| Column Name | Data Type | Key Type | Description |
| :--- | :--- | :--- | :--- |
| `TransactionID` | Text / Integer | Primary Key | Unique transaction/invoice identifier |
| `Date` | Date | Foreign Key | Transaction timestamp linked to `DateTable` |
| `CustomerID` | Text / Integer | Foreign Key | References `DimCustomer` |
| `ProductID` | Text / Integer | Foreign Key | References `DimProduct` |
| `TerritoryID` | Text / Integer | Foreign Key | References `DimTerritory` |
| `Quantity` | Whole Number | Metric | Number of units purchased |
| `UnitPrice` | Decimal Number | Metric | Base unit price per product item |
| `DiscountRate` | Decimal Number | Metric | Applied discount percentage ($0.00 - 1.00$) |
| `CostPerUnit` | Decimal Number | Metric | Manufacturing / acquisition unit cost |

#### 2. Dimension: `DimProduct`
Detailed item information and classification:

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `ProductID` | Text / Integer | Unique SKU identifier |
| `ProductName` | Text | Commercial display name |
| `Category` | Text | Top-level product grouping |
| `SubCategory` | Text | Granular product sub-tier |
| `StandardCost` | Decimal Number | Default base inventory cost |
| `Status` | Text | Lifecycle state (`Active`, `Discontinued`) |

#### 3. Dimension: `DimCustomer`
Client profiles, segmentation, and classifications:

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `CustomerID` | Text / Integer | Unique customer or account ID |
| `CustomerName` | Text | Individual name or enterprise client label |
| `Segment` | Text | Business segment (`Enterprise`, `Consumer`, `SMB`) |
| `AccountType` | Text | Account loyalty status or tier |

#### 4. Dimension: `DimTerritory`
Hierarchical geographical breakdown:

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `TerritoryID` | Text / Integer | Unique regional region ID |
| `Country` | Text | Country name |
| `Region` | Text | Regional division (e.g., North, South, EMEA, APAC) |
| `State_City` | Text | State, province, or metropolitan hub |

#### 5. Dimension: `DateTable`
Continuous calendar table marked as official Date table for Time Intelligence:

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `Date` | Date | Single continuous calendar date (PK) |
| `Year` | Whole Number | Calendar year (e.g., `2024`, `2025`, `2026`) |
| `Quarter` | Text | Quarter format (`Q1`, `Q2`, `Q3`, `Q4`) |
| `MonthName` | Text | Full month label (`January`, `February`, etc.) |
| `MonthNumber` | Whole Number | Month order (`1` through `12` for sorting) |
| `YearMonth` | Text | Period key for chronological aggregation (`2026-03`) |

---

### Entity Relationship Details

* **Cardinality:** One-to-Many (`1:*`) relationships connecting dimension primary keys to fact foreign keys.
* **Cross-Filter Direction:** Single direction from Dimension $\rightarrow$ Fact table to protect filter lineage and optimize performance.
* **Referential Integrity:** Enforced referential integrity across date, territory, and product dimensions.

---

## 🖥 Dashboard Pages & Visual Breakdown

### Page 1: Executive KPI & Performance Overview
*Report Page ID: `4e9d921b7de00c360275`*

* **Objective:** Give executives an immediate pulse on revenue health, order volumes, profitability, and periodic growth rates.
* **Components & Layout:**
  * **Top KPI Ribbon:** Standout single-value cards for `Total Revenue`, `Total Orders`, `Profit Margin %`, and `YoY Growth %`.
  * **Revenue Trend Over Time:** Line / Area chart illustrating historical timeline trajectory with period comparisons.
  * **Regional Performance:** Clustered bar chart highlighting top-producing territories.
  * **Category Distribution:** Donut / Tree chart showing revenue share across product lines.
  * **Dynamic Global Slicers:** Date range selectors and region quick-filters.

### Page 2: Detailed Trend & Breakdown Analysis
*Report Page ID: `dabc47e748256c93b187`*

* **Objective:** Allow managers and analysts to drill down into product SKUs, customer tiers, and operational variances.
* **Components & Layout:**
  * **Product Matrix Grid:** Hierarchical table grouping `Category > SubCategory > Product` with conditional data bars.
  * **Customer Tier Analysis:** Clustered column chart tracking customer volume vs. average transaction value.
  * **Variance & Profitability Scatter / Decomposition:** Multi-dimensional visual mapping profit contribution against volume.
  * **Segment Slicers:** Multi-select filtering by customer segment, product status, and fulfillment channels.

---

## 📊 Summary of Visualizations Used

| Visual Element | Power BI Visual Type | Purpose / Business Metric |
| :--- | :--- | :--- |
| **Executive Metric Cards** | Card / New Card Visual | Instant visibility into Gross Revenue, AOV, Orders, and Margins |
| **Trend Line Chart** | Line & Clustered Area Chart | Continuous monthly/quarterly timeline trend analysis |
| **Category Breakdown** | Horizontal Bar Chart | Ranking revenue and volume across categories |
| **Composition Share** | Donut / Treemap | Proportional split by segment and product family |
| **Performance Matrix** | Matrix with Data Bars | Hierarchical product and regional drill-down with in-cell indicators |
| **Interactive Filters** | Between Date & Dropdown Slicers | Dynamic cross-page visual filtering and scenario exploration |

---

## 🎨 Theme & Visual System

* **Base UI Framework:** Built upon Microsoft's **Fluent 2 Theme** (`Fluent2-CY26SU10.json`).
* **Color Hierarchy:**
  * **Primary Brand Accent:** Royal Blue (`#0078D4`)
  * **Positive / Growth State:** Emerald Green (`#107C41`)
  * **Negative / Warning State:** Coral Red (`#D13438`)
  * **Neutral Data Palette:** Clean divergent slate tones (`Divergent.json`)
* **Typography:** Clean, accessible typography with legible hierarchy and uniform card borders.

---

## 🚀 How to Set Up and Run

1. **Clone or Download the Repository:**
   ```bash
   git clone https://github.com/your-username/powerbi-analytics-dashboard.git
   cd powerbi-analytics-dashboard
   ```

2. **Prerequisites:**
   * Install the latest desktop client: [Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/).

3. **Open the Report:**
   * Double-click `Pr1-Dashboard.pbix` to launch the file.

4. **Update / Refresh Data Sources:**
   * Open **Transform Data** (Power Query) if you need to redirect the file path to your local data storage.
   * Hit **Refresh** on the `Home` ribbon to refresh data and update visuals.

---

## 💡 Key Insights Delivered

* **High-Velocity Categories:** Readily identifies top 20% of catalog items generating 80% of revenue.
* **Geographic Dispersion:** Identifies underperforming regions requiring targeted campaigns.
* **Margin Protection:** Isolates product lines with excessive discounting hurting overall net profit.
* **Seasonality Tracking:** Visualizes peak ordering quarters to assist with inventory planning.

---

## 🤝 Feedback & Contributing

Contributions, questions, and feature requests are welcome!

* Feel free to open an **Issue** to report bugs or request new features.
* Submit a **Pull Request** if you have enhanced dashboard pages, new visuals, or updated themes.

⭐ **If this dashboard helped your analytics project, please give this repository a star!**
