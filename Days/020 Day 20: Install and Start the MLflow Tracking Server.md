# Install and Start the MLflow Tracking Server


The xFusionCorp Industries ML team is adopting MLflow for experiment tracking. Your task is to bring up a local MLflow tracking server on the ML pipeline workstation so experiments can be logged from the team's training code.


MLflow 3.x is pre-installed on the controlplane. Launch the tracking server in the background so that every end-state requirement below holds.

The server is listening on port 5000 and is reachable on all interfaces.

The backend store is a SQLite database at /root/code/mlflow-backend/mlflow.db. The database file must exist after the server has started.

The artifact root is /root/code/mlflow-artifacts/.

Any parent directories the server needs must be in place before it starts—MLflow will abort if the backend directory is missing.

The MLflow UI button at the top of the lab must open a responsive dashboard in the browser. The button routes through the lab proxy, so the server must accept requests from any origin (--cors-allowed-origins '*') and any host header (--allowed-hosts '*') to avoid proxy-related rejections.

The server process must persist in the background so it survives terminal closure.


## What this task is about

This task is about setting up an ML experiment tracking service using MLflow. Instead of manually saving model metrics, logs, and artifacts, MLflow provides a centralized server where every training run can be recorded, compared, and visualized through a web UI.

### How to setup

1. Create required directories

MLflow will fail if these don’t exist:

```bash
mkdir -p /root/code/mlflow-backend
mkdir -p /root/code/mlflow-artifacts
```

2. Start MLflow tracking server in background

Use nohup so it survives terminal closure:

```bash
nohup mlflow server \
  --backend-store-uri sqlite:////root/code/mlflow-backend/mlflow.db \
  --default-artifact-root /root/code/mlflow-artifacts \
  --host 0.0.0.0 \
  --port 5000 \
  --serve-artifacts \
  --cors-allowed-origins "*" \
  --allowed-hosts "*" \
  > mlflow.log 2>&1 &
```

3. Verify it is running

```bash
ps aux | grep mlflow
```

4. Confirm backend DB exists

```bash
ls -l /root/code/mlflow-backend/mlflow.db
```

It is created automatically once the server initializes


If it successful, the MLflow ui opens without errors.

![image](https://github.com/user-attachments/assets/06d202f4-dffd-47de-9080-1f06fd6aefb6)