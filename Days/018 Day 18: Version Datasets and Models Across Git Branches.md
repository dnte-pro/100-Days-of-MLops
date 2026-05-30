# Day 18: Version Datasets and Models Across Git Branches

## Scenario:

The xFusionCorp Industries ML team keeps different dataset and model versions on different Git branches so that the team can roll between versions cleanly. Tag the current state as v1.0, produce a v2-improved branch based on a newer dataset, and confirm that switching back restores the original data.


A project exists at /root/code/fraud-detection/ with a working DVC pipeline and the baseline data/raw/transactions.csv already tracked.

An improved dataset has been pre-staged at /root/code/fraud-detection/data/raw/transactions_v2.csv and is visible in the file explorer. Do not delete this file.

On the main branch, tag the current state as v1.0.

Create a new branch named v2-improved. Replace the tracked dataset with the contents of the v2 file, re-track it with DVC, re-run the pipeline, and commit the changes.

Switch back to the main branch and use dvc checkout to restore the v1 dataset on disk. The restored content must match the hash recorded by the v1.0 tag.

The DVC extension's DVC TRACKED section in the EXPLORER panel will reflect the current branch's tracked state—it should show different dataset hashes on main and v2-improved.

### Solution

1. Tag the current state on main branch

```bash
cd /root/code/fraud-detection

git checkout main
git tag v1.0
```

Verify the tag:

```bash
git tag
```


2. Create the new branch v2-improved

Create the branch v2-improved for the changes:

```bash
git checkout -b v2-improved
```
- The command creates a new branch and switches to it.

Verify that you are on the new branch:

```bash
git branch
```

3. Replace the tracked dataset with the v2 dataset
Keep transactions_v2.csv intact, but copy its contents over the tracked dataset:

```bash
cp data/raw/transactions_v2.csv data/raw/transactions.csv
```
 
The contents of the file transactions.csv changes.

4. Update DVC tracking
Since the file contents changed, update the DVC metadata:
```bash
dvc add data/raw/transactions.csv
```
This updates the file data/raw/transactions.csv.dvc

5. Re-run the pipeline
Re-run the pipeline with the changes:
```bash
dvc repro
```

Running the pipeline generates new files.


6. Commit the v2 version
```bash
git add .

git commit -m "improved v2"
```

7. Return to main

Return to the main branch:
```bash
git checkout main
```
At this point Git restores the .dvc metadata for v1, but the workspace data file may still contain the v2 contents.


8. Restore the correct DVC-tracked data

To restore the v1 dvc-tracked data :
 ```bash
 dvc checkout
 ```

The initial data/raw/transactions.csv is restored.