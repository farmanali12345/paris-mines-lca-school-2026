# DAY 3 - Premise and Activity Browser Part II

Run these materials after completing Day 2 in the same `lca-course` environment.

Before starting Day 3, make sure that:
- the separate Day 3 Brightway project is named `paris-lca-course-2026-premise`
- `paris-lca-course-2026-premise` contains `ecoinvent-3.12-cutoff`
- you can import `ecoinvent 3.12 cutoff` either with `bw2io.import_ecoinvent_release()` or from Activity Browser if the database is not present yet
- the repo-root `.env` file is present, ideally with `IAM_FILES_KEY`, `ECOINVENT_USERNAME`, and `ECOINVENT_PASSWORD`
- you are ready to generate and compare REMIND-EU scenario databases

Core material:

1. `D3-01 Generating prospective databases with premise.ipynb`
2. `paris_premise_intro_06_05_2026.pdf`
3. `D3-02 Inspecting and comparing premise outputs in Brightway.ipynb`
4. `AB-02 Activity Browser Part II handout.md`

Optional extension:

- `D3-04 Optional custom scenarios with premise - RTE FE2050.ipynb`: clone the RTE FE2050 custom-scenario datapackage outside this course repository and run a `premise` build that combines French RTE scenarios with an IAM scenario.

The Day 3 sequence starts by creating or selecting the dedicated `premise` project in `D3-01`, confirming the `ecoinvent` import, and launching the scenario databases.
While those long-running jobs execute, the one-hour introduction lecture covers IAMs, scenarios, and the prospective LCA workflow.
The group then returns to `D3-01` for checks and export before moving into `D3-02` and the Activity Browser handout.
The Premise notebooks load the repo-root `.env` file automatically with `python-dotenv`, and still fall back to the embedded course key if `IAM_FILES_KEY` is absent.
The Activity Browser handout then focuses on scenario, year, and technology comparisons in the GUI.
