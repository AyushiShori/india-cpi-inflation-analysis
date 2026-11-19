# India CPI Inflation Analysis (2013–2023)

**A case study in applied inflation analysis — built entirely in Excel.**

Five business questions on India's Consumer Price Index, answered using Power Query, PivotTables, PivotCharts and correlation analysis across 10,044 records.

---

## Problem Statement

India's Consumer Price Index is a fixed basket tracking household spending across 27 expenditure heads — cereals, vegetables, housing, fuel, healthcare, transport, education. It is the benchmark the RBI targets when setting interest rates, and the reference point for wage indexation and welfare spending across the country.

The basket is also unusually food-heavy, which makes Indian retail inflation more exposed to supply shocks than headline figures alone reveal. This project interrogates that exposure across a decade of monthly data (2013–2023), asking four questions:

- How is the basket actually structured, and which categories carry it?
- How has inflation moved year on year, and what drove the peak?
- Did COVID-19 produce a measurable break in the trend, or continue it?
- How far do global crude oil price movements travel into Indian consumer prices, and which categories absorb them?

The analysis is delivered as a single Excel workbook — cleaned data, a long-format model, and one analysis sheet per question.

---

## Business Questions

**Q1 — Which category contributes most to the CPI basket?**
Group the 27 individual line items into broader buckets (Food, Housing, Health, Transport, Education and so on), then calculate each bucket's share of the overall basket for the most recent month. Shares must sum to 100%.

**Q2 — How has year-on-year inflation moved since 2017?**
Compute Y-o-Y growth on the General Index for the combined Rural + Urban basket, chart the trend, identify the peak year, and research what drove it.

**Q3 — What happened inside the food basket over the last 12 months?**
Break the Food bucket into its sub-categories and track month-on-month price changes. Identify the highest and lowest inflation months, and determine which individual sub-category drove the most movement.

**Q4 — Did COVID-19 change the inflation picture?**
Treating March 2020 as the pandemic onset, compare inflation before and after that point, with particular attention to Food, Health and essential household services.

**Q5 — How do global oil prices feed through to Indian inflation?**
Using month-on-month imported fuel price data for 2021–2023, measure the correlation between oil movements and each CPI category, and identify which categories are most exposed.

---

## Dataset

| Attribute | Detail |
|---|---|
| Source | Ministry of Statistics & Programme Implementation (MoSPI), Government of India |
| Period covered | January 2013 – May 2023 |
| Frequency | Monthly |
| Sectors | Rural, Urban, Rural+Urban (Combined) |
| Categories | 27 expenditure heads plus the General Index |
| Raw records | 373 rows × 30 columns |
| Modelled records | 10,044 rows after unpivoting to long format |

Each value is an **index number**, not a price. Index values are relative to a base year and cannot be summed across months or categories — all analysis therefore works with *percentage change* between periods rather than levels.

### Data Quality Notes

- **Missing values** appear in several early-period columns, marked `NA` in the source. These were imputed using a moving average of surrounding months rather than dropped, preserving the continuity of the time series.
- **2023 is a partial year** — the data ends in May. Any annual figure for 2023 is a five-month average and is not directly comparable to a full twelve-month year.
- **Category naming is inconsistent** in the source (trailing spaces produce duplicate labels such as `Clothing` and `Clothing `). These were preserved in the raw sheet and handled during classification.

---

## Approach

**1. Preserve the original.** The `Raw Data` sheet is an untouched copy of the source extract. Nothing is edited here, so the analysis can always be traced back to what was actually downloaded.

**2. Clean and impute.** The `ConsumerPrice Index` sheet holds the working copy — missing values filled, types corrected, labels standardised.

**3. Reshape wide to long.** The source arrives with one column per category, which PivotTables handle badly. Power Query unpivots this into a long format with one row per sector–year–month–category combination. This is the single most important structural decision in the project: 373 wide rows become 10,044 long rows, and every subsequent pivot becomes trivial.

**4. Classify into buckets.** A `Classified As` column maps each of the 27 granular categories into a broader bucket — Food, Housing, Health, Transport, Education, Luxury, Miscellaneous. This is what makes Q1 answerable and Q3 scopeable.

**5. Build one sheet per question.** Each `Insight` sheet contains its own PivotTable, derived growth-rate calculations, slicers for interactive filtering, and a chart. Keeping questions isolated means a change to one analysis cannot silently break another.

---

## Key Findings

**Food dominates the basket — and therefore dominates inflation.**
At 44.4% of the basket under equal weighting, Food accounts for twelve of the twenty-seven line items. Any analysis of Indian inflation that does not lead with food is analysing the wrong thing.

**2022 was the peak inflation year of the period.**
Y-o-Y growth on the combined Rural+Urban General Index reached 6.62%, driven by post-pandemic demand recovery colliding with constrained supply, the Russia–Ukraine conflict's effect on energy and fertiliser prices, and elevated global commodity costs. Rural inflation ran marginally ahead of urban in this year, reversing the pattern of 2019–2021.

**Vegetables drive short-term food inflation; staples drive the trend.**
Over the twelve months to May 2023, Vegetables produced both the sharpest rise and the sharpest fall in the food basket — swinging from +5.5% in May 2022 to −12.8% in December 2022. Milk and Pulses, by contrast, rose steadily throughout — less dramatic month to month, but a more persistent contributor to the cumulative increase.

**COVID-19 produced a measurable, category-specific shock.**
Food and beverages inflation rose from 4.2% in 2019 to 7.8% in 2020 as lockdowns disrupted supply chains and transport networks. The effect was not uniform across the basket — categories tied to physical distribution moved more than those that were not.

**Oil transmission is concentrated, not diffuse.**
Transport & Communication correlates with imported fuel prices at 0.67, against 0.34 for Education. Imported fuel prices do not raise all prices equally — transmission runs through categories with direct fuel exposure and weakens substantially beyond them.

---

## Assumptions & Limitations

**Equal weights are assumed across categories.** The brief specifies this, and the analysis follows it. In reality MoSPI assigns weights based on household expenditure share — Food and beverages alone carries roughly 46% in the official Combined index. Contribution figures here should therefore be read as *basket composition under equal weighting*, not as official weighted contribution.

**Correlation is not causation.** The oil analysis in Q5 establishes co-movement, not a causal mechanism. Both oil prices and transport costs respond to shared underlying factors, and the correlation does not isolate a direction of effect.

**2023 is incomplete.** All 2023 figures cover January through May only.

**Imputed values are estimates.** Moving-average imputation preserves trend continuity but introduces smoothing. Months with imputed inputs will understate genuine volatility.

---

## Skills Demonstrated

**Data preparation** — Power Query transformations, wide-to-long unpivoting, moving-average imputation, category classification and standardisation.

**Analysis** — Year-on-year and month-on-month growth calculations, correlation analysis using `CORREL`, period-over-period comparison around a defined event.

**Modelling** — Separation of raw, cleaned and modelled layers; a single long-format source feeding multiple independent PivotTables.

**Visualisation** — PivotCharts across pie, bar and line formats; slicers for interactive cross-filtering; one visual per analytical question.

---

*Data sourced from publicly available MoSPI releases. This project was completed as an analytical case study.*
