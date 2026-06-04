# Create and Organize MLflow Experiments


The xFusionCorp Industries ML platform team is onboarding two new ML projects and needs each one organised under its own MLflow experiment rather than sharing the Default experiment. Your task is to register both experiments through the MLflow UI and tag them with the owning team.


The MLflow tracking server is already running on port 5000. The MLflow UI button at the top of the lab can be opened to view the dashboard. One seeded experiment 
(legacy-models) is listed alongside the platform-created Default—both act as reference material and must not be modified.

Using the MLflow UI, register two new experiments with the experiment-level metadata below. The task is complete when both records satisfy every bullet.

fraud-detection

Experiment-level description is a non-empty string describing the project (any phrasing).
Experiment-level tag: key team, value ml-platform.
churn-prediction

Experiment-level tag: key team, value analytics.


## What the task is about:
This exercise demonstrates how teams organize ML work in MLflow. Instead of placing every run into the Default experiment, projects are separated into dedicated 
experiments and annotated with metadata such as ownership tags. This makes it easier to search, filter, govern, and manage experiments across multiple teams and machine 
learning projects as the number of runs grows over time.

## Solution
> Te whole task is done via the MLflow ui
1. Open the MLflow UI

Click the MLflow UI button at the top right of the lab.

Do not modify the existing experiments:

- Default
- legacy-models

2. Create the fraud-detection experiment
    1. Click the experiments on the left navigation panel.
    2. Create a new experiment, the create button is at the top right.
    3. Name the experiment 
        ```yaml
        fraud-experiment
        ```
    4. Once the experiment is created and opened, click the three dots at the right and add any description.
            ![image](https://github.com/user-attachments/assets/c3ee1224-0877-468b-89dd-56da37432358)
    5. Back at the experiments, click add new tags:
        - add new tag:
            - key:
                ```bash
                team
                ```
            - value:
            ```bash
            ml-platform
            ```
3. Create a new experiment```churn-experiment```:
    1. create a new experiment with:
    2. Name: ```churn-experiment```
    3. save the experiment 
    4. Add tags:
        - key: ```team```
        - value: ```analytics```

4. Ensure there are 4(Four) experiments in the experiment section
![](https://github.com/user-attachments/assets/c8be143d-9d22-4089-8d70-693f7cb0caf1)

