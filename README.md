# Global-B2B-Sales-Pipeline-Analysis
A 3-page Power BI dashboard built on 11,750 deals and 117,500 activities to answer one question , why is a £1 billion pipeline only converting 23.6% into revenue.
# Global B2B Sales Pipeline & Deals Analytics
### FP20 Analytics Challenge 35 | Power BI Dashboard

![Dashboard Preview](screenshots/overview.png)

---

## The Problem

A global B2B SaaS and Professional Services company had a pipeline worth over **£1 billion** but was only converting **23.6%** of it into actual revenue. Leadership had no clear visibility into where deals were stalling, which reps were performing, which products were winning and how much pipeline was silently going cold without anyone noticing.

The business was flying blind on four critical questions:

- Where exactly are deals dying in the pipeline?
- Are sales reps engaging with clients enough to win?
- How reliable is the revenue forecast?
- Which open deals are at risk of being lost right now?

Without answers to these questions, every revenue target was essentially a guess.

---

## The Dataset

| Table | Rows | Key Columns |
|---|---|---|
| FactDeals | 11,750 | DealID, DealValueEUR, Status, StageName, StageOrder, BaseWinProbability, ProductCategory |
| FactActivities | 117,500 | ActivityID, DealID, ActivityType, DurationMinutes |
| DimCompany | 1,000 | Industry, CompanySize, Region, Country, Latitude, Longitude |
| DimSalesRep | 55 | RepName, Role, Seniority, Region, JoinYear, LeaveYear |
| DimDate | 1,492 | Date, DateKey, Year, Quarter, Month, MonthName |

---

## My Approach

### Page 1 — Executive Overview
Built for leadership. Answers the big picture questions at a glance.

**5 KPI Cards:** Total Pipeline Value · Revenue Won · Win Rate % · Weighted Forecast · Avg Deal Value — each with YoY trend, directional icon and colour coding (green / amber / red)

**5 Visuals:**
- Line and Clustered Column Chart — pipeline value and deal volume over time
- Funnel Chart — stage-by-stage deal progression with conversion rates
- Filled Map — regional pipeline and win rate using Latitude/Longitude from DimCompany
- Stacked Bar Chart — industry revenue contribution (won vs open pipeline)
- Matrix Heatmap — seasonal deal closure patterns by month and year

**Key Finding:** Closing stage converts at only 41.86% while every other stage is above 82%. Deals are reaching the finish line and dying there.

---

### Page 2 — Sales Performance
Built for sales managers. Answers who is performing and why.

**5 KPI Cards:** Rep Win Rate % · Avg Activities Per Deal · SMB Avg Sales Cycle Days · Enterprise Avg Sales Cycle Days · High Engagement Win Rate

**5 Visuals:**
- Horizontal Bar Chart — top 15 rep leaderboard colour coded by seniority
- Clustered Bar Chart — activity type mix on Won vs Lost deals
- Doughnut Chart — SMB vs Enterprise sales cycle by region
- Matrix Scorecard — full rep performance table with conditional formatting

**Key Finding:** High Engagement Win Rate (59.31%) is almost identical to overall Win Rate (60.21%) — more activity is not the answer. Demo and Workshop activities are what actually separate Won deals from Lost deals.

---

### Page 3 — Risk, Forecast & Product Intelligence
Built for operations and revenue leadership. Answers what is at risk today.

**5 KPI Cards:** Weighted Forecast · Forecast Accuracy % · Deals at Risk · Pipeline Value at Risk · Top Product Win Rate

**5 Visuals:**
- Line Chart — weighted forecast vs actual revenue won month by month
- Bar Chart — product and service win rates ranked
- Bar Chart — at-risk deal count by stage name
- Bar Chart — at-risk deal count by rep name

**Key Finding:** £606M of open pipeline (59% of total) has had no activity in 30+ days. The weighted forecast consistently runs above actual revenue indicating stage probabilities are too optimistic.

---

## DAX Measures Built

| Category | Count |
|---|---|
| Base KPI measures | 15 |
| Prior Year (PY) measures | 11 |
| YoY % change measures | 11 |
| Icon measures (UNICHAR arrows) | 11 |
| Colour measures (hex conditional formatting) | 11 |
| Risk and activity calculated columns | 3 |
| **Total** | **62** |

### Key DAX Patterns Used
- `DATEADD(ALL(DimDate[Date]), -1, YEAR)` — YoY with slicer compatibility
- `AVERAGEX(VALUES(FactDeals[DealID]), CALCULATE(COUNTROWS(FactActivities)))` — activity per deal
- `DATEDIFF + LOOKUPVALUE` — sales cycle and days since last activity
- `SUMX(FILTER(...), DealValueEUR * BaseWinProbability)` — weighted forecast
- `UNICHAR(9650) / UNICHAR(9660) / UNICHAR(9654)` — trend icons
- Hex colour measures applied via conditional formatting fx button

---

## Key Insights and Recommendations

**1. The Closing stage is bleeding revenue**
41.86% conversion at Closing vs 82%+ everywhere else. Build a closing playbook, review every lost deal at that stage and train reps specifically on late-stage objection handling.

**2. £606M pipeline is going cold**
7,000 open deals inactive for 30+ days. Introduce a 48-hour re-engagement rule for any at-risk flagged deal. Eva Pereira (449), Lukas Bianchi (320) and Petra Ivanova (293) are the top three rep-level priorities.

**3. The business only works in H1**
Revenue peaks in June and collapses through H2. Restructure commission to incentivise H2 closures and start Q3/Q4 pipeline building in January.

**4. The forecast is overstated**
Weighted Forecast consistently runs above Revenue Won every month. Recalibrate BaseWinProbability per stage using actual historical conversion rates from the data.

**5. Activity quality beats activity quantity**
High engagement win rate and overall win rate are nearly identical. Demos and Workshops on Won deals significantly outnumber those on Lost deals. Coach reps on activity type not activity volume.

---

## Tools and Technologies

- **Power BI Desktop** — report building and DAX
- **DAX** — all measures and calculated columns
- **ZoomCharts Drill Down Map PRO** — regional map visual
- **Microsoft Azure Maps** — base map layer
- **Excel** — source dataset

---

## How to Use

1. Download the `.pbix` file from this repository
2. Open in Power BI Desktop
3. Use the Year slicer to compare specific years
4. Use the Region and Company Size slicers to drill into segments
5. Click any funnel stage, industry bar or rep name to cross-filter all visuals on the page

---

## Project Structure

```
├── FP20_Challenge35.pbix
├── Enterprise_Sales_Pipeline_Challenge_35.xlsx
├── screenshots/
│   ├── overview.png
│   ├── sales_performance.png
│   └── risk_forecast_intelligence.png
└── README.md
```

---

## Author

Faleye Olumide - Data Analyst|Power BI|Data Consultant
Built for **FP20 Analytics Challenge 35** organised by Federico Pastor and the FP20 Analytics Community in collaboration with ZoomCharts.
Ineractive link: https://lnkd.in/eXepmn9C Nigeria 🔗 Linkedin: https://www.linkedin.com/posts/olumide-david-79b17726a_powerbi-dax-dataanalytics-activity-7444408510194450432-0nzu?utm_source=social_share_send&utm_medium=member_desktop_web&rcm=ACoAAEHgVqcBelhbBzhkIpF2JSlZX6PrAp_NLVU 🌐 Portfolio: https://www.datascienceportfol.io/olumidedavid
*If this was useful, drop a star on the repo.*
