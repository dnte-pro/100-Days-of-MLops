# Day 6: Set Up Code Quality Tools for ML Code


## Task: 
The xFusionCorp Industries ML team enforces code quality with ruff and black on every pull request. The project at /root/code/fraud-detection/ currently fails both tools. Make it pass them.


The project at /root/code/fraud-detection/ contains a pyproject.toml and sample sources under src/.

The corrected project must meet the following requirements:

ruff and black are both configured with a line length of 120.
ruff lint rule selection includes E, F, W, and I, and is declared under [tool.ruff.lint] – The schema required by ruff 0.1 and later.
Running ruff check src/ from the project directory exits with status 0.
Running black --check src/ from the project directory exits with status 0.
Review the existing configuration and source files, and correct everything that prevents the two commands above from exiting cleanly.

ruff, black, and mypy are already installed. 

## Solution:

Start by inspecting the folders in the project using the IDE or the terminal.

#### Via the IDE:
Open the pyproject.toml in the fraud-detection folder and inspect the contents therein

#### Via the terminal 

```bash
cd /root/code/fraud-detection
cat pyproject.toml
```

Then fix the pyproject.toml so it matches the required Ruff 0.1+ schema:
```bash
[tool.black]
line-length = 120

[tool.ruff]
line-length = 120

[tool.ruff.lint]
select = ["E", "F", "W", "I"]
```

After the updates, auto-fix imports and formatting:

```bash 
ruff check src/ --fix
black src/
```

##### Verification that everything passes clearly

```bash

ruff check src/
black src/
```