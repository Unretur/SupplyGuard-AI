# SupplyGuard AI migration status

The standalone repository is being prepared from the project at `Projects/SupplyGuard` in [Unretur/ml-journey](https://github.com/Unretur/ml-journey/tree/main/Projects/SupplyGuard).

## Preservation rules
- The source repository is not modified or deleted.
- Preserve all source and model/algorithm-named files when transferring locally.
- The ~95 MB dataset, generated EDA HTML report, and MLflow database should not be copied into the tracked project by default. They remain safely in the original repository for now.
- Binary `.joblib` model artifacts need a local Git transfer path; do not try to decode them as text.
- The connected GitHub file API only supports text file creation/update for this workflow. To move the full project reliably, clone the source and use Git locally to copy the directory into this repository. That also keeps binary files intact. Full commit history can be preserved separately if desired.

See the README and the local migration instructions in the conversation for the exact commands.