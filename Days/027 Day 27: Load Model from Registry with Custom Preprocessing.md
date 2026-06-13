# Day 27: Load Model from Registry with Custom Preprocessing


## Task The xFusionCorp Industries deployment team needs a batch-prediction wrapper around the registered fraud-detector champion model, complete with custom preprocessing, before the model is exposed to downstream services. The wrapper class is pre-written. Your task is to complete the MLflow-side plumbing that loads the champion and runs the batch.


The MLflow tracking server is already running on port 5000. The MLflow UI button at the top of the lab can be opened to view the dashboard; the Models tab shows fraud-detector registered with a champion alias on version 1.

Open /root/code/predict_with_preprocessing.py in the VS Code editor. The ScaledPredictor class (a pyfunc wrapper that applies per-column mean/std scaling inside its .predict() method) and the MODEL_URI / INPUT_CSV / OUTPUT_CSV constants at the top of the file are already written and must NOT be modified. Two # TODO blocks remain:

TODO 1: Load the champion version of fraud-detector from MLflow's Model Registry into a variable named inner_model. MODEL_URI is already set to models:/fraud-detector@champion.
TODO 2: Run the batch prediction over the pre-staged inputs, attach the predictions as a new prediction column on the inputs DataFrame, and write the result to OUTPUT_CSV (/root/code/predictions.csv) with index=False.
After both TODOs are completed, run the script once:

   python3 /root/code/predict_with_preprocessing.py

The end state must include:

A file at /root/code/predictions.csv with a header row.
A prediction column in that CSV.
The number of prediction rows equal to the number of input rows in /root/code/data/inputs.csv (ten).

## Step-by-step addition

This task is testing whether you know how to:

- Load a model from the MLflow Model Registry using its alias (champion).
- Use the provided wrapper (ScaledPredictor) around that model.
- Generate predictions and save them to a CSV.

1. **TODO 1**
Load the champion model into inner_model.
The TO DO 1 section should look like:
```bash
inner_model = mlflow.pyfunc.load_model(MODEL_URI)

# Compute per-column mean and std from the pre-staged inputs, then
# build the pyfunc wrapper around `inner_model`.
inputs = pd.read_csv(INPUT_CSV)
mean = inputs.values.mean(axis=0)
std = inputs.values.std(axis=0)
std[std == 0] = 1.0  # guard against division by zero on constant columns

predictor = ScaledPredictor(inner_model, mean, std)

```

2. **TODO 2**

Configure the configuration of the prediction inputs:
```bash
predictions = predictor.predict(None, inputs.values)
inputs["prediction"] = predictions
inputs.to_csv(OUTPUT_CSV, index=False)
```


3. Run the code 
After proper file configuration run the file:
```bash
python3 /root/code/predict_with_preprocessing.py
```

After running the file, you should have:

* a prediction column,
* 10 prediction rows (plus the header),
* /root/code/predictions.csv successfully created.