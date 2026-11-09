# EduLearn: Online Course Performance Dashboard (Power BI)

A Power BI report for an online learning platform: revenue against target, course completion, ratings, and which instructors need support.

> Screenshots will be added to the `images/` folder.

## Business questions

1. Is net revenue on track against the monthly target?
2. Which course categories drive enrollments and revenue?
3. Are students completing the courses they start?
4. Which instructors have low completion or low ratings, and need support?

## Data

| Table | Rows | Grain |
|---|---|---|
| Enrollments (fact) | 3,997 | One enrollment of a student in a course |
| Student | 891 | One student: age group, country, education level, acquisition channel |
| Course | 30 | One course: category, level, duration, price, language |
| Instructor | 14 | One instructor: specialty, experience |
| Date | 1,096 | One day, Jan 2024 – Dec 2026 |
| Targets | 36 | Monthly net revenue target |

Source: `data/EduLearn_Analytics_Practice_Dataset_final.xlsx` (practice dataset).

## Data model

Star schema with `Enrollments` as the fact table, related to `Student`, `Course`, `Instructor` and `Date` (enrollment and completion dates). `Targets` connects to `Date` by month. Two field-parameter tables (`Metric`, `Dimension`) let the user switch what a chart measures and how it is split.

## DAX highlights

| Measure | Why it matters |
|---|---|
| `Net Revenue` = price paid − refunds | Revenue the business actually keeps |
| `Net Revenue Target (to date)` | Compares revenue only with the target up to the last month that has data, so a partial month does not look like a miss |
| `Revenue vs Target %` | Net revenue ÷ target to date |
| `Completion Rate (Matured)` | Counts only enrollments older than 120 days, so recent students who have not had time to finish do not pull the rate down |
| `Avg Rating (Reliable)` | Shown only when there are at least 10 ratings |
| `Instructor Status Color` | Flags instructors red when both completion (< 60%) and rating (< 3.3, with 10+ ratings) are weak |
| `Title Net Revenue` | Dynamic chart title that states the selected category and year |

## Report pages

| Page | What it shows |
|---|---|
| Overview | KPI cards, net revenue vs target by month, enrollments by category, slicers |
| Instructors | Instructor table with conditional status colours and a completion-vs-rating scatter chart |
| Instructor Detail | Drill-through page with KPI cards and a gauge for one instructor |

## Key figures

| KPI | Value |
|---|---|
| Enrollments | 3,997 by 891 students |
| Net revenue | 4.41M (refunds are 2.7% of price paid) |
| Completion rate (all enrollments) | 64.0% |
| Average rating | 3.62 / 5 |
| Largest category | Data & Analytics: 1,463 enrollments, 1.48M revenue |
| Lowest-rated category | Digital Marketing: 3.27 average rating |

## How to open

Open `EduLearn Course Analytics.pbip` in Power BI Desktop. In Power Query, update the file path to where you saved `data/EduLearn_Analytics_Practice_Dataset_final.xlsx`, then refresh.

## Author

**Omar Saad Abu Al-Khair**, Data Analyst · [LinkedIn](https://www.linkedin.com/in/omar-abualkhair) · [Portfolio](https://omar-abualkhair.github.io)
