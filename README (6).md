# Streaming Conformalized EMM

Code for the paper *Streaming Conformalized Exceptional Model Mining: Finding, Monitoring and Repairing
Under-Covered Subgroups in an ICU Sepsis Stream* (2AMM20 Research Topics in Data Mining, TU/e, 2026).

The pipeline trains a classifier on one hospital and runs conformal prediction on a stream of ICU stays that switches
to a second hospital. It finds under-covered subgroups with Conformalized Exceptional Model Mining (beam search with
the coverage gap as quality measure), monitors them with a patient-level CUSUM, and repairs their coverage with
group-conditional online conformal prediction.

## Contents

| Path | What it is |
|---|---|
| `notebooks/01_main_run_logreg_beam.ipynb` | Main experiment (logistic regression, beam search). Its saved outputs are the numbers in the paper; Section 15 draws Figure 1. |
| `notebooks/02_robustness_gradient_boosting.ipynb` | The same code with `MODEL_TYPE = "hgb"` and `SEARCH = "grid"`: the second base model in paper Section 7.5. |

The first cell of each notebook lists which notebook section produces which table of the paper.

## Data

PhysioNet/CinC 2019 sepsis challenge, training sets A and B (40,336 ICU stays from two hospital systems). The data are
public at https://physionet.org/content/challenge-2019/1.0.0/ and are not included in this repository.

- **In Google Colab**, Section 2 of each notebook downloads both training sets into your Google Drive
  (`MyDrive/physionet.org/files/challenge-2019/1.0.0/training`) if they are not there yet. The first download takes a
  while.
- **Elsewhere**, download the two training sets yourself and set `DATA_PATH` in Section 1 (or the environment variable
  `SEPSIS_DATA_PATH`) to the folder that contains `training_setA` and `training_setB`.

## How to run

Open a notebook in Google Colab and use *Runtime → Run all*. The first run installs `river` (for ADWIN) and asks for
one restart. All settings are in Section 1; results are saved as CSV files in `results_v3_<split>_<model>_<search>`
on Drive. For a quick end-to-end check, set `QUICK_TEST = True` in Section 1 (the numbers are then only a smoke test).

Outside Colab you need Python 3 with `numpy`, `pandas`, `scipy`, `scikit-learn`, `matplotlib` and `river`.

## License

The code is released under the MIT License (see `LICENSE`). The PhysioNet data have their own license and are not
redistributed here.
