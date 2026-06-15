# NFL Salary Cap Efficiency Analysis

An exploration of how NFL teams allocate their salary cap and how those
allocation decisions translate to on-field performance, covering the
2013-2022 seasons.

## Live Dashboard

[View interactive Tableau dashboard](https://public.tableau.com/views/NFL_cap_efficiency/NFLCapAllocationEfficiency?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

## The Question

In a salary-capped league, every dollar spent on one position is a dollar
not available for another. Do teams that allocate more cap space to
quarterbacks win more games? Are there diminishing returns on QB spending?
Which franchises have been most efficient at turning spending into wins?

## Findings

- **Diminishing returns on QB spending:** Teams in the medium spend tier
  (10-15% of cap on QB) averaged a 53.5% win rate, marginally outperforming
  high-spend teams (>15% of cap on QB) at 52.9%. Both significantly
  outperformed low-spend teams (under 10%) at 47.3%.

- **Rookie contracts drive efficiency:** The most efficient team-seasons
  (wins per $10M of QB spending) overwhelmingly featured quarterbacks on
  rookie deals — Russell Wilson's early Seahawks, Patrick Mahomes' first
  Chiefs years, Dak Prescott's early Cowboys.

- **Sustained efficiency varies by franchise:** The Seahawks, Cowboys, and
  Eagles lead in average wins per $10M of QB spending across the decade,
  while their playoff rates differ significantly — suggesting front-office
  philosophy matters as much as raw spending.

## Data

- **Source:** NFL salary cap data combined with team performance metrics
- **Scope:** 320 team-seasons across 10 NFL seasons (2013-2022)
- **Granularity:** One row per team per season, with position-group salary
  breakdowns and performance metrics

## Pipeline

1. **Data ingestion (Python/pandas)**
   - Loaded raw salary and performance data from two sources
   - Standardized team names across franchise relocations (Raiders, Chargers,
     Rams, Washington)
   - Selected analytical columns and handled missing values

2. **Feature engineering (Python/pandas)**
   - Calculated wins per $10M of QB spending (efficiency metric)
   - Computed position group spending percentages
   - Created spending tier categorization (Low/Medium/High)
   - Output to clean CSV for downstream loading

3. **Database loading and analysis (PostgreSQL via DBeaver)**
   - Loaded cleaned data into PostgreSQL
   - Wrote analytical queries using window functions, CTEs, and aggregate
     queries to surface spending patterns by team, season, and tier
   - Exported query results to CSV

4. **Visualization (Tableau Public)**
   - Built interactive dashboard with four connected views
   - Implemented cross-filtering and team-level drilldown

## Tools

- **Python:** pandas, NumPy
- **Database:** PostgreSQL, DBeaver
- **Visualization:** Tableau Public Desktop
- **Version control:** Git, GitHub

## Repository Structure

```
NFLSalaryCapAnalysis/
├── data/
│   ├── raw/                          # Source data files
│   │   ├── NFL Salary By Position Group.xlsx
│   │   ├── nfl_salary_by_position_group.csv
│   │   └── team_stats_2003_2023.csv
│   └── clean/
│       └── final_nfl_cap_data.csv    # Final cleaned dataset
├── notebooks/
│   └── NFLSalaryCapAnalysis.ipynb    # pandas data cleaning and feature engineering
├── sql/                              # PostgreSQL query result exports
│   ├── nfl_cap_main.csv
│   ├── QB_spending_eff.csv
│   ├── average_QB_spending_by_team.csv
│   ├── teams_by_QB_spend.csv
│   ├── top_spending_seasons.csv
│   ├── spend_and_w_pct.csv
│   ├── playoff_vs_non_spending.csv
│   ├── szn_to_avg_qb_spend.csv
│   ├── team_pt_diff.csv
│   ├── overspending_comp_avg.csv
│   └── dead_cap.csv
└── Tableau/
    └── NFL_cap_efficiency.twbx       # Tableau workbook
```

## What I'd Do Differently

- Extend the analysis to per-position granularity (e.g., RB spending efficiency,
  WR spending efficiency) rather than just QB
- Add player-level injury data to control for availability
- Incorporate strength of schedule adjustments to normalize wins across teams
- Build a predictive model on top of the descriptive analysis

## Author

Jay Karki | [LinkedIn](https://www.linkedin.com/in/jaykarki/) | jayukarki11@gmail.com
