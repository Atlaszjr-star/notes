---
tags: [PyGUI, python]
title: 01 Installation for Python GUI Programming in windows system env or conda
created: '2022-05-09T21:28:26.831Z'
modified: '2022-05-10T09:55:06.719Z'
---

# 01 Installation for Python GUI Programming in windows system env or conda 

1. Create new venv in conda and activate
```shell
conda create -n venv_name python=x.x 
conda activate venv_name
```
2. Install pyqt5, pyqt5-tools, pyinstaller in venv 
```shell
pip install pyqt5
pip install pyqt5-tools
pip install pyinstaller
pip/conda install other_package_you_need
```
3. Path to your application dir, normally run
```shell
pyinstaller app.py
``` 
- But sometimes after running complied app.exe show a command windows then immediately disapperar, since it's very common that somtimes pyinstaller won't recognize all Qt5 dependencies especially Qt5Core.dll, A simple way is to just locate file on your python path(or conda) and feed it with add-data flag.
  
- if you are using your python path:
  ```shell
  pyinstaller --noupx -F --add-data "<Python path>/lib/site-packages/PyQt5/Qt5/bin/Qt5Core.dll;./PyQt5/Qt5/bin" app.py
  ```
- if you are using conda venv:
  ```shell
  pyinstaller --noupx -F --add-data "c:/users/user_name/anaconda3/envs/venv_name/lib/site-packages/PyQt5/Qt5/bin/Qt5Core.dll;./PyQt5/Qt5/bin" app.py
  ```
4. Finally you can run the app.exe in the folder /dist



