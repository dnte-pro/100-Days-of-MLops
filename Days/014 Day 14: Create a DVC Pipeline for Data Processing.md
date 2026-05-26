# Day 14: Create a DVC Pipeline for Data Processing

## Task

The xFusionCorp Industries ML team uses DVC pipelines to keep data processing reproducible. A draft dvc.yaml exists in the fraud-detection project, but dvc repro does not complete the full pipeline. Correct the pipeline definition so it runs cleanly end to end.


A project exists at /root/code/fraud-detection/ with DVC initialised. Python scripts are at src/data/process_data.py and src/data/split_data.py; raw input is at data/raw/transactions.csv. Do not modify the Python files or the input data.

The corrected pipeline must declare two stages with the following behaviour:

process_data – Depends on data/raw/transactions.csv and src/data/process_data.py; produces data/processed/clean_transactions.csv.
split_data – Depends on data/processed/clean_transactions.csv and src/data/split_data.py; produces data/processed/train.csv and data/processed/test.csv.
Review the existing dvc.yaml and correct everything that prevents dvc repro from completing.

After your changes, dvc repro must run end to end and dvc status must report no stale stages.

<details>
<summary>Solution</summary>

1. Open the dvc.yaml and configure it:


from:
 
```yaml

stages:
  process_data:
    cmd: python src/data/process.py
    deps:
      - data/raw/transactions.csv
      - src/data/process_data.py
    outs:
      - data/processed/clean.csv

  split_data:
    cmd: python src/data/split_data.py
    deps:
      - src/data/split_data.py
    outs:
      - data/processed/train.csv
      - data/processed/test.csv

```

to:

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
```

2. Then run the pipeline in the fraud-detection folder:

```bash
cd /root/code/fraud-detection
dvc repro
```

**Ensure there is no error after running the command**

3. Verify that there are no stale changes:

```bash 
dvc status
```

</details>


### What the task is about:
The pipeline defines a reproducible ML data workflow using dvc.


#### Why DVC pipelines matter

DVC tracks:

- dependencies (deps)
- outputs (outs)
- commands (cmd)

So if:

- raw data changes,
- code changes,
- outputs disappear,

DVC automatically knows which stages must rerun.




