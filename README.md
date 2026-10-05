# Three-Cohort iEEG Cross-Frequency Coupling

Analysis code for **Cross-Cohort Agreement of Regional and Peri-Onset
Cross-Frequency Coupling Patterns in Drug-Resistant Epilepsy**.

The repository contains the five CFC estimators, patient-level aggregation,
three-cohort statistics, sensitivity checks and plotting code. One labeled
public-subject example is included. Raw cohort recordings, private clinical
annotations, precomputed paper-result tables and generated reports are not.

## Install And Run

Python **3.9-3.11**, CPU; run from the extracted repository directory:

```bash
python -m venv .venv
.venv\Scripts\python.exe -m pip install -r requirements.txt
.venv\Scripts\python.exe -m pip install -e . --no-deps
.venv\Scripts\python.exe scripts/run_demo.py --six-windows --output outputs/demo
```

On Linux/macOS replace `.venv\Scripts\python.exe` with `.venv/bin/python`.
For later commands, `python` means that environment's interpreter. The demo computes
**7,488 rows**: 4 contacts x 6 windows x 312 features. It uses 20 surrogates for
speed; `--surrogates 1000` selects the paper's count. GPU/PyTorch is optional.

Check the estimators, input selection and CPU demo against its small baseline:

```bash
python scripts/check_installation.py
```

The included signal is already preprocessed. **Do not reference/filter it
again.** Its source, units, contacts and license are in `example/metadata.json`.
This single-subject example tests software, not population-level findings.

## Files

```text
cfc_repro/                 Estimators, preprocessing, statistics and plotting
  core/                    Signal processing and surrogate calculations
  analysis/                Patient aggregation, experiments and sensitivities
scripts/                   Demo, full study, plotting, input preparation, check
example/                   One subject's small signal, metadata and demo baseline
test_reproducibility.py    Scientific and execution regression tests
study.json                 Frozen study settings and inference seeds
public_selection.json      Public recording/contact/window selection, not EEG
requirements.txt           Pinned CPU dependencies
pyproject.toml             Editable installation and CLI registration
REPRODUCE.md               Full commands, input schemas and code-to-paper map
```

`public_selection.json` identifies the exact public subset and stores repeated
contact lists once. It is needed to reproduce which records and contacts were
analyzed; it does not contain signal samples or private Lanzhou annotations.

## Full Study

Public sources: ds003029 **v1.0.3**, ds004100 **v1.1.3**. Download them separately.
Expand the public selection with `python scripts/prepare_inputs.py`. Full
three-cohort inference also requires separately authorized Lanzhou recordings
and annotations. See [REPRODUCE.md](REPRODUCE.md) for the complete procedure.


