# Day 26: Compare Model Runs and Select the Best

## Task 
A xFusionCorp Industries data scientist has trained three candidate models on the same problem and logged them to the model-comparison experiment. Your task is to review the candidates side by side in the MLflow UI and explicitly mark the winning run so downstream tooling can pick it up.


The MLflow tracking server is already running on port 5000 and the model-comparison experiment has been pre-populated with three runs, each named after its algorithm (RandomForest, GradientBoosting, LogisticRegression) and carrying accuracy and f1_score metrics. The runs can be viewed via the MLflow UI button → model-comparison experiment.

Using the MLflow UI, inspect the three runs side by side and identify the winner by metrics.f1_score.

The run with the highest f1_score must carry a run-level tag: key production-candidate, value true.
Neither of the other two runs may carry a production-candidate tag.

>The task is entirely done in the MLflow ui


### STep-by -step Evaluation
1. Open the MLflow and then the experiments
2. View the three runs:
    - RandomForest
    - GradientBoosting
    - LogisticRegression

3. Compare the f1_score metrics by opening the **Training runs** on the left navigation panel, then sort by the f1_score

4. Identify the metric with the highest f1_score.
5. After Identifying the metric with the highest score, open the Evaluatioin runs on the left panel and add the tag ```champion```

6. Ensure the other runs do not have tags
