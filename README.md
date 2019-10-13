# typeform : machine learning case : description∫

Create a model to predict the completion rate (defined as submissions/views ) of a form given the features in the dataset.

- Dataset (> 10000 samples) csv file with form_id,submissions,view,features as “-” separated.
- Delivery API and Github repo
- The model with the code and data in the repo and the README file.

Sketch architecture:
- Pipeline running in aws
- Predictions delivered as API call (should be apro 15000 call for minute)
- A robust monitoring and update system for the model.

Please describe briefly each stage - choice of tech at relevant stages of the pipeline.
Please point if any weak points of the choices you have made.

1. Using Python pandas and scypy and SciKit Learn.
2. Use Spark to solve the exercise.
3. Use a simple - not too DNN to solve the exercise (Not to worry about overfitting)

# typeform : machine learning case : delivery

## typeform : delivery details

The way in which the delivery is structured is by using jupyter notebooks to prototype each solution presented. For the notebooks to run you need to copy the original CSV file ("typeform.csv") into the data folder.

note: some models had to be zipped in order to commit them on github (.gz) unzip before use.

There are four major sections (notebooks aka solutions):

1. Python pandas and scypy and SciKit Learn: typeform-ml_case-pandas_sklearn-data.ipynb

- Reading the dataframe "typeform.csv"
- Data cleaning and calculating completion_rate
- Exploratory analysis
- Feature selection
- Model fitting: Linear Regression, Random Forest Regressor
- Model evaluation MAE

The resulting model is in the models folder.
- Linear regression validation MAE =  3.275541339886973
- Random forest validation MAE =  2.9240913766587613


2. SciKit Learn Pipeline: typeform-ml_case-prototype.ipynb

SKlearn Pipeline prototype with SciKit Learn Pipeline ready to deploy

The current pipeline is thouhgt to be ran on a AWS EMR communicating via endponts (as a service) being able to scale as much as you need. (caviat: now it runs reading a file from the filesystem but it's final integration should be with messaging or real-time sqs queues subbscription)

There are three processes:
- Data Processing: where we clean the original dataframe.
- Re-traing: Uses gridsearch for hyperparmeter tunning.
- Prediction: Reads the features and the model and does a prediction.

All it's been integrated on a sample docker container (see prototype folder)


3. Keras Deep Nerural Network: typeform-ml_case-neural_network.ipynb

- Define a sequential model and add some dense layers
- Use ‘relu’ as the activation function for the hidden layers
- Use a ‘normal’ initializer as the kernal_intializer
- Trained using only 10 epochs so it ends in a reasonable time

The resulting model is in the checkpoints folder: Weights-009--2.13214.hdf5
It is the better performming model with MAE: 2.1487201872250994

 
4. PySpark (without pipelines): typeform-ml_case-pyspark.ipynb

Here we perform the data cleaning and model fitting using an spark standalone install. Unfortunately, on the last step, the model training, the spark pipeline breaks.

## typeform : api

To be able to deploy the model as a service an keep track of the different versions we have defined the following API.

```yaml
# ml_case_api.yaml

servers:
  - url: http://api.mlcase.com/v1
    description: endpoint definition for the API
paths:
  /retrain:
    get:
      summary: Returns the S3 url with the retrained model.
      ...
  /predict:
    post:
      summary: Predicts with the actual model based on the payload features.
      ...
```

The .yaml file definition for the REST Api is stored in the <api> folder.

## typeform : deployment architecture (for the pipeline)

When considering a deployment architecture we have to take into account:

A common ML pipeline is 

### typeform : deployment achitecture: without spark


### typeform : deployment achitecture: with spark

### typeform : deployment achitecture: third party solution

Another way to do it can be

### typeform : deployment achitecture: monitoring system

## typeform : prototype (built on sections 2 and 3)

