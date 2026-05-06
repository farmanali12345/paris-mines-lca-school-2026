# INSTRUCTIONS BEFORE ARRIVAL

Please complete these steps before the course starts.
The goal is to spend Day 1 learning, not debugging installations.

If you get stuck, contact:
`romain.sacchi@psi.ch`

## Minimum hardware

- Minimum: `8 GB` RAM
- Preferred: `16 GB` RAM

## Before you start

- A stable internet connection is needed to install Git, Miniforge or Python 3.11, and the packages in the `lca-course` environment.
- You need valid `ecoinvent` credentials for the Day 2 import and the Day 3 `premise` work.
- The BAFU workbook used in Day 1 is already bundled at `data/lci-bafu.xlsx`.
- The course `premise` IAM decryption key is `tUePmX_S5B8ieZkkM7WUU2CnO8SmShwmAeWK9x2rTFo=`.
- You will create a repo-root `.env` file later with `IAM_FILES_KEY`, `ECOINVENT_USERNAME`, and `ECOINVENT_PASSWORD`.

## What these tools are for

- `Git`: downloads and updates this course repository.
- `Miniforge` / `conda`: installs Python packages in an isolated environment. This is the recommended route.
- `venv` / `pip`: standard Python environment tools. Use this alternate route if your institution does not allow conda or Miniforge.
- `Jupyter Lab`: runs the tutorial notebooks.
- `brightway`: is the main Python framework used in the course for LCA modeling and calculation.
- `Activity Browser`: is a graphical user interface for `brightway`, installed in a separate environment for the GUI sessions.
- `premise`: generates prospective LCI databases from IAM scenarios.
- `edges`: runs exchange-based and regionalized LCIA workflows.
- `trails`: supports the optional dynamic and temporal LCA examples.

## If you are new to Python

If you are completely new to Python, we recommend spending a few hours on a beginner tutorial before the course.
We suggest the University of Helsinki's online tutorial, which requires no installation:

- https://programming-25.mooc.fi/part-1/1-getting-started

For this course, the `Introduction to Programming` section is sufficient.
You do not need to complete the `Advanced Course in Programming` section.

## 1) Install Git and a Python environment tool

Recommended route:
- Git: https://git-scm.com/downloads
- Miniforge: https://github.com/conda-forge/miniforge/releases/latest

Mac example for Git:

```bash
brew install git
```

### Miniforge installation

Mac users:
- Open `Terminal`
- Download and run the official installer for your Mac architecture:

```bash
curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-$(uname -m).sh"
bash Miniforge3-MacOSX-$(uname -m).sh
```

- Accept the prompt to initialize `conda` for your shell.

Windows users:
- Download `Miniforge3-Windows-x86_64.exe`
- Run the installer and keep the Start Menu shortcuts enabled.
- After installation, open the **Miniforge Prompt** from the Start Menu.
- If possible, install Miniforge in a path without spaces or special characters.

Check that both tools are available:

```bash
git --version
conda --version
```

### If you cannot use conda or Miniforge

Install Git and Python `3.11` instead:
- Git: https://git-scm.com/downloads
- Python: https://www.python.org/downloads/

During Python installation on Windows, enable **Add python.exe to PATH** if your institution allows it.

Check that both tools are available:

```bash
git --version
python --version
```

On Windows, if `python --version` does not show Python 3.11, try:

```bash
py -3.11 --version
```

## 2) Clone this repository

You can use GitHub Desktop or the terminal. Terminal example:

```bash
mkdir GitHub
cd GitHub
git clone https://github.com/romainsacchi/paris-mines-lca-school-2026.git
cd paris-mines-lca-school-2026
```

## 3) Create the course environment (`lca-course`)

### Recommended route: Miniforge / conda

From the repository root:

```bash
cd envs
```

Choose one command:

- macOS Apple Silicon:

```bash
conda env create -f lca_course_osxARM.yaml
```

- Windows:

```bash
conda env create -f lca_course_win64.yaml
```

Then verify:

```bash
conda env list
```

You should see `lca-course` in the list.

### Alternate route: venv / pip

Use this route only if your institution does not allow conda or Miniforge.
The course notebooks should work with this environment, but some optimized sparse solvers are easier to install with conda.
If a solver warning appears during `brightway` calculations, continue unless a later cell actually fails.

From the repository root:

macOS or Linux:

```bash
python3.11 -m venv .venv-lca-course
source .venv-lca-course/bin/activate
python -m pip install --upgrade "pip<26" "setuptools<81" wheel
python -m pip install -r envs/requirements_venv.txt
python -m ipykernel install --user --name lca-course --display-name "Python (lca-course)"
```

Windows PowerShell:

```powershell
py -3.11 -m venv .venv-lca-course
.\.venv-lca-course\Scripts\Activate.ps1
python -m pip install --upgrade "pip<26" "setuptools<81" wheel
python -m pip install -r envs\requirements_venv.txt
python -m ipykernel install --user --name lca-course --display-name "Python (lca-course)"
```

If PowerShell blocks the activation script, run this in the same PowerShell window and activate again:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

The venv requirements include the optional Day 4 `trails` package and the visualization packages installed from GitHub.
If this GitHub install is blocked by your institution, send the error log before the course.

## 4) Optional: save your environment recipe

Use this if you want to save a reproducible recipe for your current environment.
This is an environment recipe, not a `conda-build` package recipe.
Run these commands from the repository root.
If you are still in `envs/`, run `cd ..` first.

### Conda environment YAML

Activate the environment first:

```bash
conda activate lca-course
```

For a portable recipe with only the packages you explicitly installed:

macOS or Linux:

```bash
conda env export --from-history | grep -v "^prefix:" > envs/lca_course_from_history.yaml
```

Windows PowerShell:

```powershell
conda env export --from-history | Where-Object { $_ -notmatch "^prefix:" } | Set-Content -Encoding utf8 envs\lca_course_from_history.yaml
```

For a more complete snapshot of the solved environment:

macOS or Linux:

```bash
conda env export --no-builds | grep -v "^prefix:" > envs/lca_course_full_export.yaml
```

Windows PowerShell:

```powershell
conda env export --no-builds | Where-Object { $_ -notmatch "^prefix:" } | Set-Content -Encoding utf8 envs\lca_course_full_export.yaml
```

Use `lca_course_from_history.yaml` when sharing a clean recipe with another student.
Use `lca_course_full_export.yaml` when you need to reproduce the exact package versions from your own machine.

To recreate the environment later:

```bash
conda env create -f envs/lca_course_from_history.yaml
```

### venv / pip requirements file

Activate the venv first.

macOS or Linux:

```bash
source .venv-lca-course/bin/activate
python -m pip freeze > envs/requirements_lca_course_local.txt
```

Windows PowerShell:

```powershell
.\.venv-lca-course\Scripts\Activate.ps1
python -m pip freeze > envs\requirements_lca_course_local.txt
```

To recreate the venv later:

macOS or Linux:

```bash
python3.11 -m venv .venv-lca-course-recreated
source .venv-lca-course-recreated/bin/activate
python -m pip install --upgrade "pip<26" "setuptools<81" wheel
python -m pip install -r envs/requirements_lca_course_local.txt
```

Windows PowerShell:

```powershell
py -3.11 -m venv .venv-lca-course-recreated
.\.venv-lca-course-recreated\Scripts\Activate.ps1
python -m pip install --upgrade "pip<26" "setuptools<81" wheel
python -m pip install -r envs\requirements_lca_course_local.txt
```

For course maintenance, update the official files in `envs/` deliberately rather than overwriting them with a personal export.

## 5) Install the Activity Browser

Please install the beta version of the AB, following the official installation guide here:
https://lca-activitybrowser.github.io/activity-browser/getting-started/installation.html

This will create a separate environment called `ab_beta` or `.venv-ab-beta`.
For this course we recommend installing Activity Browser in a separate environment from the notebooks.

### Miniforge / conda route

Create the `ab_beta` environment:

```bash
conda create -n ab_beta -c conda-forge lca::activity-browser
conda activate ab_beta
python -m pip install "PySide6==6.9.3"
```

Start the AB:

```bash 
activity-browser
```

Close the AB and type 
```bash 
conda deactivate
``` 
to deactivate the environment. Alternatively, you can keep the AB open and open another terminal to continue.

### venv / pip route

Use this route if you cannot use conda or Miniforge.

macOS or Linux:

```bash
python3.11 -m venv .venv-ab-beta
source .venv-ab-beta/bin/activate
python -m pip install --upgrade "pip<26" "setuptools<81" wheel
python -m pip install -r envs/requirements_activity_browser_venv.txt
activity-browser
deactivate
```

Windows PowerShell:

```powershell
py -3.11 -m venv .venv-ab-beta
.\.venv-ab-beta\Scripts\Activate.ps1
python -m pip install --upgrade "pip<26" "setuptools<81" wheel
python -m pip install -r envs\requirements_activity_browser_venv.txt
activity-browser
deactivate
```
    
## 6) Activate `lca-course`

Activate in the same shell.

Miniforge / conda:

```bash
conda activate lca-course
```

venv / pip on macOS or Linux:

```bash
source .venv-lca-course/bin/activate
```

venv / pip on Windows PowerShell:

```powershell
.\.venv-lca-course\Scripts\Activate.ps1
```

## 7) Create a repo-root `.env` file

If you are still in `envs/`, go back to the repository root first.

Create a file named `.env` in the repository root with:

```bash
IAM_FILES_KEY=tUePmX_S5B8ieZkkM7WUU2CnO8SmShwmAeWK9x2rTFo=
ECOINVENT_USERNAME=<your ecoinvent username>
ECOINVENT_PASSWORD=<your ecoinvent password>
```

You can also start from `.env.example`.

The Day 2, Day 3, and optional Day 4 notebooks load this file automatically with `python-dotenv`.
The `.env` file is ignored by Git and should stay local.

## 8) Run quick import checks

Still in the activated `lca-course` environment:

```bash
python --version
python -c "import bw2data, bw2calc, bw2io, premise, edges; print('Core imports: OK')"
```

### Sparse solver warning

On Apple Silicon, `bw2calc` may print a warning about missing `scikit-umfpack`.
In a venv/pip setup, you may also see a warning about missing optional optimized solvers.
These warnings usually mean calculations may use a slower fallback solver.

If this happens in the conda environment on Apple Silicon, run:

```bash
conda activate lca-course
conda install "setuptools<81"
```

Then verify:

```bash
python -c "import scikits.umfpack; print('UMFPACK import: OK')"
```

If the environment is still inconsistent, recreate it from the YAML file.
For venv/pip users, do not spend time manually compiling `scikit-umfpack` before the course unless your institution already provides the needed system libraries.

## 9) Confirm the bundled BAFU workbook is present

From the repository root:

```bash
ls data/lci-bafu.xlsx
```

If the file exists, you do not need any separate BAFU download before the course.

## 10) Start Jupyter Lab and run the setup notebook

From the repository root:

```bash
# Activate lca-course first: conda activate lca-course, or activate .venv-lca-course.
jupyter lab
```

Then open:
- `tutorials/00_SETUP/00 - Setup and First Checks.ipynb`

## 11) Before the course starts

Please complete:
- [READING_MATERIAL.md](READING_MATERIAL.md)
- [tutorials/00_SETUP/00 - Setup and First Checks.ipynb](tutorials/00_SETUP/00%20-%20Setup%20and%20First%20Checks.ipynb)

Keep the same `lca-course` environment for the full course.
Use `paris-lca-course-2026` for the Day 1 and Day 2 Brightway notebooks.
The Day 3 `premise` notebooks create or select a separate project, `paris-lca-course-2026-premise`, with `ecoinvent-3.12-cutoff`.

## 12) Updating the repository during the course

The instructors may add or update files during the course.
When this happens, you may be asked to run:

```bash
git pull
```

This usually works if you have not modified the same files.
If you have worked in a notebook that was also updated by the instructors, Git may refuse to pull or may report a conflict.
This is normal: Git is protecting your local work.

Before pulling, check whether you have local changes:

```bash
git status --short
```

If the command prints nothing, your repository is clean and you can run:

```bash
git pull
```

If it lists modified notebooks or other files, preserve your work first.
The safest course workflow is:

1. Save and close the notebook in Jupyter.
2. Copy your edited notebook outside this repository, for example to a folder named `paris-lca-course-my-work`.
3. Let Git restore the original course notebook.
4. Pull the instructor updates.
5. Open both the updated course notebook and your saved copy if you need to transfer answers or notes.

Example, replacing the path with the notebook shown by `git status`:

```bash
mkdir -p ../paris-lca-course-my-work
cp "tutorials/DAY 2 - Brightway and Activity Browser Part I/D2-01 ecoinvent import and Brightway recap.ipynb" ../paris-lca-course-my-work/
git restore "tutorials/DAY 2 - Brightway and Activity Browser Part I/D2-01 ecoinvent import and Brightway recap.ipynb"
git pull
```

On Windows, if `cp` is not available in your terminal, use File Explorer to copy the notebook outside the repository before running `git restore`.
Repeat the `cp` and `git restore` commands for each modified course notebook that blocks the pull.
Only use `git restore` after you have made a backup copy.

If you prefer to keep all local changes inside Git, you can also use a stash:

```bash
git stash push -m "my course work before update"
git pull
git stash pop
```

This preserves your changes, but `git stash pop` can still create notebook conflicts if the same notebook changed both locally and upstream.
If that happens, ask an instructor before trying to edit the notebook file manually.
Notebook files are JSON files, and manual conflict resolution is easy to get wrong.

If you are already in the middle of a failed pull, stop and ask for help.
In many cases the instructor can help you return to the pre-pull state with one of:

```bash
git merge --abort
git rebase --abort
```

Do not run `git reset --hard` or discard changes in GitHub Desktop unless you are certain your notebook work has been backed up elsewhere.
