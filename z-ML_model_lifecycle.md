- Industry follow the ML model lifecycle
1. Model Development- Datascientist & ML engineer  collects data - proprocess data - hyper parameter seclection with different models - get the best possible model.
- Based on the type (classification or regression) evaluate using accuracy, recall, precission f1s or mean_square_error.

2. Model Registry - Identified best model is registered in model registry. It is centrailzed system to manage versions of models, including metadata, stage transtion (development, staging, prodution) and model lineage. 
Model Linage - tracks model journey from developemnt to deployment includes data source, versions, training. By documenting each stage of life cycle it ensure transparency and reproducibility.

3. Model Deployment - MLOPS takes the model and put it in prodution where it makes predicion on live data. Deployment can be done using REST API (python), containers depending on requirement.

4. Monitor and retraining - If the drift is happening due to data patern or model performance retrain and redeploy.