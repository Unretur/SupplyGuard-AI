# Migration status

The project source has been extracted from [Unretur/ml-journey/Projects/SupplyGuard](https://github.com/Unretur/ml-journey/tree/main/Projects/SupplyGuard) into this standalone repository.

## Present in this repository

- `Data.py`, `features.py`, `train.py`, `evaluate.py`, and `api.py`
- `tests/` API and pipeline tests
- `01_eda.ipynb` exploratory analysis notebook
- `PERFORMANCE_REVIEW.md`
- `requirements.txt`
- A standalone GitHub Actions workflow at `.github/workflows/tests.yml`
- Root-level setup instructions in `README.md`

## Not copied as tracked files yet

The source repository is unchanged and still contains the following original assets:

- `data/DataCoSupplyChainDataset.csv` (~95 MB)
- `reports/EDA_01.html` (~40 MB generated EDA report)
- `mlflow.db` (generated experiment database)
- `encoder.joblib` and `final_model.joblib` (legacy binary model artifacts)

The dataset, generated report, database, and legacy models were deliberately not copied through the text-only GitHub file API. Do not treat this as a fully byte-for-byte migration. For binary files, use local Git/PowerShell copy commands or another binary-safe transfer path. The source repo remains unchanged.

## Git history

Files in this repository were committed into the new repository; this file-level migration does not preserve the original commit history. The original commits remain available in `Unretur/ml-journey`.