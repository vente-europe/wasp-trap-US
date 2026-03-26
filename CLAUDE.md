# Dashboard — WASP US

> **Living document** — Update after every bug fix or new pattern found. No permission needed for additions. Ask before removing.

---

## Language
All content in this project (visualizations, labels, comments, documentation) must be in **English**.

---

## Project Overview

- **Purpose:** Amazon US market analysis dashboard — WASP category
- **Active file:** `index.html` (dashboard root)
- **Git repo:** root of this folder
- **Tech stack:** HTML + vanilla JS, Chart.js 4.4.0 + chartjs-plugin-datalabels 2.2.0, no build step
- **Based on:** `_template/` (adapt as needed for WASP-specific dimensions)
- **Data source:** `Data/x-ray/WASP-US-x-ray.csv`

---

## Tab Structure

| Tab | Content |
|-----|---------|
| 1 — Segments Analysis | Total KPIs, segment KPI cards, market share pies, segment summary table, brand % unit share, monthly seasonality index |
| 2 — Market Structure | Fruit fly template data (placeholder) |
| 3 — Reviews | Fruit fly template data (placeholder) |

## Key Data Dimensions

| Dimension | Values |
|-----------|--------|
| Segment | Lure (22 ASINs), Sticky (11 ASINs), Decoy Nest (4 ASINs), Electric (121 ASINs) |
| Brands | 72 total. Top Lure: RESCUE!, Spectracide, Stingmon, TriskelBlue, outtkitywi, X-octenol, Jiermadun |
| Season | Peak: Aug (index 2.43×), Trough: Jan (0.16×), Ratio: 15.5× |
| Market | 4.68M units · $166.6M revenue (12M) — Electric dominates at 92.6% rev share |

---

## Data Sources

| Source | What it contains | Use for |
|--------|-----------------|---------|
| `Data/x-ray/` CSV | **Last 30-day snapshot** — ALL columns reflect the 30-day window at export time | ASIN metadata only: Price, Brand, Title, Rating, Reviews, BSR, Age |
| `Data/sales-units/[ASIN]-sales-3y.csv` | **Full historical daily units** with dates — `Sales` column = units sold that day | 12M sales calculations |

## Data Convention — 12M

**All sales and revenue = 12-month totals.** Every chart title includes "(12M)".

- **12M Units** = sum of `Sales` column for dates in the last 12M window (from export date)
- **12M Revenue** = 12M units × ASIN listed price from X-Ray
- **Never use X-Ray "ASIN Sales" or "ASIN Revenue" for 12M** — both are 30-day figures
- New ASINs may not have full 12M of history in sales files — sum what's available, that IS their 12M

---

## Source Data

| Path | Description |
|------|-------------|
| `Data/sales-units/` | Per-ASIN sales CSVs (H10 Xray) — not git tracked |
| `Data/x-ray/` | Full X-Ray export (CSV) — not git tracked |
| `Data/reviews/` | Amazon review scraper JSONs — not git tracked |

---

## Known Bugs & Fixes

- Electric (ZEVO) has no sales data for Mar–Jun 2025 in its CSV → seasonality index shows 0.0 for those months. This is actual data, not a bug.
- B0C5F7WFFY (RESCUE! Carpenter Bee TrapStik 4-pack, Sticky) has no 3y sales CSV → negligible impact (~42 units/mo X-Ray).

---

## Chart Insertion Rule

**When adding a new chart to any existing section:**
- **NEVER remove or replace existing charts or content**
- **ALWAYS insert the new chart below existing charts and push everything else down**
- This applies even if the user says "add here" — preserve all existing elements, only insert

## Self-Update Rules

**Update this file when:**
- Dashboard is built → add active file path and tab structure
- A bug is found and fixed → add to Known Bugs & Fixes
- New data is added → update Source Data table
- Key dimensions confirmed → fill in Key Data Dimensions

**Ask before:**
- Removing existing entries
- Changing core structure
