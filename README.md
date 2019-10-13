# typeform : machine learning case

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

## typeform : file structure


## typeform : deployment architecture