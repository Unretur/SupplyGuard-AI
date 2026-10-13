# SupplyGuard AI

SupplyGuard predicts **shipment delay in days** using the DataCo Supply Chain dataset.

`delay_days = Days for shipping (real) - Days for shipment (scheduled)`

Positive predictions indicate late delivery, zero indicates on-schedule delivery, and negative predictions indicate earlier-than-scheduled delivery. This is a retrospective ML project, not a guarantee of real-world delivery performance.

## Repository contents

- `Data.py` — data loading, target construction, and chronological holdout split.
- `features.py` — shared preprocessing and feature-schema validation.
- `train.py` — baseline comparison, chronological validation, and model selection.
- `evaluate.py` — holdout metrics and diagnostics.
- `api.py` — FastAPI prediction API with liveness/readiness checks.
- `01_eda.ipynb` — exploratory analysis notebook.
- `tests/` — API contract and pipeline tests.
- `PERFORMANCE_REVIEW.md` — engineering and modeling review.

## Dataset setup

The original project uses the DataCo Supply Chain dataset at `data/DataCoSupplyChainDataset.csv`.

The raw CSV (~96 MB) is intentionally not duplicated into this repository during migration. Place a licensed/local copy at that path before training, or adjust the `--data` argument to its location. Keep datasets and generated reports out of Git unless you have a clear redistribution right and a reason to version them.

## Local setup (Windows PowerShell)

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m pytest tests/ -q
```

On Linux/macOS, activate with `source .venv/bin/activate`.

## Train and evaluate

```powershell
python train.py --data data/DataCoSupplyChainDataset.csv --trials 5
python evaluate.py --data data/DataCoSupplyChainDataset.csv
```

Training may be expensive on CPU. Start with a small number of trials to verify the pipeline before increasing it. The final chronological holdout should remain reserved for final evaluation; model selection uses a validation window from the training period.

## Run the API

```powershell
uvicorn api:app --reload
```

Open `http://127.0.0.1:8000/docs` to try the API.

- `GET /health`: process liveness.
- `GET /ready`: checks whether a compatible model artifact is available.
- `GET /model-info`: information about the loaded model and target.
- `POST /predict`: estimates shipping delay in days.

The API expects `artifacts/supplyguard_pipeline.joblib` by default. Set `SUPPLYGUARD_MODEL_PATH` to use another path. Retrain using the current pipeline before relying on older serialized files; legacy `final_model.joblib` and `encoder.joblib` files may not match the current inference contract.

## Generated files and artifacts

Model artifacts, MLflow tracking databases, and generated HTML EDA reports are reproducibility outputs rather than source-of-truth code. The legacy artifacts and MLflow database remain in the original `ml-journey` project and can be copied locally when needed. They are not required to run unit tests. Never load joblib/pickle artifacts from an untrusted source.

## Important limitations

The dataset contains fields that may not be known at the time an operational prediction is needed. Define a prediction timestamp and audit feature availability before presenting this as an early-warning system. Historical estimates do not guarantee performance on current carriers, routes, or warehouses. Full retraining and holdout verification against the entire dataset have not been completed as part of this repository migration.
