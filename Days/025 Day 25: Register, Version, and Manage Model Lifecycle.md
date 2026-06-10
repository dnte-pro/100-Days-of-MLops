# Day 25: Register, Version, and Manage Model Lifecycle


## Task

The xFusionCorp Industries ML platform team needs two trained candidates promoted through the MLflow Model Registry so the ops side can track which model version is serving production traffic. Both runs already exist in the fraud-detection experiment. Your task is to register both as versions of a new fraud-detector model, add a model-level description, and assign challenger and champion aliases—all through the MLflow UI.


The MLflow tracking server is already running on port 5000 and two runs are pre-populated in the fraud-detection experiment: a baseline run (n_estimators=100, max_depth=5, f1_score=0.80) and an improved run (n_estimators=200, max_depth=10, f1_score=0.89). Both runs can be opened via the MLflow UI button → fraud-detection experiment.

Using the MLflow UI, reach the end state below. The order (baseline first, improved second) matters because MLflow assigns version numbers sequentially within a registered model.

A registered model named fraud-detector exists in the Model Registry.
The registered model carries a non-empty description that references the word fraud (any phrasing; for example Fraud detection model for xFusionCorp transactions).
Version 1 of fraud-detector is the baseline run and carries the alias challenger.
Version 2 of fraud-detector is the improved run and carries the alias champion.



### Step-by-step implementation


#### 1. Open the fraud-detection experiment
Open the MLflow UI.
- Go to the fraud-detection experiment.
- Identify the two runs:



| Run      | Parameters                     | F1 Score |
| -------- | ------------------------------ | -------- |
| Baseline | n_estimators=100, max_depth=5  | 0.80     |
| Improved | n_estimators=200, max_depth=10 | 0.89     |


#### 2. Register the baseline run first

It is important to register the baseline run first(as per the instructions) because MLflow assigns version numbers sequentially.

- Open the baseline run.
- In the model artifact section, choose Register Model.
- Create a new registered model named: ```fraud-detector```
- Complete registration - this creates: ```fraud-detector v1``


#### 3. Register the improved run 
1. Open the improved run.
2. Register its model artifact.
3. Select the existing registered model: ```fraud-detector```
This creates ```fraud-detector v2```


#### 4. Add model description

Open the model registry and edit the model description and enter any non-empty text containing the word fraud, for example:
```text 
Fraud detection model for xFusionCorp transaction monitoring.
```
















































