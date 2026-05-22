# Day 10: Install and Initialize DVC in an ML Project

The xFusionCorp Industries ML team is adopting DVC so that datasets and model files are versioned separately from code. Initialise DVC inside the existing Git repository at /root/code/fraud-detection/ and record the initialisation in Git.


A Git repository already exists at /root/code/fraud-detection/ with an initial commit.

Initialise DVC inside that repository so that the standard .dvc/ control directory and .dvcignore file are created alongside the existing Git working tree.

Stage every file that DVC produces during initialisation, and record them in a new Git commit with the message Initialize DVC.

Once initialisation is complete, the DVC extension will detect the new .dvc/ directory and surface the DVC TRACKED section in the EXPLORER panel together with a DVC indicator in the bottom status bar.


### DVC is Data Version Control used by Machine Learning Engineers to store large datasets and ML artifacts - because committing large(like 14GB) model checkpoints directly to git could cost teams.

## Solution

In the terminal, change to the fraud-detection folder
```bash
cd /root/code/fraud-detection
```

Initialize dvc
```bash
dvc init
```

Stage the files added to git
```bash
git add .dvc .dvcignore
```

Commit with the message ```InitializeDVC```
```bash
git commit -m "Initialize DVC"
```


### What this does
- dvc init
    - initializes DVC inside the existing Git repository
    - creates:
      - .dvc/
      - .dvcignore
    - git add
      - stages the DVC configuration files
    - git commit
      - records the initialization in Git history

After this:
  - VS Code should detect DVC automatically
  - the .dvc/ directory becomes visible
  - the DVC extension activates in the UI/status bar