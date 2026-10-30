# App Insights Unlocked | Google Play Store Analytics

An interactive **Power BI portfolio project** exploring historical Google Play Store app listings to understand category composition, ratings, reported installation thresholds, review counts, pricing, app size, and last-update dates.

## Project overview

The goal is to turn a raw app-store CSV into an accessible analytical report that helps explore how applications differ across categories and business metrics. The project combines data preparation in Power Query, DAX measures, interactive metric selectors, and a multi-page Power BI report.

> **Scope:** This is a historical snapshot of app listings, not live Google Play Store data. The `Installs` field represents reported **minimum-install thresholds**, not exact downloads or unique users.

## Report structure

| Page | Focus |
| --- | --- |
| Dashboard Overview | High-level KPIs, selected charts, and interactive metric selectors |
| KPI Overview | Total apps, average rating, reported installs, reviews, categories, and high-rated apps |
| App Size Distribution | App counts across size bands |
| Free vs Paid Apps Distribution | Distribution by pricing model |
| Category Performance | Dynamic comparison of categories by apps, ratings, installs, and reviews |
| Top Apps Analysis | Top 10 app names by summed reported installs or reviews |
| App Pricing vs User Ratings | Scatter analysis of price and rating, segmented by app type |
| App Update Trends | Distribution of apps by the month of their **last recorded update** |

## Highlights

The following values are rounded as displayed in the Power BI report:

- **~10K** app records across **33** categories after cleaning.
- **4.19 / 5** average rating among records with ratings.
- **~7K** records with ratings of **4.0 or above**.
- **~147 billion** summed reported minimum-install thresholds and **~4 billion** summed reviews.
- **FAMILY** has the most app records (**1,943**); **GAME** leads summed reported installs (**~31.5 billion**) and reviews (**~1.42 billion**).
- **EVENTS** has the highest category-level average rating shown (**4.44 / 5**).
- **92.60%** of records are labeled Free and **7.39%** Paid; a small invalid/missing `Type` share is visible in the source analysis.
- Last-update dates are heavily concentrated in **2018**, within this historical dataset.

These are descriptive findings, not causal conclusions. Aggregation by app name can combine multiple records for the same application.

## Tools and techniques

- **Power BI Desktop:** report design, interactions, page navigation, and visual analytics
- **Power Query:** data-type fixes, cleaning, size conversion, and removal of malformed/exact-duplicate rows
- **DAX:** KPI measures, size groups, dynamic metric selection, and time-related calculations
- **CSV:** historical Google Play Store dataset

### Core DAX measures

```dax
Total Apps = COUNTROWS('googleplaystore')

Average Rating = AVERAGE('googleplaystore'[Rating])

Total Installs = SUM('googleplaystore'[Installs])

Total Reviews = SUM('googleplaystore'[Reviews])

Total Categories = DISTINCTCOUNT('googleplaystore'[Category])

High Rated Apps =
CALCULATE(
    COUNTROWS('googleplaystore'),
    'googleplaystore'[Rating] >= 4
)
```

## Data preparation

1. Imported the CSV into Power BI Desktop.
2. Removed a malformed category row and exact duplicate records.
3. Standardized numeric fields, including `Reviews`, `Installs`, `Price`, and `Rating`.
4. Parsed `Last Updated` as a date.
5. Converted reported app sizes to MB where possible; retained unknown sizes separately.
6. Created size bands, month-level last-update fields, and DAX measures.

## Data limitations

- **Installs:** Reported lower-bound buckets, not exact download totals. Summing them is descriptive only.
- **Repeated app names:** Multiple records with the same name may be aggregated together in top-app rankings.
- **Ratings:** Missing ratings are excluded from the average; ratings are not weighted by number of reviews.
- **Reviews:** Counts do not measure sentiment, active users, or retention. The dataset does not contain review text for sentiment analysis.
- **Updates:** Only the last-update date is available, so update frequency and total updates per month cannot be determined.
- **Pricing:** App prices do not establish revenue, profit, or the success of a monetization strategy.
- **Data quality:** Some size values are unknown, and a small number of `Type` entries may be invalid or missing.
- **Historical coverage:** Findings describe the supplied snapshot and should not be interpreted as current market conditions.

## Repository contents

```text
App-Insights-Unlocked/
├── Google_Play_Store_Analytics.pbix
├── README.md
├── data/
│   └── googleplaystore.csv
└── docs/
    ├── App_Insights_Unlocked_Case_Study.docx
    ├── App_Insights_Unlocked_Final_Solution_Guide.docx
    └── Additional_Resources.docx          # Add when prepared
```

*Adjust filenames and folder paths to match the files you actually upload. The Additional Resources document is planned and should not be linked until it exists.*

## How to explore the report

1. Download `Google_Play_Store_Analytics.pbix`.
2. Open it with **Microsoft Power BI Desktop**.
3. Start on **Dashboard Overview** for a summary.
4. Use the page navigator to explore detailed analysis.
5. Use the category metric selector and **Rank Apps By** selector to change chart measures.
6. If Power BI prompts for a data source, point it to the CSV in the `data` folder and refresh.

## Project documentation

- **Case Study:** business problem, objectives, data dictionary, and 25 analytical questions.
- **Solution Guide:** analytical approaches, observed findings, DAX examples, and explicit limitations for questions that cannot be fully answered.
- **Additional Resources:** further reading and reference material (to be added).

## Takeaway

This project demonstrates an end-to-end analytics workflow: cleaning a real-world dataset, defining interpretable measures, designing an interactive report, and communicating insights with appropriate caveats.
