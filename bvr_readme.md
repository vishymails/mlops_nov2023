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

