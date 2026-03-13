# 6gsmartez_models

Shared model artifacts and notebooks for UPF traffic forecasting using Prophet and XGBoost.

## What this repository contains

- A Prophet workflow that loads a pre-trained serialized bundle and reproduces shared forecasts.
- An XGBoost workflow with two variants:
1. Base time-feature model.
2. Lagged 15-minute model.
- Exported forecast CSV files produced from those shared bundles.

## Quick start

1. Create an environment with `python>=3.9`.
2. Install notebook dependencies:
   - `pandas`
   - `matplotlib`
   - `jupyter`
3. Open and run:
   - `UPF_Phrophetv3.ipynb`
   - `UPF_XGBoostv3.ipynb`
4. Keep each notebook in the same folder as its `.pkl` model bundle.

## Data and outputs overview

- `prophet_shared_forecast.csv`: 5754 rows, columns `ds, yhat, yhat_lower, yhat_upper`, range `2023-09-02 00:00:00` to `2023-10-31 22:30:00`.
- `xgboost_base_shared_forecast.csv`: 2874 rows, columns `ds, y_XGBoost`, range `2023-10-02 00:00:00` to `2023-11-01 00:00:00`.
- `xgboost_lagged_shared_forecast.csv`: 2873 rows, columns `ds, y_XGBoost_lag15`, range `2023-10-02 00:15:00` to `2023-11-01 00:00:00`.
- `xgboost_shared_comparison.csv`: 2873 rows, columns `ds, y_XGBoost, y_XGBoost_lag15`, range `2023-10-02 00:15:00` to `2023-11-01 00:00:00`.

## File-by-file details

Note: this list covers project files and notebook checkpoints. Internal `.git/*` metadata is intentionally excluded.

| Path | Type | Details |
| --- | --- | --- |
| `README.md` | Documentation | Project documentation (this file). |
| `LICENSE` | License | Repository license text. |
| `UPF_Phrophetv3.ipynb` | Notebook | Prophet shared notebook (`11` cells: `2` markdown, `9` code). Loads `upf_prophet_model.pkl`, rebuilds/plots forecast, exports `prophet_shared_forecast.csv`. |
| `upf_prophet_model.pkl` | Model artifact | Serialized Prophet bundle consumed by `UPF_Phrophetv3.ipynb` (includes model, reference forecast, and metadata such as frequency/test rows/future periods). |
| `UPF_XGBoostv3.ipynb` | Notebook | XGBoost shared notebook (`13` cells: `2` markdown, `11` code). Loads `upf_xgboost_models.pkl`, compares base vs lagged forecasts, exports 3 CSV outputs. |
| `upf_xgboost_models.pkl` | Model artifact | Serialized XGBoost bundle used by `UPF_XGBoostv3.ipynb` (contains base and lagged model bundles and shared metadata). |
| `prophet_shared_forecast.csv` | Data output | Prophet forecast export with prediction interval bounds. |
| `xgboost_base_shared_forecast.csv` | Data output | Forecast from base XGBoost model. |
| `xgboost_lagged_shared_forecast.csv` | Data output | Forecast from lagged (15-minute) XGBoost model. |
| `xgboost_shared_comparison.csv` | Data output | Side-by-side base and lagged XGBoost forecasts aligned by timestamp. |
| `.ipynb_checkpoints/UPF_Phrophetv3-checkpoint.ipynb` | Notebook checkpoint | Auto-saved checkpoint for the Prophet notebook (`8` cells: `2` markdown, `6` code). |
| `.ipynb_checkpoints/UPF_XGBoostv3-checkpoint.ipynb` | Notebook checkpoint | Auto-saved checkpoint for the XGBoost notebook (`13` cells: `2` markdown, `11` code). |

## Imported libraries in notebooks

Both notebooks currently import:

- `pickle`
- `pandas`
- `matplotlib.pyplot`
- `pathlib.Path`

## Notes

- The shared workflows are artifact-driven: they load pre-trained bundles instead of retraining from source data.
- Naming is kept as-is from the repository (including `UPF_Phrophetv3.ipynb` filename spelling).


## ACKs
This work was supported by the Spanish Ministry of Economic Affairs and Digital Transformation and the European Union – NextGenerationEU, in the framework of the Recovery Plan, Transformation and Resilience (PRTR) (Call UNICO I+D 5G 2021, ref. numbers TSI-063000-2021-15 – 6GSMART-EZ).