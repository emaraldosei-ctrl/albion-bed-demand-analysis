# Albion Care Network — Bed Demand & Capacity Analysis

Forecasting bed demand and identifying capacity risk across **5 hospitals and 8 wards**, using two years of hourly operational data.

**Tools:** Power BI · Power Query (M) · DAX · DAX Studio · Excel
**Role:** Data Analyst (data cleaning, EDA, dashboard, reporting) — in a team with a Project Manager and a Data Scientist
**Data:** Hourly records, January 2024 – December 2025 · 130,993 admissions

> All figures in this project were verified against the source data before being reported.

---

## The problem

Albion Care Network managed bed capacity **reactively** — decisions were made only after shortages occurred — because operational data was fragmented and planning relied on historical averages. The goal was to consolidate the data into a single view and use it to anticipate demand, surface risk, and recommend practical improvements.

---

## Key findings

| Finding | Detail |
|---|---|
| **Demand is strongly seasonal** | Occupancy peaks at **86.3% in February**, bottoms at **59.7% in August** — a **16.8-point** winter-to-summer swing that repeats every year. |
| **Demand is emergency-driven** | **80%** of admissions are emergencies (unscheduled and unplannable); only 18% is elective. |
| **The average hides the pressure** | Network occupancy averages **74.6%**, but a **third of all ward-hours (33.6%)** are at 100% capacity. |
| **A staffing mismatch** | Occupancy swings 16.8 points while staffing varies only **9.6%** — the busiest months are the least cushioned. Safe staffing ratios were missed in **4.3%** of shifts (6.2% in winter vs 3.5% in summer). |
| **A clear breaking point** | Scenario modelling shows the network becomes operationally unsafe (>85%) at a **20% emergency surge**, and runs out of beds entirely at **~40%**. |
| **Bed-days concentrate in a few wards** | Oncology (123 hrs) and ICU (104 hrs) hold patients far longer than the network average (83 hrs). |

---

## What was built

A three-page Power BI report, designed so each page answers one question.

### 1. Executive Dashboard — occupancy, demand and risk at a glance

![Executive Dashboard](images/executive_dashboard.png)

Five headline KPIs, seasonality with the 85% safe-operating line, ward pressure with amber alerts, the emergency/elective demand mix, and the staffing-vs-demand risk.

### 2. Operational View — day-to-day detail for managers

![Operational Dashboard](images/operational-dashboard.png)

Occupancy trend over time, length of stay by ward, patient flow (admissions vs discharges), staffing plan vs actual, and occupancy by bed type — filterable by hospital, ward and date.

### 3. Scenario Planning — interactive what-if modelling

![Scenario Planning](images/scenario-planning.png)

Three what-if sliders (emergency surge, delayed discharges, bed closures) with preset **Today / Bad Flu Season / Discharge Crisis / Winter Crisis** bookmarks. Colour is used as a signal: KPI cards and ward bars turn amber then red as they cross the 85% safe threshold.

---

## Methodology

**1. Data cleaning (Power Query)** — Six source tables cleaned on the principle that *missing does not always mean broken*: most blanks were structurally correct and were retained, while genuine gaps were repaired. Length of stay was recomputed from timestamps; expected LOS was filled by procedure-group median; 486 duplicate rows were removed and 37 conflicting records flagged.

**2. Data modelling** — A star schema with a DAX Calendar dimension. A date-relationship bug (datetime columns failing to match against pure calendar dates) was diagnosed and fixed with date-only columns.

**3. Measures (DAX)** — 20+ measures including occupancy, beds available, hours at capacity, seasonal comparisons, and the scenario what-if measures. Every value was cross-checked against the raw data.

**4. Exploratory data analysis** — Trends, seasonality, correlations (emergency admissions and staffing vs occupancy) and length-of-stay distributions.

**5. Scenario planning** — What-if parameters modelling emergency surges, discharge delays and bed closures, anchored to the verified base occupancy rate.

**6. Reporting** — A written report, an insights deck, and evidence-based recommendations.

---

## Recommendations

Four actions, none requiring new physical beds:

1. **Flex staffing to the seasonal curve** — add winter cover for General Medicine and ICU, triggered at 85% occupancy.
2. **Target long-stay wards** — focus discharge planning on Oncology and ICU, where bed-days concentrate.
3. **Use elective scheduling as a release valve** — shift plannable work out of the winter peak into summer's spare capacity.
4. **Plan to the demand curve, not the average** — use the dashboard and scenario planner to anticipate winter before it arrives.

---

## Repository contents

```
├── documentation/     Data cleaning report, DAX measures reference, scenario docs, data dictionary, work log
├── reports/           Bed demand analysis report, EDA insights deck
├── presentation/      Report & recommendations presentation
└── images/            Dashboard screenshots
```

---

## Links

- **Live Power BI dashboard:** <!-- PASTE YOUR PUBLISHED POWER BI LINK HERE -->
- **Analysis report:** see `/reports`
- **Full documentation:** see `/documentation`

---

## Notes

- This project uses a **fictional dataset** provided as part of a data analytics internship program. The raw data is not included in this repository.
- The analysis covers a **five-hospital sample** of the wider network.
- The **85% safe-occupancy figure** is an established healthcare planning benchmark, not a value derived from the dataset.
- Forecasting models (SARIMAX, XGBoost and others) were developed by the Data Science track and are referenced in the presentation; the analytics, dashboard and recommendations here are the Data Analyst deliverables.

---

*Built by Esmeralda Osei · [LinkedIn](https://www.linkedin.com/in/esmeralda-pinamang-osei-942a35111) · [Portfolio](https://emaraldosei-ctrl.github.io)*
