# 🏏 T20 World Cup 2022 — Best XI Player Selection (Data-Driven Team Analytics)

**Executive Summary:** Built a criteria-driven player selection system using T20 World Cup 2022 data, scraped from ESPNcricinfo, cleaned with Python/pandas, and modeled into an interactive Power BI dashboard. The dashboard filters 200+ players against role-specific performance thresholds (Power Hitters, Anchors, Finishers, All-Rounders, Specialist Fast Bowlers) to arrive at a statistically optimal Best XI.

---

## 📑 Table of Contents
- [Business Problem](#-business-problem)
- [Objective](#-objective)
- [Live Dashboard](#-live-dashboard)
- [Dataset](#-dataset)
- [Tools & Tech](#-tools--tech)
- [Workflow](#-workflow)
- [Business Questions Answered](#-business-questions-answered)
- [Key Insights](#-key-insights)
- [Business Recommendations](#-business-recommendations)
- [KPI Impact](#-kpi-impact)
- [Business Impact](#-business-impact)
- [Dashboard Preview](#-dashboard-preview)
- [How to Run](#-how-to-run)
- [Future Work](#-future-work)
- [Author & Contact](#-author--contact)

---

## ⭐ Business Problem
Team selection in cricket is often driven by reputation, recency bias, or gut feel rather than consistent, role-specific statistical evidence. Selectors need an objective way to identify which players actually meet the performance bar for their intended role (opener, anchor, finisher, all-rounder, fast bowler) using a full tournament's worth of data — not just headline stats.

## 🎯 Objective
Design and build an end-to-end analytics pipeline that:
- Scrapes ball-by-ball and scorecard-level T20 World Cup 2022 data from ESPNcricinfo
- Cleans and models the data into a proper star schema
- Applies role-specific statistical filters (batting average, strike rate, boundary %, bowling economy, strike rate, dot-ball %) to shortlist players
- Surfaces the results in an interactive Power BI dashboard that lets a selector compare, combine, and finalize a Best XI

## 🚀 Live Dashboard

Explore the interactive Power BI dashboard here:

**🔗 Power BI Service:**  
https://app.powerbi.com/groups/me/reports/dd0c8abc-d855-47a3-a45d-99a14e5b7cd3/ReportSection3a8cb23b814911c94608?experience=power-bi

> **Note:** The report may require Power BI access permissions.  

## 🗂 Dataset
- **Source:** ESPNcricinfo (T20 World Cup 2022), scraped via Bright Data's Data Collector
- **Tables collected:**
  - Match Results (45 matches)
  - Batting Summary (ball-by-ball batting scorecards)
  - Bowling Summary (bowling scorecards)
  - Player Info (role, batting/bowling style, team, image)
- **Format:** Raw JSON → transformed to flat CSV files for Power BI ingestion

## 🛠 Tools & Tech
| Category | Tools |
|---|---|
| Web Scraping | Bright Data (Data Collector), JavaScript |
| Data Cleaning & Transformation | Python, Pandas, JSON |
| Data Modeling | Power BI (Star Schema), Power Query |
| Visualization | Power BI, DAX |
| Version Control | Git, GitHub |

## 🔄 Workflow
```
ESPNcricinfo (Web Scraping via Bright Data)
        ↓
Raw JSON Files (Match Summary, Batting, Bowling, Player Info)
        ↓
Python + Pandas (Cleaning, Out/Not-Out flag, Match ID mapping, Name cleanup)
        ↓
Flat CSV Files
        ↓
Power BI (Power Query transformation + Star Schema modeling)
        ↓
DAX Measures & Calculated Columns
        ↓
Interactive Dashboard (Role-based filtering → Best XI selection)
```

**Star Schema:**
- **Fact tables:** `fact_batting_summary`, `fact_bowling_summary`
- **Dimension tables:** `dim_players`, `dim_match_summary`
- Relationships built on `match_id` (matches) and `player name` (batting/bowling ↔ player info)

## ❓ Business Questions Answered
- Which players statistically qualify as elite Power Hitters/Openers based on strike rate, boundary %, and consistency?
- Who are the best Anchors capable of building an innings while keeping strike rate competitive?
- Which finishers can be trusted to close out an innings under pressure?
- Which all-rounders offer the best balance of batting strike rate and bowling economy for the middle order?
- Which fast bowlers deliver the best combination of economy, strike rate, and dot-ball percentage?
- What does the optimal, data-backed Best XI look like — and how does swapping one player affect team-level batting average and strike rate?

## 💡 Key Insights
- Applying strike rate (>140), batting average (>30), boundary % (>50%), and batting position (<4) filters narrowed 200+ players down to **5 realistic opener candidates**, led by Jos Buttler (144.23 SR, 45.00 avg) and Rilee Rossouw (169.88 SR, 35.25 avg).
- The Buttler–Rossouw opening partnership projects a **combined average of ~40 runs at 150+ strike rate**, enough to clear a 180-run team target within the first 4 overs on average.
- Virat Kohli and Suryakumar Yadav emerged as the clear middle-order anchors, with Suryakumar Yadav striking at **~190** and averaging **60**.
- Filtering fast bowlers on economy (<7), bowling strike rate (<16), and dot-ball % (>40%) isolated a 3-bowler core (Sam Curran, Anrich Nortje, Shaheen Shah Afridi) with a **combined economy of ~6 runs/over** and a wicket roughly every 11–12 balls.
- Swapping the No. 6 all-rounder from Hardik Pandya to Marcus Stoinis improved team batting average from **37.76 to 39.6** and strike rate from **151 to 154.4**, demonstrating the dashboard's what-if comparison capability.
- Star player Mitchell Starc was correctly excluded by the model — his economy (8.5), bowling average (34), and strike rate (24) all fell outside the fast-bowler threshold, and he played only 3 of the required 4 qualifying innings.

## ✅ Business Recommendations
- Use role-specific statistical thresholds (not reputation alone) as the first filter in any player shortlisting process.
- Evaluate opening and middle-order pairs on **combined/partnership performance**, not just individual stats, before finalizing a batting order.
- For all-rounder slots, weight the decision by team composition needs (e.g., prioritize batting strike rate when the bowling attack is already strong).
- Re-run the filter criteria per match conditions (e.g., relax the fast-bowler threshold to include a specialist spinner on turning pitches).

## 📈 KPI Impact
| KPI | Before Filtering | After Data-Driven Selection |
|---|---|---|
| Team Batting Average | Not defined | 39.6 |
| Team Strike Rate | Not defined | 154.4 |
| Bowling Economy (Top 3 pace) | Not defined | ~6.0 runs/over |
| Bowling Strike Rate (Top 3 pace) | Not defined | 1 wicket / 11–12 balls |

## 🚀 Business Impact
Replaced a subjective, reputation-driven selection process with a **repeatable, criteria-based decision framework** — reducing selection bias and giving decision-makers (selectors/analysts) an interactive tool to test alternate combinations (e.g., Stoinis vs. Maxwell vs. Pandya) and immediately see the projected impact on team batting average and strike rate before locking in a final XI.

## 🖼 Dashboard Preview

**Power Hitters / Openers Page** — role-based filtering with trend lines and a Strike Rate vs. Batting Average scatter plot for quick comparison.

<img width="1325" height="745" alt="image" src="https://github.com/user-attachments/assets/9c06b825-3c4b-4109-8afe-751e0178b3f5" />


*(Additional pages — Anchors, Finishers, All-Rounders, Specialist Fast Bowlers, Final XI

<img width="1331" height="745" alt="image" src="https://github.com/user-attachments/assets/031c6017-6085-40b0-94ff-8388ab0a692f" />


## ▶️ How to Run
1. Clone this repository
   ```bash
   git clone https://github.com/Sahajahanur/<repo-name>.git
   ```
2. Install Python dependencies
   ```bash
   pip install pandas
   ```
3. Run the data cleaning notebook: `notebooks/01_data_cleaning.ipynb` (converts raw JSON → clean CSVs in `data/processed/`)
4. Open `dashboards/T20_Best11.pbix` in Power BI Desktop
5. In Power Query, point the folder source to your local `data/processed/` path and click **Refresh**

## 🔮 Future Work
- Automate tooltip context (e.g., show "vs Pakistan" instead of "IND vs Pakistan" for home-team players)
- Add a custom color theme and refreshed visual design
- Extend the model with additional insight pages (e.g., powerplay-specific and death-overs-specific filtering)
- Incorporate opposition-strength data once available, to simulate matchup-specific team selection

## 👤 Author & Contact
**Sahajahanur Rahman Laskar**
Data Analyst Intern @ AtliQ Technologies
📧 connectingsrl@gmail.com
🔗 [GitHub](https://github.com/Sahajahanur)
