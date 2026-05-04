# DAY 2 - Brightway and Activity Browser Part I

Run these materials after completing Day 1 in the same `lca-course` environment and Brightway project.

Before starting Day 2, make sure that:
- the project `paris-lca-course-2026` is still available
- the BAFU database imported on Day 1 is still present
- the repo-root `.env` file contains `ECOINVENT_USERNAME` and `ECOINVENT_PASSWORD`

Core material:

1. `D2-01 ecoinvent import and Brightway recap.ipynb`
2. `D2-02 Foreground and background uncertainty split.ipynb`
3. `D2-03 Database-level parameters and Monte Carlo.ipynb`
4. `AB-01 Activity Browser Part I handout.md`

The first notebook imports `ecoinvent 3.12 cutoff` into the same project, loading credentials from the repo-root `.env` file when available.
The second notebook compares carbon-fiber Monte Carlo results with foreground-plus-background uncertainty and foreground-only uncertainty.
The third notebook moves the carbon-fiber parameter example from activity-level parameters to database-level parameters and injects sampled parameter uncertainty into Monte Carlo.
The handout then uses the shared project state in Activity Browser for parameterisation, Monte Carlo, and GSA.
