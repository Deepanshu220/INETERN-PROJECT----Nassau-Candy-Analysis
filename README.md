# ⚡ Nassau Candy Profitability & Margin Performance Analysis

An interactive BI dashboard analyzing product-line profitability, margin efficiency, and concentration risk for Nassau Candy Distributor, built with Python, Pandas, Streamlit, and Plotly.

**Live dashboard:** https://perfomanceanalysis.streamlit.app/

## The Problem

Sales volume doesn't equal profitability. Nassau Candy's product catalog spans multiple divisions, but raw revenue numbers alone don't show which products are actually generating profit versus which are consuming margin. I wanted to find out where the real profit concentration was, and how much risk that concentration created.

## What I Found

Working through the full transaction dataset (149K+ records), a clear pattern emerged: **profit is almost entirely concentrated in a single division.** Five products — all from the Chocolate division (the Wonka Bar line) — drive **95.2% of total gross profit** (₹35,912 of ₹37,724), while the remaining products across the Sugar and Other divisions contribute less than 5% combined.

The concentration goes deeper than that at the individual product level: **"Wonka Bar - Scrumdiddlyumptious" alone accounts for ~20.9% of total gross profit** — the single largest contributor in the entire catalog. That's a meaningful dependency risk for the business: if that one product line underperforms (pricing pressure, supply issue, demand shift), a fifth of total profit is exposed.

This is the core insight the dashboard is built to surface — not just "what sold," but where the business is structurally dependent on a small number of SKUs. The division-level view confirms it independently: Chocolate generates ₹35,912 of the company's ₹37,724 total gross profit, despite being just one of three divisions in the catalog — Sugar and Other combined contribute the rest.

## A Real Technical Problem I Ran Into

Once I had the profit-contribution numbers per product, the natural next step was a bar chart. But the data itself made that chart unreadable: the 5 chocolate products had profit values in the thousands, while most of the other 10 products contributed less than 1% each. Plotted directly, the chart was 5 tall bars and a row of visually meaningless slivers — the long tail was there, but you couldn't read anything from it.

The fix: instead of plotting every product individually, I bucketed any product contributing **less than 1% of total profit** into a single "Other" category, aggregated together, while keeping every product above that threshold visible on its own. This kept the chart honest (nothing is hidden — the "Other" bucket is labeled and its total is shown) while making the actual concentration pattern legible at a glance. It's a small decision, but it's the difference between a chart that looks impressive and a chart that a stakeholder can actually read a decision from.

## Core Analytical Areas

- **Product Profitability** — gross profit ranking, margin tracking, revenue-vs-profit comparison, high-revenue/low-margin detection
- **Division Performance** — division-level margin benchmarking, revenue-profit imbalance
- **Cost vs. Margin Diagnostics** — cost-heavy product identification, pricing inefficiency detection
- **Profit Concentration (Pareto)** — 80/20 contribution analysis, dependency risk detection

## Key KPIs

| KPI | Definition |
|---|---|
| Gross Margin % | Gross Profit ÷ Sales |
| Profit per Unit | Gross Profit ÷ Units |
| Revenue Contribution | Product Sales ÷ Total Sales |
| Profit Contribution | Product Profit ÷ Total Profit |
| Margin Volatility | Margin fluctuation over time |

## Tech Stack

| Category | Tools |
|---|---|
| Language | ![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white) |
| Dashboard | ![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat&logo=streamlit&logoColor=white) |
| Data Processing | ![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white) ![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white) |
| Visualization | ![Plotly](https://img.shields.io/badge/Plotly-3F4F75?style=flat&logo=plotly&logoColor=white) ![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat&logo=python&logoColor=white) |
| Deployment | ![Streamlit Cloud](https://img.shields.io/badge/Streamlit_Cloud-FF4B4B?style=flat&logo=streamlit&logoColor=white) |

## Dashboard Features

- Interactive filtering (date range, division, product search, margin threshold)
- Treemaps, scatter plots, Pareto charts, KPI cards, margin trend views
- Responsive layout with a mobile-friendly sidebar mode


## Run It Locally

```bash
git clone https://github.com/Deepanshu220/INETERN-PROJECT----Nassau-Candy-Analysis.git
cd Nassau-Candy-Analysis-v2
pip install -r requirements.txt
streamlit run dashboard.py
```

## What I'd Do Differently

Given more time, I'd add a time-series view of the concentration ratio itself — right now the dashboard shows *current* dependency risk, but not whether that risk is growing or shrinking over time. That would turn this from a snapshot into an early-warning signal.
