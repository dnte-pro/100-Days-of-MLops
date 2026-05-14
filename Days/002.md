#  Day 2: Set Up and Configure Jupyter Notebook Server

 A teammate has configured a JupyterLab server for the xFusionCorp Industries data science team, but the server does not behave correctly. Inspect the configuration,  diagnose the issues, and start the server.

 JupyterLab is already installed in the virtual environment at /root/code/ml-env/. The team's configuration file is at /root/code/jupyter_lab_config.py and is visible in the file explorer.

When JupyterLab is started, the Jupyter UI button at the top of the lab must open the notebook interface.

For this to work, the running server must meet the following requirements:

- it listens on port 8888;
- it binds on 0.0.0.0 (the lab proxy cannot reach a server that is only bound on 127.0.0.1);
the notebook root directory is /root/notebooks/, and that directory exists on disk.

- Open the configuration file, identify every setting that prevents the requirements above from being met, and correct it. Create any missing directories.
Start JupyterLab from the virtual environment using the corrected configuration:
``` bash
   source /root/code/ml-env/bin/activate
   jupyter lab --config=/root/code/jupyter_lab_config.py --allow-root --no-browser &
```

Make sure JupyterLab is running before using the button at the top of the lab.
> **Important:** Ensure to change as your lab directs.
---
 # Step-by-step solution

 ## 1. Inspect the Current Configuration
 Open the jupyter config file via the code editor, or via the terminal

- Via the IDE:
        Ensure the configurations in jupyter_lab_config.py are as stated by the instructions.

- Via the terminal;
        Use Vim to edit jupyter_lab_config.py

 ```bash
        vi /root/code/jupyter_lab_config.py
```

---
## 2. Identify the Incorrect Settinngs
Ensure the server has the following configurations:
|     Requirement                |               Value                   |
|--------------------------------|---------------------------------------|
|  Port                          |       < specified port number >       |
|  IP binding                    |       < specified IP >                |
| Notebook directory             |       < specified location >          |

Modify the incorrect lines to be as provided by the instructions


Save and exit after you have made changes

## 3. Create the notebook directory
Create the directory,(The directory is as instructed)

Run
```bash
mkdir -p /root/code/notebooks
```
The verify the directory 
```bash
ls -l /root/code/notebooks
```
## 4. Activate the Python Virtual Environment
Ensure that the virtual environment is activated via the code given:

```bash
source /root/code/ml-env/bin/activate
```
The shell will end with (ml-env)

## 5. Start JupyterLab
To start the jupyterLab run the below code:

```bash
jupyter lab --config=/root/code/jupyter_lab_config.py --allow-root --no-browser &
```
& - makes the code run in the background

## 6. Verifying that JupyterLab is running

Check whether the process is running

```bash
ps -f | grep jupyter
```
Also confirm that the specified port is listening

```bash
ss -tulnp | grep 8888
```
The output should have
```bash
0.0.0.0:8888
```
The output confirms:
  - correct binding
  - correct port