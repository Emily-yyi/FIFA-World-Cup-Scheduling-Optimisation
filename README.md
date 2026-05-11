# FIFA World Cup Scheduling Optimisation

This project builds a three-stage optimisation framework for designing a FIFA World Cup group-stage schedule. The goal is to balance competitive fairness, match popularity, and stadium capacity allocation for a 48-team tournament format.

## Project Overview

The project models tournament scheduling as a prescriptive analytics problem. It uses FIFA ranking points, confederation constraints, spectator-demand proxies, match popularity measures, and stadium capacity data to support scheduling decisions.

The optimisation workflow is divided into three stages:

1. Balanced group formation
2. Group letter assignment based on match popularity
3. Stadium assignment based on row-set popularity and venue capacity

## Business Problem

Large sports tournaments need to satisfy several competing objectives:

- keep groups competitively balanced
- follow draw rules such as pot structure and confederation restrictions
- distribute high-demand matches across the schedule
- assign popular match sets to suitable stadiums with larger capacity

This project demonstrates how mathematical optimisation can support those decisions in a structured and reproducible way.

## Methodology

### Model 1: Balanced Group Formation

The first model assigns 48 teams into 12 groups of four teams. FIFA ranking points are used as a proxy for team strength.

Objective:

- maximise the minimum group strength across all groups

Key constraints:

- each team is assigned to exactly one group
- each group contains four teams
- each group contains one team from each pot
- confederation restrictions are respected

The model is implemented with Pyomo and solved with GLPK.

### Model 2: Group Letter Assignment

The second model assigns the balanced groups to tournament group letters from A to L. Match popularity is estimated using spectator index values for the teams in each match.

Objective:

- balance row-set popularity across the schedule

The model is implemented with Google OR-Tools CP-SAT.

### Model 3: Stadium Assignment

The final model assigns row-sets to stadiums using row-set popularity and stadium capacity.

Objective:

- maximise total spectator exposure

The model is implemented with Pyomo and solved with GLPK.

## Data

The project uses a prepared Excel workbook containing:

- FIFA ranking points and team confederations
- 2026 FIFA World Cup stadium capacity data
- historical attendance and spectator-demand proxies
- group-stage match schedule structure
- intermediate model outputs

Main data file:

```text
data/world_cup_scheduling_data.xlsx
```

## Key Results

- Built a three-stage optimisation pipeline for a 48-team, 12-group tournament structure.
- Generated balanced group allocations with a minimum group strength of 6,341.67 ranking points.
- Assigned group letters to balance match popularity across 16 row-sets.
- Allocated row-sets across 16 stadiums with an optimal spectator exposure objective value of approximately 5.34 million.

## Repository Structure

```text
world-cup-scheduling-optimisation/
├── README.md
├── README.zh-CN.md
├── requirements.txt
├── data/
│   └── world_cup_scheduling_data.xlsx
├── docs/
│   └── project_summary.md
└── notebooks/
    └── world_cup_scheduling_optimisation.ipynb
```

## Tools Used

- Python
- pandas
- Pyomo
- Google OR-Tools CP-SAT
- GLPK
- Excel

## How to Run

Install the required Python packages:

```bash
pip install -r requirements.txt
```

Install GLPK separately if it is not already available on your machine.

Then open and run:

```text
notebooks/world_cup_scheduling_optimisation.ipynb
```

## Portfolio Summary

This project shows the use of optimisation modelling for tournament planning and resource allocation. It combines data preparation, mathematical programming, constraint modelling, and business interpretation in a sports analytics context.
