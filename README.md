Vanguard A/B Test — UX Redesign Analysis

- [Presentation link](https://docs.google.com/presentation/d/1lGH5Y6p-mxHJRQSHTaX6tOOv4QyF9S-Wy4TJtKxTIVs/edit?slide=id.gc6f980f91_0_0#slide=id.gc6f980f91_0_0)

Project Overview

This project analyzes the results of an A/B experiment conducted by Vanguard to evaluate the impact of a new digital interface (Test) compared to the previous design (Control).

The main goal is to determine whether the new design improved the user experience by increasing completion rates, reducing time per step, and minimizing user errors.

The analysis includes:

Data cleaning & integration across three datasets

Exploratory Data Analysis (EDA)

KPI calculation (Completion Rate, Error Rate, Time per Step)

Statistical hypothesis testing (Z-test)

Cost-effectiveness validation (≥ +5 percentage points threshold)

Visualization of results (Python & Tableau)

🧩 Datasets Used
| Dataset                           | Description                          | Key Columns                                                     |
| --------------------------------- | ------------------------------------ | --------------------------------------------------------------- |
| `df_final_web_data_pt_`           | Web log data (user navigation steps) | `visit_id`, `visitor_id`, `process_step`, `date_time`           |
| `df_final_experiment_clients.txt` | Experiment roster                    | `client_id`, `Variation (Test/Control)`                         |
| `df_final_demo.txt`               | Client demographics                  | `client_id`, `clnt_age`, `gendr`, `clnt_tenure_yr`, `num_accts` |

After merging and cleaning, the combined dataset (dw) contained 755,405 user events.

🧼 Data Cleaning Summary

Main cleaning steps performed:

Fixed column delimiters — handled incorrectly separated headers (, instead of \t).

Merged datasets — joined web logs, demographics, and experiment roster on client_id.

Removed duplicates — eliminated 185 users appearing in both Test and Control groups.

Created age_band — categorized clients in 10-year intervals.

Handled missing values — preserved NaN for transparency in demographics.

Before cleaning: ~765K rows
After cleaning: 755,405 valid events (≈ 99% usable)

🔍 Exploratory Data Analysis (EDA)

Key findings:

Majority of users are between 30–59 years old, evenly distributed across Test and Control.

Tenure and engagement (logins, calls) correlate weakly with conversion, suggesting UX design is the key factor.

Users over 60 years showed slower progression and higher backtracking rates.

📈 Performance Metrics
| KPI                 | Definition                                   | Purpose                              |
| ------------------- | -------------------------------------------- | ------------------------------------ |
| **Completion Rate** | % of users reaching the final “confirm” step | Main success indicator               |
| **Time per Step**   | Avg. duration between steps                  | UX efficiency                        |
| **Error Rate**      | % of backward moves (users going back)       | Measures confusion or poor usability |

🔹 Global Completion Rate

Test: 64,4%

Control: 51,7%

Improvement: +Z percentage points
✅ Statistically significant (p < 0.05)
✅ Meets cost-effectiveness threshold (+5 p.p.)

🔹 By Age Band

Biggest improvement observed among 30–49-year-olds.

Groups 60+ showed slightly more navigation errors (likely due to UI complexity).

🧪 Hypothesis Testing
🎯 Test #1 — Completion Rate Difference

Null Hypothesis (H₀): Completion rate (Test) = Completion rate (Control)
Alternative (H₁): Completion rate (Test) ≠ Completion rate (Control)

📊 Method: Two-proportion Z-test
📈 Result: Statistically significant (p < 0.05)

💰 Test #2 — Cost-Effectiveness Threshold

Business rule: The redesign must increase completion rate by at least 5 percentage points to justify costs.

✅ The observed increase exceeds +5 p.p.
✅ Statistically significant → redesign is cost-effective

🧮 Key Visualizations

Completion Rate — Test vs Control

Global and by age band (+5% threshold line)

Error Rate per Step

Shows where users backtrack most often

Time per Step

Step duration comparison between groups

Z-test Results

p-value annotations per age band

Tableau Dashboard

Interactive visual filters by age & group

📊 Tableau Dashboard

An interactive Tableau dashboard was built to visualize:

Completion rate differences

Error rates

Time spent per step

Demographic breakdowns

🎨 Filters available: Age Band, Variation (Test/Control)

🔗 View Dashboard on Tableau Public
### 🔗 Dashboards no Tableau Public

- [Tableau_1](https://public.tableau.com/app/profile/sina.ahmadian.yazdi/viz/Vangaurd2/Avg_BackwardMovespervisitbyage)
- [Tableau_2](https://public.tableau.com/views/Vangaurd2/Avg_BackwardMovespervisitbyage?:language=de-DE&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
- [Tableau_3](https://public.tableau.com/views/Vanguard_17598448949960/AgeDistribution?:language=de-DE&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)


🧰 Tech Stack
| Category            | Tools Used                   |
| ------------------- | ---------------------------- |
| Language            | Python 3                     |
| Data Analysis       | Pandas, NumPy                |
| Visualization       | Matplotlib, Seaborn, Tableau |
| Statistical Testing | Statsmodels, SciPy           |
| Notebook            | Jupyter Notebook             |
| Version Control     | Git / GitHub                 |

🧑‍💻 Repository Structure
vanguard-ab-test/
│
├── data/
│   ├── raw/                   # Original datasets (.txt, .zip)
│   ├── processed/             # Cleaned and merged data
│
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_kpi_analysis.ipynb
│   ├── 03_hypothesis_testing.ipynb
│
├── scripts/
│   ├── data_cleaning.py
│   ├── performance_metrics.py
│   ├── ztest_analysis.py
│
├── tableau/
│   ├── dashboard.twbx
│
├── README.md
└── requirements.txt

🎓 Lessons Learned

Importance of structured data merging and cleaning in real-world datasets.

How small navigation frictions impact conversion.

Practical application of Z-tests for business decision-making.

Integration of data science + UX analysis for evidence-based redesigns.

🏁 Conclusion

✅ The Test design outperformed the Control in both completion and usability.
💰 It exceeded Vanguard’s 5% ROI threshold.
📊 Statistical testing validated that the improvement is real and significant.

Recommendation:
Roll out the new design for most users, but improve accessibility for users aged 60+ (e.g., clearer labels, larger buttons).
