# Day 15: Parameterize a DVC Pipeline

The xFusionCorp Industries ML team manages model hyperparameters through params.yaml so experiments can vary without code changes. The fraud-detection project's train stage already wires params.yaml for n_estimators, but dvc repro currently fails. Correct the parameter wiring and demonstrate that DVC re-runs the train stage when the parameter changes.


A project exists at /root/code/fraud-detection/ with a three-stage DVC pipeline (process_data, split_data, train) and a params.yaml already in place. Do not modify the Python files.

The train stage in dvc.yaml references the n_estimators parameter. Every name listed under params: must resolve to a key in params.yaml.

Review params.yaml, correct whatever prevents dvc repro from completing, and run the full pipeline.

Demonstrate that DVC tracks parameter changes by updating n_estimators to a different value (for example 200). Run dvc repro again—only the train stage should re-execute, the new value must be recorded in dvc.lock, and models/model.pkl must be regenerated.

The DVC extension's PARAMS section under the DVC view will surface the values from params.yaml directly in the editor.


## Solving the Task:

The problem is that the parameter referenced in dvc.yaml under the train stage does not correctly exist in params.yaml.

1. Fix params.yaml
 Open the dvc.yaml file 
 ```bash
 params:
    -n_estimators
```

then the params.yaml must contain:
```bash
n_estimators: 100
```


2. Run the pipeline to check if it is running
 In the terminal, open the fraud-detection folder, then run the pipeline

 ```bash
 cd /root/code/fraud-detection

 dvc repo
 ```

This should successfully execute:

- process_data
- split_data
- train


3. Demonstrate parameter tracking 

Modify the params.yaml
```bash
n_estimators: 200
```


4. Rerun the pipeline

```bash 
dvc repro
```

After the n_estimators value is changed, only the train  re-executes.

5. Verify the dvc.lock

The new value is recorded in dvc.lock, and models/model.pkl are regenerated.

```bash 
cat dvc.lock
```

The updated parameters are stored in the dvc.lock 
![dvc.lock](https://github.com/user-attachments/assets/dc96f866-369b-405a-a539-e818886cac95)


## What the task entails
The setup enables reproducible ML experimentation
DVC essentially treats parameter changes like first-class pipeline dependencies.

Which is extremely useful because ML experimentation without parameter tracking quickly turns into:
“Which model produced these results?”
“No idea, but I think it was Tuesday’s random forest.”