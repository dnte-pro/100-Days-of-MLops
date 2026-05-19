# Day 7: Package an ML Project as Installable Python Package

## The task
The xFusionCorp Industries deployment team needs the fraud-detection model code packaged as an installable Python distribution. A draft pyproject.toml exists at /root/code/fraud-detection/, but it does not build a wheel that meets the team's standard. Correct the file and produce a compliant package.


The project at /root/code/fraud-detection/ already contains the source code under src/fraud_detection/. The Python files are complete—you do not need to modify any of them.

The corrected pyproject.toml must satisfy every one of the following:

it declares a [build-system] section with requires = ["setuptools>=61.0", "wheel"] and build-backend = "setuptools.build_meta";
name is fraud_detection (the distribution name must match the module path under src/);
version is 0.1.0;
requires-python is >=3.10;
dependencies is ["scikit-learn", "pandas", "numpy"].
Review the existing pyproject.toml and correct everything that does not match the requirements above.

Build the package from the project directory:

   cd /root/code/fraud-detection
   python3 -m build

The build must produce a wheel named fraud_detection-0.1.0-*.whl under dist/.
The build package is already installed. Use python3 rather than python.


## Solution

Edit the contents of the pyproject.toml as directed by the instructions with the details :
```bash
[build-system]
requires = ["setuptools>=61.0", "wheel"]
build-backend = "setuptools.build_meta"

[project]
name = "fraud_detection"
version = "0.1.0"
requires-python = ">=3.10"
description = ""
dependencies = [
    "scikit-learn",
    "pandas",
    "numpy",
]

[tool.setuptools.packages.find]
where = ["src"]
```
**Ensure the name has the underscore(_) as in fraud_detection**

Then build the package
In the terminal, change the directory to fraud-detection
```cd /root/code/fraud-detection ```
Build the package 
``` python3 -m build```
Verify that the wheel was created:
```ls dist/```

A file is created in the src folder similar to
```fraud_detection-0.1.0-p____.whl ```
The important detail is that the distribution name matches the package path under src/fraud_detection/. Packaging systems become surprisingly emotional when those names drift apart.