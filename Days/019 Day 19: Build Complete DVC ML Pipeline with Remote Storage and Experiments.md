# Day 19: Build Complete DVC ML Pipeline with Remote Storage and Experiments

## Scenario:
Complete the xFusionCorp Industries fraud-detection production DVC pipeline. Three stages are already wired in dvc.yaml, two remain, and the pipeline must finish as a reproducible, SeaweedFS-backed, v1.0-tagged release.


A project exists at /root/code/ml-pipeline/ with Git and DVC initialised. The params.yaml is in place and the .dvc/config is pre-configured to push to the SeaweedFS bucket dvc-storage at http://localhost:8333.

The ingest, validate, and preprocess stages are already declared in dvc.yaml, but one of them contains an incorrect output path that prevents dvc repro from completing. Find and fix it.

The remaining two stages need to be added:

train – Depends on the preprocessed dataset and scripts/train.py; reads n_estimators, max_depth, test_size, and random_seed from params.yaml; outputs models/model.pkl and data/processed/test_split.csv; declares metrics.json as a DVC metric with cache: false.
evaluate – Depends on models/model.pkl, data/processed/test_split.csv, and scripts/evaluate.py; outputs reports/evaluation.json declared with cache: false.

The two scripts you need are pre-staged at /root/code/ml-pipeline/scripts-staging/train.py and scripts-staging/evaluate.py. Copy them into scripts/ before adding the stages.

Run the full pipeline with dvc repro, push the cache to the SeaweedFS remote with dvc push, and tag the current state as v1.0.

Commit every change to Git so the release is fully captured.

Open the SeaweedFS Filer button at the top of the lab and navigate to /buckets/dvc-storage/ to confirm that the bucket holds the pushed artefacts under the files/md5/... layout.



### Step-by-step solution:
1. Copy the provided scripts

Get into the correct directory and copy the scripts:

```bash
cd /root/code/ml-pipeline

cp -f scripts-staging/train.py scripts/train.py
cp -f scripts-staging/evaluate.py scripts/evaluate.py
```

2. Fix dvc.yaml

The validator has already told us:

- train must depend on data/processed/clean.csv
- evaluate must run scripts/evaluate.py
- metrics.json must be a metric
- reports/evaluation.json must be a non-cached output


>The train and the evaluate metrics should look like:

```bash
train:
    cmd: python scripts/train.py
    deps:
      - data/processed/clean.csv
      - scripts/train.py
    params:
      - n_estimators
      - max_depth
      - test_size
      - random_seed
    outs:
      - models/model.pkl
      - data/processed/test_split.csv
    metrics:
      - metrics.json:
          cache: false

  evaluate:
    cmd: python scripts/evaluate.py
    deps:
      - models/model.pkl
      - data/processed/test_split.csv
      - scripts/evaluate.py
    outs:
      - reports/evaluation.json:
          cache: false
```
3. Preprocess metric edit

Edit the preprocess out metric, it should look like:
```yaml
outs:
  - data/processed/clean.csv
```


4. Run the pipeline

```bash
dvc repro
```

The command should run successfully and generate new files.

5. Verify the dvc status

Verify:

```bash
dvc status
```
```Data and pipelines are up to date. ``` should be the output of the command

6. Push artifacts to SeaweedFS
Push the artifacts to the bucket 
```bash
dvc push
```
7. Commit 

```bash
git add .
git commit -m "Complete production DVC pipeline"
```

8. Create the release tag

```bash
git tag v1.0
```

Verify the tag was created:
```bash
git tag v1.0
```