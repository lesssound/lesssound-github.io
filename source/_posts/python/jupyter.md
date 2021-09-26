---
title: jupyter 
categories:
  - python
date: 2021-07-17 11:25:43
tags:
---


```python

# jupyter config
pip install jupyter
jupyter notebook --generate-config

### ipython
from notebook.auth import passwd
passwd()
## or
jupyter notebook password

vim ~/.jupyter/jupyter_notebook_config.py 

c.NotebookApp.ip='*'
c.NotebookApp.password = u''
c.NotebookApp.open_browser = False
c.NotebookApp.port = 8000

jupyter notebook
```
