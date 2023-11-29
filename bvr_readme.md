Create environment

```bash 
    conda create -n wineq python=3.8 -y
   21  conda activate wineq
   
   
```

Create requirements.txt

```

touch requirements.txt


dvc
dvc[gdrive]
scikit-learn


pip install -r requirements.txt

```


```
python template.py
```

```
download winequality.csv file from https://drive.google.com/drive/folders/18zqQiCJVgF7uzXgfbIJ-04zgz1ItNfF5?usp=sharing


mkdir data_given

copy winequality.csv to data_given folder 
```


```
 32  git init
   33  dvc init
   34  dvc add data_given/winequality.csv
   35  git add .
   36  git commit -m "first commit"
   
```

```
 38  git add . && git commit -m "updated Read me file"
   39  git remote add origin https://github.com/vishymails/mlops_nov2023.git
   40   git branch -M main
   41    git push -u origin main
```


```
update params.yaml

git add . && git commit -m "added params.yaml"
git push -u origin main
```


```
create get_data.py
create load_data.py

```

```
update dvc.yaml

stages :
  load_data :
    cmd : python src/load_data.py --config=params.yaml
    deps :
      - src/get_data.py
      - src/load_data.py
      - data_given/winequality.csv
    outs :
      - data/raw/winequality.csv
```

``` update requirements.txt

dvc
dvc[gdrive]
scikit-learn
pandas
pytest
tox
flake8
flask
gunicorn


```


```
pip install requirements.txt
```

```
If require run independent programs 

python get_data.py (make sure you remove commented syntax in the program to see result)

Note : if you run load_data.py it will create target .csv file in that case dvc command will fail 

so delete generated files before running below command 


dvc repro
```


``` update split_data stage in dvc.yaml

split_data :
    cmd : python src/split_data.py --config=params.yaml
    deps : 
      - src/split_data.py
      - data/raw/winequality.csv
    outs :
      - data/processed/train_winequality.csv
      - data/processed/test_winequality.csv

CREATE SPLIT_DATA.PY
```


``` 
   69  git add . && git commit -m "SPLIT_DATA STAGE ADDED"
   70  git push origin main
 ```

```
   83  mkdir report
   84  touch report/params.json
   85  touch report/scores.json
   
```

```
add to train_and_evaluate in dvc.yaml

metrics :
      - report/scores.json :
          cache : false
      - report/params.json :
          cache : false


```

```
FINAL COPY 


train_and_evaluate :
    cmd : python src/train_and_evaluate.py --config=params.yaml
    deps :
      - data/processed/train_winequality.csv
      - data/processed/test_winequality.csv
      - src/train_and_evaluate.py
    params :
      - estimators.ElasticNet.params.alpha
      - estimators.ElasticNet.params.l1_ratio
    metrics :
      - report/scores.json :
          cache : false
      - report/params.json :
          cache : false
      
    outs :
      - saved_models/model.joblib
```

```
   86  dvc repro
   
```

```
   88  dvc params diff
   89  dvc metrics show
   91  dvc metrics diff
   92  git add . && git commit -m "Tracker added"
   93  git push origin main

```


``` Update params.yaml file 

estimators :
  ElasticNet :
    params :
      #alpha : 0.88
      #l1_ratio : 0.11
      alpha : 0.9
      l1_ratio : 0.4

```

```
git add . && git commit -m "Tracker added"
   96  git push origin main
   97  git push origin main
   98  dvc repro
   99  dvc metrics diff
  100  dvc metrics show
  101  git add . && git commit -m "Tracker added"
  102  git push origin main
  103  dvc metrics diff
  104  dvc metrics show
```


```
Create setup.py 

from setuptools import setup, find_packages

setup(
    name = "src",
    version="0.0.1",
    description="Case study project for Oracle India",
    author="BVR", 
    packages=find_packages(),
    license="MIT"

)

```

```
118  tox
  119  tox -r 
  120  pip install -e .
  121  pip freeze
  122  python setup.py sdist bdist_wheel
  123  history
```