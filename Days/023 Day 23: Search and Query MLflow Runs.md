# Search and Query MLflow Runs


## Task:

A xFusionCorp Industries data scientist has accumulated ten runs in the fraud-detection MLflow experiment. Your task is to triage those runs via the MLflow UI: mark the single best-performing candidate as the shortlisted model, and flag every clearly under-performing run for removal.


The MLflow tracking server is already running on port 5000, and the fraud-detection experiment has been pre-populated with ten runs. The runs can be viewed via the MLflow UI button → fraud-detection experiment.

Using the MLflow UI, complete the triage below. The end state is what is tested—the path taken through the UI is not.

Shortlist the best candidate. Among all runs where metrics.f1_score > 0.85, the single run with the highest f1_score must carry a run-level tag: key review-status, value shortlisted.

Reject the under-performers. Every run where metrics.f1_score < 0.75 must carry a run-level tag: key review-status, value rejected.

The other runs (those in the 0.75 ≤ f1 ≤ 0.85 band, and the second-best shortlisting candidate) must carry no review-status tag at all.

### Step-by-step Implementation

> The task is entirely in the MLflow UI, click the ui button to open the MLflow

1. Open the fraud-detection experiment
- After opening the UI and selecting the fraud-detection experiment, on the left panel open the experiment runs to see the 10 runs made.
2. Identify the shortlisted run 
- Find the run with the highest f1_score open the run ad add the tag:

| Key                       | Value       |
| --------------------------| ----------- |
| review-status             | shortlisted |


Only the one with the highest f1_score should have this tag

3. Reject under-performing runs

Inspect runs where ```f1_score < 0.75``:
for each run in this category add the tag

| Key           | Value    |
| ------------- | -------- |
| review-status | rejected |

4. Ensure only the shortlisted run and the rejected ones are the only ones tagged.
- Any run with ```0.75 ≤ f1_score ≤ 0.85``` must not have a **review-status** tag








| Condition                                        | Tag                         |
| ------------------------------------------------ | --------------------------- |
| Highest f1_score among runs with f1_score > 0.85 | `review-status=shortlisted` |
| f1_score < 0.75                                  | `review-status=rejected`    |
| 0.75 ≤ f1_score ≤ 0.85                           | No tag                      |
| Other runs > 0.85 but not the best               | No tag                      |
