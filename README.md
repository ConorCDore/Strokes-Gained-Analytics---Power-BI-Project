# Strokes-Gained-Analytics---Power-BI-Project

## Overview

This project analyzes professional golf performance using **Strokes Gained** metrics to understand:

1. How player performance varies across skill domains
2. How overall performance translates into consistency (making cuts)
3. Which specific skills are most associated with cut percentage

The goal was to produce a **portfolio‑grade BI project** demonstrating clean data modeling, defensible assumptions, and interactive analysis using **SQL + Power BI**.

Target audience: Business Intelligence / Analytics roles (sports, media, or general analytics).

---

## Key Questions

* Who are the top performers by average Strokes Gained?
* How strong is the relationship between average performance and cut percentage?
* Which Strokes Gained components (Off‑the‑Tee, Approach, Around‑the‑Green, Putting) are most associated with making cuts?
* How do results change as minimum sample size increases?

---

## Data Sources

* **Round‑level PGA Tour data** (player, event, finish outcomes)
* **Strokes Gained components**:

  * Off‑the‑Tee (OTT)
  * Approach (APP)
  * Around‑the‑Green (ARG)
  * Putting (PUTT)
  * Total SG

All metrics are evaluated **per round** and aggregated at the player level.

---

## Data Preparation & Modeling

### Data Cleaning (Power Query / SQL)

* Converted all Strokes Gained fields from text to numeric
* Replaced NA / error values with nulls
* Standardized finish outcomes:

  * `CUT`, `MDF` → Did not make cut
  * `WD`, `DQ`, missing → Excluded from cut opportunities
  * Placements (e.g. T28) → Made cut

### Fact Table Design

A **denormalized fact table** was used for BI performance and clarity:

* `event_results` (fact)

  * Player, event, SG components, finish status
* Dimension tables:

  * `players`
  * `events`

Relationships:

* Players → Event Results (1‑to‑many)
* Events → Event Results (1‑to‑many)

To avoid ambiguity, single-direction was required.

---

## Core Metrics (DAX)

### Performance

* Average SG Total
* Average SG by skill bucket (OTT, APP, ARG, PUTT)
* Events Played

### Cut Performance

* Cuts Made
* Cut Opportunities
* Cut Percentage = Cuts Made / Cut Opportunities

### Sample Control

A **What‑If parameter** enforces a minimum event threshold:

* Users select a minimum number of events
* Players qualify only if they meet or exceed this threshold
* Qualification is applied via measures to preserve model integrity and optionality

---

## Dashboard Pages

### Page 1 — Player SG Leaderboard

**Purpose:** Establish baseline performance rankings

Features:

* Player leaderboard sorted by Avg SG Total
* Supporting SG buckets (T2G, Putting)
* Minimum event slider to reduce small‑sample noise
* KPI cards showing:

  * Number of qualified players
  * Average player SG (qualified)
  * Top‑10 average SG (qualified)

Insight:

> Elite performers separate meaningfully from the field even as sample requirements increase.
> Average player SG (Qualified) increases as minimum event threshold is raised
---

### Page 2 — Cut Performance

**Purpose:** Link performance to consistency

Features:

* Table of Cut %, Cuts Made, and Opportunities
* Scatter plot: Cut % vs Avg SG Total
* Skill mix bar chart showing SG component profiles

Insight:

> Higher average Strokes Gained strongly correlates with higher cut percentage, indicating performance translates to consistency over large samples.

---

### Page 3 — SG Components vs Cut Percentage

**Purpose:** Identify which skills matter most for consistency

Features:

* Component selector (OTT, APP, ARG, PUTT)
* Scatter plot: Selected SG component vs Cut %
* Dynamic KPI cards:

  * Correlation (r)
  * R² (relationship strength)
  * Slope (effect size per +1 SG)

Insight:

> Different skills contribute differently to consistency; relationship strength and effect size vary meaningfully by component.
> Across the evaluated skills, SG Approach (iron play) shows the strongest relationship with cut consistency.

---

## Analytical Decisions & Assumptions

* MDF treated as not making a full cut
* Withdrawals and disqualifications excluded from cut opportunities
* Minimum sample enforced dynamically rather than via hard filters
* Player‑level aggregation used to study consistency across careers

These choices prioritize **interpretability and analytical honesty** over maximizing headline numbers.

---

## Tools & Technologies

* **PostgreSQL** – data storage and validation
* **Power BI** – data modeling, DAX, and visualization
* **Power Query** – data cleaning and transformation
* **DAX** – custom measures, correlation, regression metrics

---

## Skills Demonstrated

* Data modeling (fact/dimension design)
* SQL data ingestion and validation
* Advanced DAX (filters, TOPN, correlation, regression logic)
* Interactive dashboard design
* Statistical reasoning applied in a BI context
* Clear communication of assumptions and insights

---

## How to Use

1. Adjust **Min Events Played** slider to control sample size
2. Explore leaderboards to identify top performers
3. Examine how performance translates to cut consistency
4. Switch SG components to compare skill‑specific relationships

---

## Final Notes

This project was designed to mirror real‑world BI workflows:

* Clear problem framing
* Explicit assumptions
* Reproducible metrics
* Insight‑driven visuals

It is intended as a demonstration of analytical thinking and BI craftsmanship rather than a predictive model.
