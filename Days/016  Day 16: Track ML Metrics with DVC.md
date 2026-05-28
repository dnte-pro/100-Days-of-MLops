# Day 16: Track ML Metrics with DVC

## Task:

After training a model, the xFusionCorp Industries ML team wants DVC to surface metrics through dvc metrics show and the DVC extension's METRICS view. The fraud-detection pipeline already trains a model and writes a metrics.json, but DVC does not recognise the file as a metric. Wire it in correctly.


A project exists at /root/code/fraud-detection/ with a three-stage DVC pipeline (process_data, split_data, train). The train stage runs src/models/train.py, which writes the model to models/model.pkl and metrics to metrics.json. Do not modify the Python files.

The train stage in dvc.yaml must declare metrics.json as a DVC metric output, not as a regular file output. The metric must be declared with cache: false so the JSON lives in Git for diff history rather than in the DVC cache.

Re-run the pipeline with dvc repro so the metric registration takes effect.

After your changes, dvc metrics show must report the accuracy and f1_score values from metrics.json.



## Solution:

Inspect all the files:

"The train stage in dvc.yaml must declare metrics.json as a DVC metric output, not as a regular file output. The metric must be declared with cache: false so the JSON lives in Git for diff history rather than in the DVC cache."


The line states that the train stage should have 4 metrics, the metrics.json is the fourth metric but has been declared as an output. 

The train stage looks like:

```yaml
train:
  cmd: python src/models/train.py
  deps:
    - data/processed/train.csv
    - src/models/train.py
  outs:
    - models/model.pkl
    - metrics.json
```

The correct configuration should have:

```yaml
train:
  cmd: python src/models/train.py
  deps:
    - data/processed/train.csv
    - src/models/train.py
  outs:
    - models/model.pkl
  metrics:
    - metrics.json:
        cache: false
```



The full dvc.yaml should look  like:
```yaml
stages:
  process_data:
    cmd: python src/data/process_data.py
    deps:
      - data/raw/transactions.csv
      - src/data/process_data.py
    outs:
      - data/processed/clean_transactions.csv

  split_data:
    cmd: python src/data/split_data.py
    deps:
      - data/processed/clean_transactions.csv
      - src/data/split_data.py
    outs:
      - data/processed/train.csv
      - data/processed/test.csv

  train:
    cmd: python src/models/train.py
    deps:
      - data/processed/train.csv
      - src/models/train.py
    outs:
      - models/model.pkl
    metrics:
      - metrics.json:
          cache: false
```


After the edits, run the pipeline:

```bash
cd /root/code/fraud-detection

dvc repro
```

Verify metrics registration:

```bash
dvc metrics show
```

It should show metrics as:
```bash
                    accuracy:        f1_score:
metrics.json:           1.0             1.0

```





**Takeaways** 

The task test the understanding of how This task tests understanding of how DVC manages machine learning experiment outputs beyond datasets and models. Specifically, it teaches the distinction between regular pipeline outputs (outs) and tracked evaluation metrics (metrics). By declaring metrics.json as a metric with cache: false, DVC treats the file as lightweight experiment metadata that should remain in Git for easy comparison and history tracking instead of storing it in the DVC cache. This enables commands like dvc metrics show and metric diffing between experiments, which are essential for reproducible ML workflows.