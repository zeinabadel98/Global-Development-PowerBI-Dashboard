# Global Development & Country Comparison Dashboard

**Tools:** Microsoft Power BI Desktop · Power Query · M Language · DAX

## Project Overview

This project explores economic, population, and health indicators across countries and territories. The goal is to make country-level comparisons easier through an interactive, multi-page Power BI report.

The dataset includes indicators such as GDP, GDP per capita, population, life expectancy, infant mortality, birth rate, and inflation. The analysis is **cross-sectional**: the supplied data does not include a year column, so the report should not be interpreted as a time-series analysis of trends.

## Business Questions

- How do countries and territories compare in total GDP and GDP per capita?
- What differences appear in life expectancy and infant mortality?
- How are selected economic indicators associated with health outcomes?
- Which countries rank highest for a selected development indicator?
- How can a user explore one country's profile and compare it with others?

## Data Preparation

The source data was prepared in **Power Query**:

1. Split the imported data into separate fields using the semicolon delimiter.
2. Promoted the first row to column headers and removed the extra data-type row.
3. Set appropriate data types and handled non-numeric or missing values without assuming they represent zero.
4. Created derived fields such as **Population Density** and **Data Completeness %**.
5. Created a referenced `Country_Indicators` query and **unpivoted** GDP per capita, life expectancy, and infant mortality into `Country`, `Indicator`, and `Indicator Value` columns.
6. Related `Country_Indicators` to the main country table through the `Country` field using a many-to-one relationship, with single-direction filtering.

The main table was retained for existing report calculations and visuals; the unpivoted table supports the selectable indicator comparison.

## Report Pages

| Page | Purpose |
| --- | --- |
| **Overview** | High-level KPIs, geographic view, and top locations by GDP |
| **Economic Analysis** | GDP per capita, inflation, and economic comparison charts |
| **Health & Population** | Life expectancy, birth rate, infant mortality, and their relationship to economic indicators |
| **Country Comparison** | Side-by-side rankings, a formatted comparison table, and an interactive indicator explorer |
| **Country Profile** | Country-specific detail page, designed for drill-through |
| **Country Tooltip** | Supporting page for report-page tooltips |

## DAX & Analytics

The report uses measures for country counts, total GDP, total population, average GDP per capita, average inflation, average life expectancy, average infant mortality, average birth rate, GDP rank, GDP share, population share, and related comparisons.

A **GDP Category** calculated column groups locations by GDP per capita using project-defined thresholds; these are analytical bands, **not official World Bank income classifications**.

Examples of techniques used include `AVERAGE`, `SUM`, `DISTINCTCOUNT`, `DIVIDE`, `CALCULATE`, `ALLSELECTED`, `RANKX`, and `SELECTEDVALUE`.

## Interactive Features

- Country and indicator slicers
- Map-based country exploration
- Drill-through to the Country Profile page
- Report-page tooltip
- Bookmark-based filter reset
- Conditional formatting in the country comparison table
- Dynamic country profile title
- Performance review using Power BI Performance Analyzer

## Key Considerations

- **Countries and territories:** the source contains both; counts should be described as *locations* rather than strictly sovereign countries.
- **European Union:** the aggregate entry was excluded from the working report to avoid combining an aggregate with its constituent countries.
- **Missing data:** available-country averages exclude blank values; the report should not treat missing indicators as zero.
- **Different units:** GDP per capita, life expectancy, and infant mortality should be compared as separate indicators, not summed together.
- **No time dimension:** the source has no year field, so the dashboard does not claim historical population or GDP trends.
- **Correlation is not causation:** relationships in scatter plots are exploratory, not causal conclusions.

## How to Open

1. Download the `.pbix` file from this repository.
2. Open it in **Microsoft Power BI Desktop**.
3. Use the slicers and charts to explore locations and indicators.
4. Right-click a country data point where drill-through is enabled and select **Country Profile**.

> If the source Excel file is stored outside this repository, refreshing Power Query may require updating the source file path in Power BI Desktop. Report map visuals may also depend on local Power BI security/network settings.

## Repository Files

```text
Global-Development-PowerBI/
├── README.md
├── <your-final-report>.pbix
└── screenshots/
    ├── overview.png
    ├── economic-analysis.png
    ├── health-population.png
    └── country-comparison.png
```

*Replace `<your-final-report>.pbix` with the actual filename, and add screenshots only after exporting them from the completed report.*

## Portfolio Summary

An interactive Power BI project for exploring global economic and health development indicators. It demonstrates Power Query transformations, unpivoting, data modeling, DAX measures, multi-page report design, country comparisons, drill-through, bookmarks, tooltips, and conditional formatting.
