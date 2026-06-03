# Day 21: Log an ML Experiment to MLflow

A xFusionCorp Industries data scientist needs a training run recorded in MLflow so the team has a baseline record on the tracking dashboard. The non-MLflow scaffolding has already been written at /root/code/log_experiment.py; the MLflow logging calls are left as TODO blocks. Your task is to complete the script so that every element of the run is captured by the MLflow tracking server.


The MLflow tracking server is already running on port 5000. The MLflow UI button at the top of the lab can be opened to view the dashboard; the Default experiment is present on first load.

/root/code/log_experiment.py can be opened in the VS Code editor. The script prepares a params dictionary, fits a trivial sklearn model, and advertises a pair of synthetic evaluation scores (accuracy and f1). Three blocks marked # TODO inside the mlflow.start_run() context are the only edits required.

Execute the script once (python3 /root/code/log_experiment.py) after the TODOs are completed. The end state must include:

Exactly one new run in the Default experiment.
Every hyperparameter in the params dict (n_estimators=100, max_depth=5, random_state=42) recorded as a run parameter.
Both advertised scores (accuracy, f1_score) recorded as run metrics.
The sklearn model captured as an MLflow model artefact on the run.


## Solution

This task is testing your understanding of the three core things MLflow tracks:

1. Parameters → hyperparameters used for training
2. Metrics → model performance values
3. Artifacts/Models → the trained model itself

The script already creates:

- a params dictionary
- a trained sklearn model
- two metric values (accuracy and f1_score)

Your job is only to fill in the MLflow logging calls inside the with mlflow.start_run(): block.

Modify the log_experiment.py file inside the with mlflow.start_run():

```bash
with mlflow.start_run():

    # TODO 1
    for key, value in params.items():
        mlflow.log_param(key, value)

    # TODO 2
    mlflow.log_metric("accuracy", accuracy)
    mlflow.log_metric("f1_score", f1)

    # TODO 3
    mlflow.sklearn.log_model(model, "model")

```

The task explicitly says:
log accuracy and f1 as MLflow metrics named "accuracy" and "f1_score" respectively

After the modifications, run:
```bash
python3 /root/code/log_experiment.py
```
In the MLflow ui you should see the dafault parameter

