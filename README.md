# 📊 Global Sales Analysis — Power BI Project

An end-to-end Business Intelligence project built in **Power BI**, transforming a raw transactional sales dataset into a clean **Star Schema** data model and delivering interactive dashboards that answer real business questions across **Sales, Profit, Geography, Time, and Shipping**.

---

## 🎯 Project Overview

This project simulates a real-world BI workflow: from raw data ingestion, modeling, and DAX measure development, to building multi-page interactive reports with actionable insights and recommendations for stakeholders.

The report answers **12 key business questions** covering product performance, profitability, regional sales, time-based trends, and shipping cost optimization — including forecasting for future shipping costs.

---

## 🛠️ Tools & Technologies

- **Power BI Desktop** — Data modeling, visualization, and reporting
- **Power Query (M)** — Data cleaning and transformation
- **DAX** — Custom measures and calculated columns
- **Star Schema Modeling** — Optimized analytical data model
- **ETS Forecasting** — Built-in Power BI time-series prediction

---

## 🧱 Data Model — Star Schema

The transactional dataset was transformed into a **Star Schema** for fast, scalable analytical queries.

### Fact Table
- **Fact_Sales** — Central table containing Order ID, Order Date, Delivery Date, Discount, Discount Cost, Material & Utility Cost, Net Profit, Order Size, Order Month, and foreign keys linking to all dimensions.

### Dimension Tables
| Table | Description |
|-------|-------------|
| **Dim_Customer** | Customer ID, Name, Segment (Consumer / Corporate / Home Office) |
| **Dim_Product** | Product ID, Name, Category, Sub-Category |
| **Dim_Geography** | City, State, Country, Market, Region |
| **Dim_Date** | Date, Month, Quarter, Year, Week, Reporting Period |
| **Dim_Ship_Mode** | Shipping methods (Standard, First Class, Same Day, etc.) |
| **Dim_Order_Priority** | Order priority levels (Low, Medium, High, Critical) |

Each dimension uses a **surrogate key (SK_)** for efficient joins with the fact table.

---

## 📑 Report Pages

The Power BI report is organized into multiple pages for focused analysis:

1. **Overview** — KPIs for Net Profit, Cost, Sales
2. **Products** — Top/Least performing products by sales and profit
3. **Time Analysis** — Trends across years, quarters, and months
4. **Geography** — Sales and profit by Market, Region, and Country
5. **Shipping** — Cost analysis by shipping mode, region, and priority

---

## 🔍 Key Insights & Findings

| # | Business Question | Insight |
|---|-------------------|---------|
| 1 | Highest profit product? | **Apple Smart Phone, Full Size** (`TEC-PH-3184`) |
| 2 | Lowest sales product? | **Eureka Disposable Bags** (`OFF-AP-4215`) |
| 3 | Avg delivery days by priority | Critical: 1.8d • High: 3.1d • Medium: 4.5d • Low: 6.5d |
| 4 | Top sub-category (Sales & Profit) | **Phones** — $1.70M Sales, $853K Profit |
| 5 | Total Company Net Profit | **$2.29M** |
| 6 | Total Company Cost | **$10.33M** |
| 7 | Best sales month (2015) | **November** ($554,150) |
| 8 | Most profitable market | **Asia Pacific** ($4.0M) |
| 9 | Least sales country | **The Gambia** |
| 10 | Sales trend (2012–2015) | Consistent growth: $2.25M → $4.29M |
| 11 | Shipping cost reduction | Ship-mode, regional, product, and priority-based optimization |
| 12 | Shipping cost forecast | ETS forecast model predicts **$60,436** for Oct 2016 |

---

## 💡 Sample DAX Measures

```DAX
Top Profit Product ID =
VAR TopProduct =
    TOPN(1,
        SUMMARIZE('Fact_Sales', 'Dim_Product'[Product ID], "Total_Profit", SUM(Fact_Sales[Net Profit])),
        [Total_Profit],
        DESC
    )
RETURN
    CONCATENATEX(TopProduct, Dim_Product[Product ID], ", ")
```

```DAX
Top Sales Month 2015 =
VAR BestMonth =
    TOPN(1,
        SUMMARIZE(
            FILTER('Fact_Sales', Fact_Sales[order year] = 2015),
            'Fact_Sales'[order month],
            "Total_Sales", [Sales]
        ),
        [Total_Sales],
        DESC
    )
RETURN
    CONCATENATEX(BestMonth, Fact_Sales[order month], ", ")
```

Additional measures include: `Lowest Sales Product ID`, `Top Profit Market`, `Lowest Sales Country`, and more.

---

## 📈 Business Recommendations

Based on the analysis, the following actions were recommended to stakeholders:

- **Optimize Ship Mode:** Limit Same Day & First Class shipping to truly urgent orders — Standard Class is **54% cheaper** and handles most volume efficiently.
- **Regional Distribution:** Establish regional hubs in high-cost areas like **Eastern Asia** (avg $40 shipping) to reduce costs.
- **Order Bundling:** Bundle Office Supplies ($13 avg) with Technology ($50) and Furniture ($44) shipments to reduce marginal shipping cost.
- **Priority Review:** Tighten criteria for "Critical" priority — these orders cost **227% more** than Medium priority shipping.

---

## 📁 Repository Contents

```
📦 PowerBI-Sales-Analysis
 ┣ 📄 Sales_Analysis.pbix                          # Power BI report file
 ┣ 📄 Star_Schema_Transformation_Documentation.pdf # Data model documentation
 ┣ 📄 Sales_Analysis_Use_case_Insights_and_Answers.pdf # Business Q&A + DAX
 ┗ 📄 README.md
```

---

## 🚀 How to Use

1. Clone or download this repository.
2. Open `Sales_Analysis.pbix` in **Power BI Desktop** (latest version recommended).
3. Navigate through the report pages to explore visuals and insights.
4. Refer to the included PDFs for full documentation of the data model and business answers.

---

## 📬 Contact

If you have questions, feedback, or want to connect:

- **GitHub:** [github](https://github.com/kariman29)
- **LinkedIn:** [linkedin-profile](https://www.linkedin.com/in/karimanibrahem45/)

---

⭐ *If you found this project helpful or inspiring, please consider giving it a star!*
