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

Note : if you run load_data.py it will create target .csv file in that case dvc command will fail 

so delete generated files before running below command 


dvc repro
```