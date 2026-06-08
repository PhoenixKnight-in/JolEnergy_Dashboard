# 🔋 JOL Energy Pvt. Ltd. — Business Intelligence Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Excel](https://img.shields.io/badge/Microsoft%20Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![Kaggle](https://img.shields.io/badge/Kaggle-20BEFF?style=for-the-badge&logo=kaggle&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-1A6B3A?style=for-the-badge)

> **SDE & Data Analytics Track | Internship Assessment**
> A fully operational Business Intelligence Dashboard simulating JOL Energy's end-to-end commercial operations in battery recycling.

---

## 📌 Project Overview

JOL Energy Pvt. Ltd. is a battery recycling company. This project builds a **4-page Business Intelligence Dashboard** in Power BI tracking the company's core commercial verticals:

| Dashboard Section | Description |
|---|---|
| 🏭 Supplier Pipeline | Track supplier leads, ESG risk scores, and funnel conversion |
| 🛒 Buyer Pipeline | Monitor buyer stages, product interest, and offtake potential |
| 🗺️ Collection Network | Map collection points geographically with volume analysis |
| 📈 Market Intelligence | Track commodity prices for Li, Ni, Co, and Battery Scrap |
---

## 📁 Repository Structure

```
jol-energy-dashboard/
│
├── 📂 raw-data/                  # Original Kaggle CSVs (untouched)
│   ├── ev_sales_raw.csv
│   ├── ev_infrastructure_raw.csv
│   └── supply_chain_esg_raw.csv
│
├── 📂 clean-data/                # Cleaned & standardized Excel files
│   ├── ev_sales_clean.xlsx
│   ├── ev_trends_monthly_clean.xlsx
│   ├── ev_market_master_clean.xlsx
│   ├── ev_charging_monthly_clean.xlsx
│   ├── charging_station_clean.xlsx
│   ├── Supply_chain_clean.xlsx
│   └── fuel_prices_monthly_clean.xlsx
│
├── 📂 mock-data/                 # Self-generated pipeline simulation data
│   └── pipeline_mock.xlsx
│       ├── SupplierPipeline      # 30 supplier leads across 5 stages
│       ├── BuyerPipeline         # 30 buyer leads across 5 stages
│       ├── CollectionPoints      # 25 collection points (India-heavy)
│       └── CommodityPrices       # 24 months Li/Ni/Co/Scrap prices
│
├── 📂 powerbi/                   # Power BI files
│   ├── JolEnergy_Dashboard.pbix  # Main Power BI file
│   └── JolEnergy_Dashboard.pdf   # Exported PDF of all pages
│
├── 📂 screenshots/               # Annotated dashboard screenshots
│   ├── 01_supplier_pipeline.png
│   ├── 02_buyer_pipeline.png
│   ├── 03_collection_network.png
│   └── 04_market_intelligence.png
│
├── 📂 report/                    # Insights report
│   └── JolEnergy_Insights_Report.docx
│
├── 📂 documentation/             # Technical notes
│   └── technical_notes.md
│
└── README.md
```

---

## 📊 Dashboard Pages

### Page 1 — Supplier Pipeline
![Supplier Pipeline](screenshots/01_supplier_pipeline.png)

| KPI | Value |
|---|---|
| Total Supplier Leads | 30 |
| LOI Received | 3 |
| Conversion Rate | 10% |
| Avg ESG Risk Score | 31.73 |

### Page 2 — Buyer Pipeline
![Buyer Pipeline](screenshots/02_buyer_pipeline.png)

| KPI | Value |
|---|---|
| Total Buyer Leads | 30 |
| LOI Received | 2 |
| Sample Requested | 5 |
| Conversion Rate | 7% |

### Page 3 — Collection Network
![Collection Network](screenshots/03_collection_network.png)

| KPI | Value |
|---|---|
| Total Collection Points | 25 |
| Active Points | 17 |
| Total Monthly Volume | 60,000 KG |
| Countries Covered | 5 |

### Page 4 — Market Intelligence
![Market Intelligence](screenshots/04_market_intelligence.png)

| Commodity | Jan 2023 | Dec 2024 | Change |
|---|---|---|---|
| Lithium (USD/tonne) | 78,500 | 13,900 | -82% |
| Nickel (USD/tonne) | 27,800 | 15,500 | -44% |
| Cobalt (USD/tonne) | 33,500 | 18,900 | -44% |
| Battery Scrap (USD/kg) | 1.85 | 1.08 | -42% |

---

## 🗄️ Datasets Used

| Dataset | Source | Maps To |
|---|---|---|
| EV Sales & Trends | Kaggle | Buyer Pipeline, Market Intelligence |
| EV Charging Infrastructure | Kaggle | Collection Network |
| EV Battery Supply Chain & ESG Risk 2023-24 | Kaggle | Supplier Pipeline |
| Commodity Prices (Li/Ni/Co) | Self-generated (Macrotrends reference) | Market Intelligence |
| Pipeline Mock Data | Self-generated | All 4 sections |

---

## 🧮 DAX Measures

```dax
-- Supplier Pipeline
Total Supplier Leads = COUNTROWS(SupplierPipeline)
Supplier LOI Received = COUNTROWS(FILTER(SupplierPipeline, SupplierPipeline[stage] = "LOI Received"))
Supplier Conversion Rate = DIVIDE([Supplier LOI Received], [Total Supplier Leads], 0)
Supplier Qualified Count = COUNTROWS(FILTER(SupplierPipeline, SupplierPipeline[stage] = "Qualified"))
Avg Supplier ESG Risk = AVERAGE(SupplierPipeline[esg_risk_score])

-- Buyer Pipeline
Total Buyer Leads = COUNTROWS(BuyerPipeline)
Buyer LOI Received = COUNTROWS(FILTER(BuyerPipeline, BuyerPipeline[stage] = "LOI Received"))
Buyer Conversion Rate = DIVIDE([Buyer LOI Received], [Total Buyer Leads], 0)
Sample Requested Count = COUNTROWS(FILTER(BuyerPipeline, BuyerPipeline[stage] = "Sample Requested"))

-- Collection Network
Total Collection Points = COUNTROWS(CollectionPoints)
Active Collection Points = COUNTROWS(FILTER(CollectionPoints, CollectionPoints[status] = "Active"))
Total Monthly Volume KG = SUM(CollectionPoints[estimated_monthly_kg])

-- Market Intelligence
Latest Lithium Price = CALCULATE(LASTNONBLANK(CommodityPrices[lithium_usd_per_tonne], 1), LASTDATE(CommodityPrices[date]))
Latest Nickel Price = CALCULATE(LASTNONBLANK(CommodityPrices[nickel_usd_per_tonne], 1), LASTDATE(CommodityPrices[date]))
Latest Cobalt Price = CALCULATE(LASTNONBLANK(CommodityPrices[cobalt_usd_per_tonne], 1), LASTDATE(CommodityPrices[date]))
Latest Battery Scrap Price = CALCULATE(LASTNONBLANK(CommodityPrices[battery_scrap_usd_per_kg], 1), LASTDATE(CommodityPrices[date]))
```

---

## 🔗 Data Model (Star Schema)

```
DateTable (1)
    └── CommodityPrices (*)

Supply_chain_clean (*)
    └── SupplierPipeline (*)

ev_sales_clean (*)
    └── BuyerPipeline (*)

CollectionPoints
    (standalone — used for map visual via lat/lon)
```

---

## 🎨 Design Standards

| Element | Value |
|---|---|
| Primary Color | `#1A6B3A` (Deep Green) |
| Secondary Color | `#00695C` (Teal) |
| Alert/Highlight | `#F57F17` (Gold) |
| Font | Calibri / Arial |
| Theme | JOL Energy Custom |

---

## 💡 Key Insights

1. **Supplier Pipeline bottleneck** — 37.5% drop-off between Contacted and Qualified stages. Structured 3-touch outreach recommended.
2. **Tesla Supply Chain lead** (9,000 KG/month potential) is stuck at Leads Generated — highest priority escalation.
3. **Lithium prices dropped 82%** from peak — ideal time to lock offtake agreements and build battery scrap inventory.
4. **8 Prospective collection points** represent 15% volume upside when activated.
5. **Battery scrap spread is widening** — recycling margins improving despite lower absolute prices.

---

## 🛠️ Tools & Technologies

- **Power BI Desktop** — Dashboard development, DAX measures, data modeling
- **Microsoft Excel / WPS Office** — Data cleaning, mock data generation
- **Kaggle** — Public EV datasets
- **Power Query** — ETL transformations
- **DAX** — KPI calculations and measures

---

## 📋 Deliverables Checklist

- [x] Power BI Dashboard (.pbix)
- [x] Exported PDF (all 4 pages)
- [x] Cleaned Kaggle datasets (.xlsx)
- [x] Mock pipeline data (.xlsx)
- [x] Insights Report (.docx)
- [x] Screenshots (4 pages)
- [x] Technical Documentation
- [x] README (this file)

---

## 📄 License

This project was created as part of an internship assessment for JOL Energy Pvt. Ltd. All pipeline data is simulated and does not represent real business data.

---

<div align="center">

**JOL Energy Pvt. Ltd. | Business Dashboard | SDE & Data Analytics Track**

*Built with Power BI | Data-driven insights for battery recycling operations*

</div>
