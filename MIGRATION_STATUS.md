# Migration status

The project source has been extracted from [Unretur/ml-journey/Projects/SupplyGuard](https://github.com/Unretur/ml-journey/tree/main/Projects/SupplyGuard) into this standalone repository. The source repository is unchanged.

## Copied into this repository

- `Data.py`, `features.py`, `train.py`, `evaluate.py`, and `api.py`
- `tests/` API and pipeline tests
- `01_eda.ipynb` exploratory analysis notebook
- `PERFORMANCE_REVIEW.md` and `requirements.txt`
- Standalone GitHub Actions workflow at `.github/workflows/tests.yml`
- Legacy binary model files `encoder.joblib` and `final_model.joblib`
- MLflow tracking database `mlflow.db`

## Still only in the source repository

- `data/DataCoSupplyChainDataset.csv` (~95 MB)
- `reports/EDA_01.html` (~40 MB generated EDA report)

The dataset and generated EDA report have been left in the original repository rather than added to this new repo by default. The dataset is needed for full training; download/copy it into `data/DataCoSupplyChainDataset.csv` locally. The tracked `.gitignore` excludes the dataset, reports, and generated artifacts.

## Compatibility note

The API expects `artifacts/supplyguard_pipeline.joblib`; the two copied `.joblib` files are legacy assets and are not compatible with the current API contract. Retrain with the current `train.py` to generate the expected artifact.

## Git history

The source files are copied as new commits into this repository; original historical commit history is not preserved here. It remains available in `Unretur/ml-journey`.