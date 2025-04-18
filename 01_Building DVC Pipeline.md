## Stage-1 Data collection.
- Data collection is done by downloading the file "water_potability.csv" from "https://www.kaggle.com/datasets/uom190346a/water-quality-and-potability".
- Use ps are VScode terminal, create src folder and init
```sh
mkdir src
git init
pip install dvc
pip show dvc
```
- The dvc.exe file will be in the Scripts subdirectory **C:\Users\Lucky Dell\AppData\Roaming\Python\Python312\Scripts**
### Add the Scripts directory to your PATH 
- Open Start → Search for "Edit environment variables" → Open it. 
- Under "System variables", select Path → Click Edit → New. 
- Add the path to the Scripts folder (e.g., C:\Users\Lucky Dell\AppData\Roaming\Python\Python312\Scripts). 
- Click OK → Restart PowerShell.
```sh
dvc --version
dvc init
```
- To develop code
    - Fetch the data
    - Train Test split
    - data, raw
    - train.csv and test.csv
- Install dependencies
```sh
pip install pandas
pip show pandas
pip install -U scikit-learn 
pip show scikit-learn
```
- Once code is developed then create dvc.yml file use the instruction
```sh
src/data_collection.py (this will create data/raw folder) delete it later
cd ..
# dvc stage add -n <stage-name> -d <dependecy location> -o <output location> python <exeutable py file>
# dvc stage add -n <stage-name> -d deps -o outs cmd
dvc stage add -n data_collection -d  src/data_collection.py -o data/raw python src/data_collection.py
```
- To execute the stage of dvc.yaml file
```sh
dvc repro (this will create data and raw folder)
dvc dag (vizualise the pipeline stages)
```

## Stage-2 Data Preparation.
- To develop code
    - Fetch the data form raw folder
    - fill the missing values
    - data, processed
    - train_processed.csv and test_processed.csv
```sh
dvc stage add -n pre_processing -d src/data_preprocessing.py -d data/raw -o data/processed python src/data_preprocessing.py
dvc repro
dvc dag
```
## Stage-3 Feature Engineering.
- In this project we are not going to build Feature Engineering

## Stage-3 Modle Building
- To develop the code
    - Fetch the data from the Preprocessed folder
    - train.csv
    - Random Forest Classifier (Binary classification problem)
    - Save Model
```sh
dvc stage add -n model_build -d src/model_building.py -d data/processed/ -o model.pkl python src/model_building.py  
dvc repro
dvc dag
```

## Stage-4 Model Evaluation
- To develop the code
    - Fetch test data
    - create feature and target
    - load pickle data, calculate target prediction
    - calulate metrics
    - use json to store the metrics
```sh
dvc stage add -n model_evaluation -d src/model_evl.py -d model.pkl --metrics metrics.json python src/model_evl.py
dvc repro
dvc dag
dvc metrics show
```