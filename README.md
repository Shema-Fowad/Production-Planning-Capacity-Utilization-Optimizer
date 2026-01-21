# Production-Planning-Capacity-Utilization-Optimizer
Operations analytics project analyzing production capacity utilization, downtime, bottlenecks, and shift productivity to improve throughput without additional capacity.

## Project Overview
This project focuses on **manufacturing operations analytics**, specifically analyzing **capacity utilization, downtime, bottlenecks, and shift productivity** using a realistic production dataset.

The objective is to answer **plant-level decision questions** such as:
- Are we fully utilizing installed capacity?
- Which production lines are true bottlenecks?
- How does shift-wise performance impact output and cost?
- Can throughput be improved without adding new capacity?

The project emphasizes **execution efficiency over capex**, mirroring how real operations teams work.

---

## Key Business Questions Answered

1. What is the overall capacity utilization of the plant?
2. Which production lines lose the most capacity due to downtime?
3. How does utilization vary by shift (Morning / Evening / Night)?
4. Which shifts are less productive and more expensive per unit?
5. How strongly does downtime impact utilization?
6. What improvement is possible through operational fixes alone?

---

## Dataset Design (Operations Grade)

**Time Period:** Jan–Jun 2024  
**Granularity:** Line × Shift × Day × Product  
**Scale:** ~5,000 production runs

### Tables Used
| Table | Description |
|-----|------------|
| plants | Manufacturing plant master |
| production_lines | Line capacity and constraints |
| shifts | Shift definitions and labor cost |
| products | Product master |
| production_calendar | Working day planning |
| orders | Demand inputs |
| production_runs | Core execution fact table |
| maintenance_logs | Downtime and maintenance events |

All KPIs are **derived**, not stored, following analytics best practices.

---

## Data Modeling Approach
- `production_runs` acts as the **central fact table**
- Strong use of **primary and foreign keys**
- Capacity is based on **rated machine throughput × run hours**
- No pre-aggregated or hard coded KPIs

---

## Analysis Performed

### Step 1: Capacity Utilization Analysis
- Overall, plant-level, line-level, and shift-level utilization
- Monthly utilization trends
- Validation of physical feasibility (no false capacity inflation)

**Key Metric**
Capacity Utilization % = Actual Units / (Rated Capacity × Run Hours)

---

### Step 2: Bottleneck & Downtime Analysis
- Downtime contribution by line
- Downtime as % of available production time
- Planned vs breakdown maintenance
- Quantification of **lost units due to downtime**

This step identifies **true operational constraints**, not surface-level underperformance.

---

### Step 3: Shift Productivity & Labor Efficiency
- Units produced per hour by shift
- Capacity utilization by shift
- Labor cost per unit by shift
- Planned vs actual output consistency

This translates operational inefficiencies directly into **cost impact**.

---

## What-If Scenario: Downtime Reduction
A scenario analysis was conducted assuming a **10% reduction in downtime**:
- Results show potential utilization improvement from ~84% to ~86%
- Gains are concentrated on a few high downtime lines
- Indicates **execution improvements outperform capacity expansion**

---

## Key Insights

- Overall utilization is healthy (~84%) but below best in class levels
- Downtime is the primary constraint, not demand
- Night shift consistently underperforms across months
- A small number of lines drive most capacity loss
- Targeted maintenance and shift improvements offer high ROI

---
## Data Versioning & Realism Roadmap

This project currently uses a **Version 1 (v1) synthetic dataset** designed to represent a **steady-state manufacturing baseline**.

### Version 1 – Baseline Operations Model
The v1 dataset focuses on:
- Correct operational grain (Line × Shift × Day × Product)
- Physically valid capacity logic (rated capacity × run hours)
- Realistic downtime, scrap, and shift structures
- Clean KPI definitions and data modeling

This version intentionally keeps variability controlled to:
- Validate KPI calculations and aggregation logic
- Test SQL queries and Power BI measures
- Establish a stable operational baseline

As a result, some KPIs (e.g., utilization) may appear relatively stable over time.

---

### Planned Enhancements – Version 2 (Roadmap)
The next version of the dataset will introduce additional realism layers commonly observed in real manufacturing environments:

- **Seasonality effects**  
  Peak and slack periods impacting demand, utilization, and downtime

- **Line-specific behavior**  
  Aging equipment, chronic bottlenecks, and differing reliability profiles

- **Shift-level dynamics**  
  Fatigue effects, learning curves, and supervision impact on night shifts

- **Operational shock events**  
  Major breakdowns, maintenance backlogs, or short-term disruptions

These enhancements will allow deeper analysis of:
- Volatility in capacity utilization
- Stress behavior during peak demand
- ROI of targeted downtime reduction strategies

---

### Why This Approach
In real operations analytics projects, datasets evolve iteratively:
1. Establish a stable baseline  
2. Validate logic and KPIs  
3. Introduce complexity and volatility over time  

This repository follows the same progression.


## Tools & Technologies
- **SQL Server** – core analytics & KPI logic
- **Python (pandas, numpy)** – realistic data generation
- **Power BI** – executive operations dashboard
