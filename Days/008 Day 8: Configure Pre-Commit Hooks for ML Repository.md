# Day 8: Configure Pre-Commit Hooks for ML Repository

## The task:

The xFusionCorp Industries ML team enforces code quality on every commit via pre-commit. A draft .pre-commit-config.yaml exists in the git repository at /root/code/fraud-detection/, but it does not match the team's standard and pre-commit run --all-files fails against it. Correct the configuration.


A git repository already exists at /root/code/fraud-detection/ with .pre-commit-config.yaml and process.py already tracked. pre-commit is installed system-wide.

The corrected configuration must declare the following five hooks so that pre-commit run --all-files executes every one of them:

trailing-whitespace, end-of-file-fixer, and check-yaml – All three sourced from the pre-commit/pre-commit-hooks repository, pinned to a current release;
ruff – Sourced from the astral-sh/ruff-pre-commit repository, pinned to a current release;
black – Sourced from the psf/black-pre-commit-mirror repository, pinned to a current release.
Every repository entry in the configuration must include a rev: field.

Review the existing .pre-commit-config.yaml and correct everything that prevents the hooks above from running.

Once the configuration is correct, register the hooks with git and run them against the tracked files:

   pre-commit install
   pre-commit run --all-files

Tip: pre-commit autoupdate queries each referenced repository and rewrites the rev: pins to the latest released tag. This is the standard way to discover current versions without looking them up by hand.

## Solution

#### Take ins:
The instructions requires;
- trailing-whitespace, end-of-file-fixer, and check-yaml – All three sourced from the pre-commit/pre-commit-hooks repository, pinned to a current release;

- ruff – Sourced from the astral-sh/ruff-pre-commit repository, pinned to a current release;

- black – Sourced from the psf/black-pre-commit-mirror repository, pinned to a current release.

- **Every repository entry in the configuration must include a rev: field.**

- The tricky part in the first instruction is in the **check-yaml**

#### Steps

Replace the contents of /root/code/fraud-detection/.pre-commit-config.yaml with:

```bash
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v5.0.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml

  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.11.13
    hooks:
      - id: ruff

  - repo: https://github.com/psf/black-pre-commit-mirror
    rev: 25.1.0
    hooks:
      - id: black
```
---
Changes made are:
- Changed the rev version of the first repository updated to the latest version, and the rev in the black repository added as per the instructions.

- Changed the ruff repository to be sourced from astral-sh/ruff-pre-commit repository, and pinned to a current release.

- In the first repo, update the third id in the hooks from check_yaml to ```check-yaml```

- Updated the second repository- ruff-lint to ```ruff```
---
Once the changes are made;
register the hooks with git and run them against the tracked files:
```bash 
pre-commit install 
pre-commit run --all-files
```
---


## Takeaways:
This task is about setting up automated code-quality checks that run before code is committed to Git.

The tool being used is pre-commit, which manages Git hooks automatically.
So before a commit succeeds, these tools run automatically.

###### 1. What .pre-commit-config.yaml does

This file tells pre-commit:

- which repositories contain hooks,
- which hook versions to use,
- which checks to run.

##### 2. The hooks in the task
1. trailing-whitespace

Removes unnecessary spaces at the ends of lines.
2. end-of-file-fixer

Ensures files end with exactly one newline.


3. check-yaml

Validates YAML syntax.

This prevents broken CI/CD configs and deployment configs.


4. ruff

Ruff is a fast Python linter.

It checks:

- unused imports,
- undefined variables,
- import ordering,
- style issues,
- potential bugs.


5. black

Black automatically formats Python code consistently.

Instead of developers arguing about:

- spacing,
- quotes,
- line wrapping,

Black decides for everyone.