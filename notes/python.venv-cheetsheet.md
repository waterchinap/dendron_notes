---
id: nul2wvm4by9lkdoar8os1hw
title: Venv Cheetsheet
desc: ''
updated: 1662565912902
created: 1662565912902
isDir: false
---
## create env

```bash
cd /project/dir
python -m venv envname
```
## activate env 

```shell
source envname/bin/activate
# if use fish
source envname/bin/activate.fish

# list installed packages
pip list

# list one package
pip show pandas
```
## leaving

```bash
deactivate
```
## freeze

```shell
python -m pip freeze
pip freeze > requirements.txt

# install in other place
python -m pip install -r requirements.txt
```