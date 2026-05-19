# Day 1 — Create a Python Virtual Environment for ML

## 1. Create the Virtual Environment

```bash
mkdir -p /root/code
python3 -m venv /root/code/ml-env
```
Ensure you are in the correct directory


## 2. Activate the environment

```bash
source /root/code/ml-env/bin/activate 
```

## 3. Install the required ML packages

```bash
pip install numpy pandas scikit-learn matplotlib
```
Installed libraries:
- numpy
- pandas
- scikit-learn
- matplotlib

## 4. Generate requirements.txt

```bash
pip freeze > /root/code/requirements.txt
```
## 5. Verify

```bash
cat /root/code/requirements.txt
```
