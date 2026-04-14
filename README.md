# 📊 Sales Analysis Dashboard — Power BI Portfolio Project

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)
![Data](https://img.shields.io/badge/Data-Retail%20Sales-blue?style=for-the-badge)
![DAX](https://img.shields.io/badge/DAX-Measures%20%26%20KPIs-orange?style=for-the-badge)

---

## 📌 Overview

This project presents an end-to-end **interactive sales analytics dashboard** built in Power BI, designed to transform raw transactional retail data into strategic business intelligence. The dashboard enables leadership teams to monitor revenue performance, identify high-value customer segments, and uncover seasonal and category-level trends across a four-year period (2014–2017). By consolidating key metrics into a single, filterable view, this solution reduces the time-to-insight for sales managers and empowers data-driven decisions at both operational and executive levels. The result is a scalable, reusable reporting framework that replaces manual spreadsheet analysis with a dynamic, always-current intelligence layer.

---

## 🧩 Business Problem

Retail organizations frequently struggle with fragmented sales reporting — data spread across multiple systems, slow manual aggregation, and a lack of clear visibility into what's driving (or dragging) revenue. Decision-makers are often left asking:

- *Which product categories and segments are generating the most profit — and which are underperforming?*
- *Are we shipping orders in the most cost-effective way, and is it affecting customer satisfaction?*
- *How does regional performance compare, and where should we prioritize resources?*
- *Is revenue growth sustainable, or driven by one-time spikes?*

**Stakeholders served by this dashboard include:**

| Stakeholder | How They Use It |
|---|---|
| C-Suite / Executive Leadership | High-level KPI monitoring, YoY strategy |
| Sales & Revenue Teams | Category and segment performance tracking |
| Operations & Logistics | Ship mode analysis, order fulfillment optimization |
| Finance | Profitability by category, discount impact analysis |

This dashboard directly informs decisions around inventory allocation, discount strategies, sales channel investments, and regional market prioritization.

---

## 🎯 Objectives

- **Track aggregate performance** across key KPIs: total sales, profit, quantity, and discounts
- **Segment revenue by category** (Technology, Furniture, Office Supplies) to identify the most and least profitable lines
- **Analyze customer segments** (Consumer, Corporate, Home Office) to support targeted sales strategies
- **Reveal seasonal and quarterly patterns** in sales volume to inform campaign planning and inventory management
- **Evaluate shipping mode efficiency** and its relationship to order volume and profitability
- **Surface the top-performing products** by revenue to guide upselling and stock prioritization
- **Enable year-over-year comparison** (2014–2017) through dynamic slicers for trend analysis
- **Support regional performance reviews** across Central, East, South, and West territories

---

## 📂 Dataset

| Attribute | Details |
|---|---|
| **Source** | Superstore-style retail transactional dataset (commonly derived from the Tableau/Kaggle Superstore dataset) |
| **Time Range** | 2014 – 2017 (4 full years) |
| **Total Sales Volume** | ~$2.3M aggregate across all years |
| **Records** | ~9,994 orders |
| **Geography** | North America (4 regional divisions: Central, East, South, West) |

**Key Variables Used:**

- `Order Date` — used for monthly, quarterly, and yearly time-series analysis
- `Sales` — primary revenue metric
- `Profit` — profitability measure per transaction
- `Quantity` — units sold per order
- `Discount` — discount value applied to orders
- `Category` — Technology, Furniture, Office Supplies
- `Sub-Category` — granular product grouping
- `Segment` — Consumer, Corporate, Home Office
- `Ship Mode` — Standard Class, Second Class, First Class, Same Day
- `Region` — Central, East, South, West
- `Product Name` — for top-product analysis

**Assumptions & Limitations:**

- The dataset reflects historical retail data and may not account for returns or cancellations
- Geographic data points to North America only; international markets are not represented
- Profit figures are assumed to be net after cost of goods sold, but before tax
- Discount values are aggregated totals, not percentage-based breakdowns

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Power BI Desktop** | Primary dashboard development environment |
| **DAX (Data Analysis Expressions)** | Calculated measures, KPI logic, time intelligence |
| **Power Query (M Language)** | Data ingestion, transformation, and cleaning |
| **Bing Maps (integrated)** | Geographic sales distribution visualization |
| **Excel / CSV** | Source data format prior to Power BI ingestion |

---

## 🔧 Approach & Methodology

### 1. Data Preparation (Power Query)
- Loaded raw transactional CSV data into Power BI via Power Query Editor
- Cleaned and standardized column names and data types (dates, currency, integers)
- Removed duplicate order entries and handled null values in discount and profit fields
- Created a dedicated **Date Table** to support time intelligence functions (YoY, QoQ comparisons)
- Established relationships between the fact table (orders) and dimension tables (products, customers, regions)

### 2. Data Modeling
- Implemented a **star schema** with the Orders fact table at the center, connected to:
  - `DimDate` — for time-based filtering and slicing
  - `DimProduct` — for category and sub-category hierarchies
  - `DimCustomer` — for segment-level analysis
  - `DimRegion` — for geographic breakdowns
- Set up **bi-directional filtering** where needed for cross-visual interactivity

### 3. DAX Measures & Calculated Columns

Key measures developed:

```dax
-- Total Sales
Total Sales = SUM(Orders[Sales])

-- Total Profit
Total Profit = SUM(Orders[Profit])

-- Profit Margin %
Profit Margin = DIVIDE([Total Profit], [Total Sales], 0)

-- Total Quantity
Total Quantity = SUM(Orders[Quantity])

-- Total Discounts
Total Discounts = SUM(Orders[Discount])

-- YoY Sales Growth
YoY Sales Growth =
  VAR CurrentYear = [Total Sales]
  VAR PriorYear = CALCULATE([Total Sales], SAMEPERIODLASTYEAR(DimDate[Date]))
  RETURN DIVIDE(CurrentYear - PriorYear, PriorYear, 0)
```

### 4. Dashboard Design Decisions
- **Year slicer buttons (2014–2017)** placed prominently at the top for quick period switching
- **KPI cards** for Sales, Profit, Quantity, and Discounts provide immediate executive summary
- **Treemap** used for category-level sales — intuitive for proportional comparison at a glance
- **Donut charts** for segment and ship mode breakdown — clean and mobile-readable
- **Combo chart** (bar + line) for Monthly Sales & Quantity to surface volume-vs-revenue relationships
- **Scatter plot** (Sales vs Profit) for identifying outlier products and profitability gaps
- **Dark regional selector** for geographic drill-down without overwhelming the layout
- Consistent **purple-teal color palette** for professional, accessible visual hierarchy

---

## 💡 Key Insights & Findings

### 1. 🏆 Technology Leads in Revenue, But Not Always in Profit
Technology is the top-grossing category at **$836K** (all years), but its profit margin is not always the highest. In 2016, Office Supplies delivered the largest profit share at **57.13%** despite lower total sales — suggesting Technology may carry higher cost of goods or heavier discounting.

### 2. 📈 Revenue Peaks Sharply in Q4
Across all years, Q4 consistently accounts for the largest sales share — **38.22% of annual revenue** in aggregate. November and December show pronounced spikes in the monthly trend charts, pointing to seasonal demand (likely holiday/year-end procurement cycles). This has direct implications for inventory build-up and staffing.

### 3. 👥 Consumer Segment Dominates, Corporate Offers Higher Per-Order Value
The Consumer segment drives the majority of volume at **50.56% of sales**, but the Corporate segment — at 30.74% — likely drives higher-margin, bulk orders. The Home Office segment (18.7%) remains underserved and represents a growth opportunity, particularly in the post-2016 era.

### 4. 🚚 Standard Class Shipping Carries Disproportionate Revenue Share
Over **59% of total sales** are fulfilled via Standard Class shipping. While this is cost-efficient, the near-absence of Same Day shipping in the mix suggests an opportunity to upsell premium fulfillment options to high-value customers — potentially improving satisfaction and loyalty.

### 5. 📉 Furniture Category Has the Lowest Profit Contribution
Furniture consistently holds the lowest profit share across all years (as low as **6.44% in aggregate**). Despite generating $742K in sales, its poor margin profile suggests pricing pressure, high return rates, or excessive discounting — warranting a strategic pricing review.

### 6. 📆 Mid-Year Sales Slumps Are Consistent
February and April show recurring dips in monthly sales across multiple years. This mid-year slump represents a predictable gap that could be addressed with targeted promotions or outbound sales campaigns in Q1 and Q2 to flatten the seasonal curve.

### 7. 🖨️ A Small Set of Products Drives Disproportionate Revenue
The top 10 products account for **$244K+** in revenue (all years combined). Products like the Fellowes PB500 Electric Punch ($27,453) and HON 5400 Series Task Chairs ($21,870) are clear anchor SKUs. Ensuring their consistent availability and promotion could meaningfully protect topline revenue.

### 8. 📊 2017 Shows the Strongest Single-Year Performance
The 2017 filtered view shows **$250.1K in sales with $43.8K profit** — the strongest profit delivery of any single year in the dataset, with Q3 and Q4 contributing over 61% of that year's revenue. This trajectory suggests accelerating momentum heading into future periods.

---

## ✅ Business Recommendations

### 1. 🎯 Double Down on Q4 — Plan 90 Days Ahead
Given that Q4 consistently delivers 35–40% of annual revenue, the business should initiate supply chain, marketing, and sales outreach activities by early Q3. **KPI to track:** Q4 revenue as % of annual target; stock-out rate during November–December.

### 2. 📦 Investigate and Restructure Furniture Pricing
Furniture's persistently low profit margin (often below 7%) is a red flag. A profitability audit — examining product cost, discount frequency, and return rates — should be prioritized. **Recommendation:** Apply minimum margin thresholds per SKU and limit promotional discounting on low-margin items. **KPI to track:** Furniture profit margin %; discount rate by category.

### 3. 🤝 Build a Corporate Segment Growth Strategy
The Corporate segment's combination of high order values and consistent purchasing behavior makes it ideal for a dedicated account management program. Targeted B2B outreach, volume discount tiers, and custom procurement portals can accelerate this segment's share. **KPI to track:** Corporate segment revenue growth rate YoY; average order value by segment.

### 4. 🚀 Introduce Premium Shipping Incentives for High-Value Orders
With Standard Class accounting for ~59% of fulfillment and premium options underutilized, there is a clear upsell opportunity. Offer First Class or expedited shipping as a free threshold reward on orders above a set value. **KPI to track:** First Class shipping adoption rate; customer satisfaction score (CSAT) by ship mode.

### 5. 📣 Launch Mid-Year Sales Campaigns to Smooth Revenue Curve
The consistent February–April slump is predictable and therefore actionable. A structured mid-year promotion (Q1 product bundles, Q2 loyalty discounts) targeted at Consumer and Home Office segments can reduce revenue seasonality. **KPI to track:** Q1 and Q2 revenue as % of annual sales (target: increase from ~35% to 40%+ of annual).

---

## 📸 Dashboard Preview

> 📊 *Screenshot of the full dashboard here — replace with exported `.png` from Power BI Desktop*

![Sales Analysis Dashboard Preview](assets/dashboard_preview.png)

> **Tip:** To export a screenshot from Power BI Desktop, go to `File → Export → Export to PDF` or use `Windows + Shift + S` to capture the canvas directly.

---

## 🚀 How to Use / Setup

### Requirements
- **Power BI Desktop** — Version 2.115 or later (January 2024+) recommended
- **Operating System:** Windows 10 / 11 (Power BI Desktop is Windows-only)
- **No external database connection required** — data is embedded in the `.pbix` file

### Steps to Open & Explore

```bash
# 1. Clone this repository
git clone https://github.com/Leonard434/sales-analysis-dashboard.git

# 2. Navigate to the project directory
cd sales-analysis-dashboard
```

3. Open `Sales_Analysis.pbix` in **Power BI Desktop**
4. Use the **year buttons (2014 / 2015 / 2016 / 2017)** at the top to filter by year
5. Click on **region tiles** (Central, East, South, West) to filter all visuals by geography
6. Click any **chart element** (bar, slice, category) to cross-filter the entire dashboard
7. Hover over data points for detailed tooltips

### Data Refresh (If Connecting to Live Source)
- Go to `Home → Transform Data → Data Source Settings`
- Update the file path to your local CSV/Excel data source
- Click `Home → Refresh` to reload with updated data

---

## 📁 Project Structure

```
sales-analysis-dashboard/
│
├── Sales_Analysis.pbix          # Main Power BI dashboard file
├── README.md                    # Project documentation (this file)
│
├── data/
│   └── sales_data.csv           # Source dataset (raw transactional data)
│
├── assets/
│   └── dashboard_preview.png    # Dashboard screenshot for README
│
└── docs/
    └── Overview.pdf             # Project overview and summary export
```

---

## 👤 Author & Contact

**Leonard Thuranira**
*Data Scientist | Power BI Developer | ML Practitioner*

| Platform | Link |
|---|---|
| 🌐 Portfolio | [leonard434.github.io](https://leonard434.github.io) |
| 💼 LinkedIn | [linkedin.com/in/leonard-thuranira-67785024a](https://www.linkedin.com/in/leonard-thuranira-67785024a/) |
| 🐙 GitHub | [github.com/Leonard434](https://github.com/Leonard434) |

---

> *Built as part of a data science and analytics portfolio. Open to collaboration, freelance engagements, and feedback.*
