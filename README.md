# QDLM-code


## 1. Environment

Python 3 with: `numpy`, `pandas`, `scipy`, `scikit-learn`, `matplotlib`,
`seaborn`, `openpyxl` (reads `.xlsx`), `torch` (only for the
`sec6_3_benchmark_comparison` cores, GPU optional).

## 2. How to run

Toy-simulation scripts (all folders directly below the repo root) follow one
convention: **run the script from its own folder**.  Inside the scripts,

* `os.path.dirname(os.getcwd())` then equals the repo root, so
  `.../Result_data/...` (input caches) and `.../Result_figure/<section>/`
  (figure output) resolve automatically;
* each such script inserts the **repo root** into `sys.path` itself and imports
  the shared libraries as packages, e.g. `from common.Function_same_block import ...`
  (the `common/__init__.py` marker is included), so imports resolve without any
  setup — do not call the library files without the `common.` prefix.

Real-data projects (`sec7_1_warfarin/`, `sec7_1_warfarin_clinical/`,
`sec7_2_labor_stage/stage{1,2}/`) keep their original in-project convention:

* figure/preprocess scripts at the project top level: run from the project
  folder (paths use `os.getcwd()` or the script's own location);
* `compute/` scripts: run from the `compute/` folder, so
  `os.path.dirname(os.getcwd())` is the project root; they add the project
  root (where `Function_same_block_warfarin*.py` lives) to `sys.path`.

Dimension/party-count switches via environment variables:

* `QDLM_DIM` (1 or 5, default 5): `sec6_2_privacy_MIA/Fig5a_MIA_attack_classifiers.py`,
  `sec6_2_privacy_MIA/compute_MIA_LAR_20trial.py`,
  `appendix_C4_interpretability/FigAppC4b_ALG.py` and `FigAppC4c_SAD.py`,
  `sec6_3_benchmark_comparison/FigAppC4a_CAI_bars.py` (via `QDLAR_DIM`),
  `sec6_3_benchmark_comparison/Fig7_pareto_1x3.py` (CLI arg or `QDLAR_DIM`).
* `QDLM_M` (number of parties, default 10, multiple of 5 in [5,350]):
  `sec6_2/compute_MIA_LAR_20trial.py`.  The paper used M = 5,10,...,100 with
  DIM = 1 and 5.

  