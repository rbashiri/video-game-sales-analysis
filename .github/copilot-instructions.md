# Copilot / AI Agent Instructions — video-game-sales-analysis

Purpose
- Help maintainers run and extend the single-analysis Jupyter notebook and locate the dataset used for the analysis.

Quick facts
- Repo type: small exploratory data analysis (EDA) in a single Jupyter notebook: `video_game_analysis.ipynb`.
- Primary data: external CSV referenced in the notebook (not checked into repo). Notebook reads: `C:\Users\robab\OneDrive\2025\Tripleten\Sprint 5\games.csv`.
- Typical libraries used: pandas, numpy, scipy, matplotlib.

How to get started (developer workflow)
- Open `video_game_analysis.ipynb` in VS Code or Jupyter Lab and run the cells interactively.
- Ensure a Python environment with these packages: pandas, numpy, scipy, matplotlib. Example (PowerShell):
  ```powershell
  pip install pandas numpy scipy matplotlib
  ```
- If the notebook errors on the CSV path, search the workspace for `games.csv` or ask the repo owner for the correct dataset path. Do NOT assume the file is present in the repo.

Project-specific patterns and gotchas
- Single-file analysis: The repo contains one notebook and no scripts/tests. Agents should treat changes as exploratory and keep transformations reproducible (prefer creating a small .py script or new notebook rather than editing the original notebook in place when adding functionality).
- Hard-coded external path: The notebook currently loads data from a hard-coded OneDrive path. Example problematic line (cell 1):

  game-sale = pd.read_csv( r"C:\Users\robab\OneDrive\2025\Tripleten\Sprint 5\games.csv")

  Issues to fix if editing: invalid Python identifier (`game-sale`) and fragile absolute path. Use a more robust pattern, for example:

  ```python
  data_path = r"C:\path\to\games.csv"  # update to actual location or make configurable
  games_df = pd.read_csv(data_path)
  ```

- Naming: prefer snake_case (e.g., `games_df`) not hyphens. The notebook currently uses `game-sale` which is a syntax error.
- Imports: notebook imports `math as mt` and `scipy.stats as st` but they are only needed if used later; keep imports minimal when refactoring into scripts.

Integration points and external dependencies
- No external APIs or services are referenced. The only external dependency is the dataset CSV. Confirm where `games.csv` lives (local drive, OneDrive, or a data folder). If adding automation, prefer placing datasets in a `data/` directory and adding a small README entry.

Editing guidance for AI agents
- Non-destructive edits: when adding code, prefer adding new cells or a new file (e.g., `notebooks/analysis_clean.py` or `notebooks/video_game_analysis_clean.ipynb`) rather than mutating the user's original notebook unless requested.
- Reproducibility: make data paths configurable via a top-level variable or environment variable. Example: read from `DATA_PATH` env var with a sensible fallback.
- Minimal examples: when suggesting fixes, include the exact replacement lines and reference the notebook cell (Cell 1) so a human can apply the change.

Files worth inspecting
- `video_game_analysis.ipynb` — the main analysis. Cell 1 imports libraries and attempts to load `games.csv`.
- `README.md` — one-line project description; no further instructions.

When you’re unsure
- If you can’t find `games.csv` in the workspace, ask: “Where should I read the dataset from? Please provide the path or upload `games.csv`.”
- If you plan to refactor the notebook into scripts, indicate which outputs to preserve (plots, summary tables) and offer a small CI-friendly script instead of a large notebook rewrite.

Next steps suggestions for maintainers (optional)
- Add a `requirements.txt` or `environment.yml` listing the packages used by the notebook.
- Add a `data/` folder or a short CONTRIBUTING.md entry explaining where to place the CSV.

If anything above is unclear, tell me which part you want expanded or whether you want me to (a) fix the notebook import line, (b) create a small requirements.txt, or (c) scaffold a script that reproduces the notebook analysis.