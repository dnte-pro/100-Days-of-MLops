# Day 4: Create a Makefile for ML Workflow Automation
The xFusionCorp Industries ML team uses a Makefile to orchestrate common tasks—data processing, training, testing, and cleanup. A draft Makefile exists at /root/code/fraud-detection/Makefile, but make all does not complete successfully. Bring the Makefile in line with the team's standard. 

Change into /root/code/fraud-detection/ and run make all to observe the current failure. 

The corrected Makefile must declare the following six targets and behaviour: 

setup – Creates a virtual environment at mlops-venv/ and installs dependencies from requirements.txt; 

data – Runs python src/data/process_data.py; 

train – Runs python src/models/train.py;

test – Runs pytest tests/;

clean – Recursively removes every __pycache__ directory, removes .pytest_cache, and clears the contents of models/; 

all – Runs setup, data, train, and test in that order. 

All six target names must be declared as .PHONY so that Make never confuses them with files of the same name.

After your changes, make all must complete without error. 

Makefile recipes must be indented with a real tab character, not spaces. Make rejects any recipe that is not tab-indented.


# Solution 

#### The current Makefile has a few errors:
- data: recipe is indented with spaces instead of a TAB.
- clean only removes one __pycache__ directory instead of all recursively.
- clean does not remove .pytest_cache.
- clean does not clear models/.
- all is missing the data target and required order. 
- PHONY declarations are missing.
- setup should be clearer as separate commands.

  Replace the contents with :
```bash
.PHONY: setup data train test clean all

setup:
	python3 -m venv mlops-venv
	./mlops-venv/bin/pip install -r requirements.txt

data:
	python src/data/process_data.py

train:
	python src/models/train.py

test:
	pytest tests/

clean:
	find . -type d -name "__pycache__" -exec rm -rf {} +
	rm -rf .pytest_cache
	rm -rf models/*

all: setup data train test
  ```

Then in the terminal run the command :
```bash
cd /root/code/fraud-detection
make all
```
The ``` make all ``` command performs:
- creates the virtual environment and installs dependencies
- processes the data
- trains the ML model
- runs the tests
