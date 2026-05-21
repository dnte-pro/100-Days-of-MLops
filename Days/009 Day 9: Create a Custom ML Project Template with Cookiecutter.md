# Day 9: Create a Custom ML Project Template with Cookiecutter
---
### The Task :
The xFusionCorp Industries ML platform team maintains a Cookiecutter template that new ML projects are generated from. A draft template exists at /root/code/mlops-template/, but it does not render. Correct the template and use it to generate a project.


A Cookiecutter template exists at /root/code/mlops-template/. cookiecutter is installed system-wide.

The corrected template must satisfy every one of the following:

The cookiecutter.json declares four variables:
project_name (default my-ml-project)
author (default xFusionCorp)
python_version (default 3.11)
ml_framework with the choices sklearn, pytorch, and tensorflow
The generated requirements.txt logic:
Contains scikit-learn when ml_framework is sklearn
Contains torch when ml_framework is pytorch
Contains tensorflow when ml_framework is tensorflow
The generated README.md content:
Must reference both the project_name and the author from cookiecutter variables.
The template directory structure {{cookiecutter.project_name}}/ must contain:
Files: README.md and requirements.txt
Directories: data/, models/, src/, and tests/
Review the existing template in the VS Code explorer and correct everything that prevents it from rendering.

Once the template renders, generate a project at /root/code/churn-model/:

   cookiecutter /root/code/mlops-template/ -o /root/code/ --no-input project_name=churn-model ml_framework=sklearn

The generated project must contain a requirements.txt listing scikit-learn and a README.md that mentions xFusionCorp.

---
### What it is about:
The company has a reusable ML project template.

Instead of manually creating:

- folders,
- README files,
- requirements,
- boilerplate structure,

they use Cookiecutter to generate projects automatically.

---
#### What to fix
For the template to render correctly, we need to fix:
- cookiecutter.json
- template variables
- Jinja templating logic
- directory structure
- generated files

1. The cookiecutter.json should contain :
```bash
{
  "project_name": "my-ml-project",
  "author": "xFusionCorp",
  "python_version": "3.11",
  "ml_framework": [
    "sklearn",
    "pytorch",
    "tensorflow"
  ]
}
```

2. The template structure should be as below:
```bash 
{{cookiecutter.project_name}}/
├── README.md
├── requirements.txt
├── data/
├── models/
├── src/
└── tests/
```

3. The README.md should have:
```bash
# {{ cookiecutter.project_name }}

Created by {{ cookiecutter.author }}
```

**Note the 'a' in ```cookiecutter.author```**

4. Confirm the requirements.txt:
```bash
{% if cookiecutter.ml_framework == "sklearn" %}
scikit-learn
{% elif cookiecutter.ml_framework == "pytorch" %}
torch
{% elif cookiecutter.ml_framework == "tensorflow" %}
tensorflow
{% endif %}
```

**The 'endif' is necessary - Without endif, Cookiecutter/Jinja will throw a template parsing error, it is a required syntax**


---
Once the template renders, generate a project at /root/code/churn-model/:
```bash 
cookiecutter /root/code/mlops-template/ -o /root/code/ --no-input project_name=churn-model ml_framework=sklearn
```