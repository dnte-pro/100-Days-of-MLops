# Enable MLflow Autologging

## Task
The xFusionCorp Industries ML team wants to replace the manual log_param / log_metric boilerplate in their training scripts with MLflow's autologging feature, so every training run captures its constructor parameters, training metrics, and model artefact automatically. A training scaffold has been pre-staged at /root/code/autolog_experiment.py—it configures MLflow, fits a small synthetic sklearn model, and prints a confirmation message. Two # TODO blocks remain empty. Your task is to complete them so the end state below holds.


The MLflow tracking server is already running on port 5000. The MLflow UI button at the top of the lab can be opened to view the dashboard; only the Default experiment is present on first load.

Open /root/code/autolog_experiment.py in the VS Code editor and complete the two TODO blocks—both are one-line additions—so that, after the script is executed, the following end state holds:

An experiment named autolog-demo exists on the MLflow server.
At least one run exists in the autolog-demo experiment.
The run's Parameters panel lists every sklearn constructor parameter that the LogisticRegression in the scaffold implicitly carries (for example C, max_iter, solver, tol, penalty) – Not only the three explicit keyword arguments the scaffold passes.
The Artifacts panel on the run contains a model directory with an MLmodel descriptor and a pickled estimator.
Once the TODOs are in place, execute the script:

   python3 /root/code/autolog_experiment.py

Confirm the result in the MLflow UI.


- This lab is testing two MLflow features:
    - Creating/selecting an experiment
    - Enabling sklearn autologging

## Step-by-step solving

1. Fix the missing parameters in autolog_experiment.py
- The first TODO should contain:

```bash
mlflow.sklearn.autolog()
```

and the second TODO:

```bash
mlflow.set_experiment("autolog-demo")
```
2. Run 
 Run with the code:

```bash
python3 /root/code/autolog_experiment.py
 ```
3. Verify in the MLflow:
Open the MLflow UI and confirm:

An experiment named:
```bash
autolog-demo
```
exists.

The experiment contains at least one run.

## What the task is about
This lab demonstrates MLflow autologging with MLflow. Instead of manually writing ```log_param()```, ```log_metric()```, and model logging code, autologging automatically intercepts supported ML library calls (such as ```sklearn.fit()```) and records model parameters, metrics, tags, and artifacts. This reduces boilerplate, ensures consistency across projects, and captures far more metadata than developers typically log by hand.