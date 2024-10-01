# Project: Predict passenger satisfaction while traveling on the Shinkansen Bullet Train

## Overview

- This project contains Allison Dzubak's submission attempts for the MIT Applied Data Science Program Hackathon competition
- The goal of the problem is to predict whether a passenger was satisfied or not considering their overall experience of traveling on the Shinkansen Bullet Train
- The hackathon evaluation metric is the accuracy score (True Positives + True Negatives) / (Total Observations)
- The uncleaned datasets were provided by the MIT program office with a basic data description
- The hackathon opened March 3, 2024 @ 6AM EST and closed on March 8, 2024 @ 6AM EST

## Data
- Data_Dictionary.xlsx is the data description provided by the MIT program office
- Traveldata_train.csv contains the training data with passenger demographic and travel information
- Traveldata_test.csv contains the test data with passenger demographic and travel information
- Surveydata_train.csv contains the training data with passenger survey responses and target feature
- Surveydata_test.csv contains the test data survey responses without the target feature

## Notebooks
### 0-Exploratory-Data-Analysis.ipynb 
- Explore dataset sizes, structures, features, null/duplicate values, summary statistics
- Perform univariate and bivariate analysis / visualization

### 1-Feature-Map-0-1.ipynb
This notebook contains first round of model testing and the first submission for the Shinkansen MIT Hackathon competition. The submission from this notebook achieved an accuracy of 89.34% on the unknown test dataset.

- Feature set:
  - Perform a mapping of categorical survey quality response data to a 0/1 scale (negative/positive), explore dataset after mapping
  - Create an Avg_Delay feature that averages two highly collinear features: Arrival_Delay, Departure_Delay
  - Drop features: ID, Arrival_Delay, Departure_Delay, Seat_Class, Arrival_Time_Convenient, Platform_Location

- Categorical null values: 
    - Impute with 'unknown'

- Test models, compare classification reports, visualize misclassifications:
  - Model 1:
    - Impute numerical null values with the median
    - Perform random forest classification
  - Model 2: 
    - Impute numerical null values with the median 
    - Perform XGBoost classification
  - Model 3: 
    - Impute numerical null values with matrix completion
    - Perform random forest classification
  - Model 4: 
    - Impute numerical null values with matrix completion
    - Perform XGBoost classification

- Make predictions on test dataset using best performing model (Model 1) and save to submissions directory

### 2-Feature-Map-0-5.ipynb
This notebook contains second round of model testing and the second submission for the Shinkansen MIT Hackathon competition. The submission from this notebook achieved an accuracy of 94.96% on the unknown test dataset.

- Feature set:
  - Perform a mapping of categorical survey quality response data to a 0-5 scale (extremely poor-excellent)
  - Create an Avg_Delay feature that averages two highly collinear features: Arrival_Delay, Departure_Delay
  - Drop features: ID, Arrival_Delay, Departure_Delay

- Categorical null values: 
    - Impute with 'unknown'

- Test models, compare classification reports, visualize misclassifications:
  - Model 1:
    - Impute numerical null values with the median
    - Perform random forest classification
  - Model 2: 
    - Impute numerical null values with the median 
    - Perform XGBoost classification
  - Model 3: 
    - Impute numerical null values with matrix completion
    - Perform random forest classification
  - Model 4: 
    - Impute numerical null values with matrix completion
    - Perform XGBoost classification

- Make predictions on test dataset using best performing model (Model 1) and save to submissions directory

### 3-Avg-Collinear.ipynb
This notebook contains third round of model testing and the third submission for the Shinkansen MIT Hackathon competition. The submission from this notebook achieved an accuracy of 95.44% on the unknown test dataset.

- Feature set 1:
  - Perform a mapping of categorical survey quality response data to a 0-5 scale (extremely poor-excellent)
  - Create an Avg_Delay feature that averages two highly collinear features: Arrival_Delay, Departure_Delay
  - Drop features: ID, Arrival_Delay, Departure_Delay

- Feature set 2:
  - Perform a mapping of categorical survey quality response data to a 0-5 scale (extremely poor-excellent)
  - Create an Avg_Delay feature that averages two highly collinear features: Arrival_Delay, Departure_Delay
  - Create an Avg_Online_Quality feature that averages four semi-collinear features: Online_Boarding, Ease_of_Online_Booking, Online_Support, Onboard_Wifi_Service
  - Create a Seat_Comfort_Catering feature that averages two semi-collinear features: Seat_Comfort, Catering
  - Drop features: ID, Arrival_Delay, Departure_Delay, Online_Boarding, Ease_of_Online_Booking, Online_Support, Onboard_Wifi_Service, Seat_Comfort, Catering

- Null values: 
    - Impute categorical null values with 'unknown'
    - Impute numerical null values with the median

- Test models, compare classification reports, visualize misclassifications:
  - Model 1:
    - Perform XGBoost classification with hyperparameter scan and feature set 1
  - Model 2: 
    - Perform XGBoost classification with hyperparameter scan and feature set 2
  - Model 3: 
    - Perform XGBoost classification using Model 1 with more cv folds

- Make predictions on test dataset using best performing model (Model 3) and save to submissions directory

- Perform feature and misclassification analysis on Model 3


### 4-Feature-Int.ipynb
This notebook contains fourth round of model testing and the fourth submission for the Shinkansen MIT Hackathon competition. The submission from this notebook achieved an accuracy of 95.58% on the unknown test dataset.

- Explore differences between numerical imputation methods

- Null values: 
    - Impute categorical null values with 'unknown'
    - Impute numerical null values with matrix completion

- Feature set 1:
  - Perform a mapping of categorical survey quality response data to a 0-5 scale (extremely poor-excellent)
  - Create an Avg_Delay feature that averages two highly collinear features: Arrival_Delay, Departure_Delay
  - Create interaction term Seat_Ent_Int = Seat_Comfort * Onboard_Entertainment
  - Drop features: ID, Arrival_Delay, Departure_Delay

- Feature set 2:
  - Perform a mapping of categorical survey quality response data to a 0-5 scale (extremely poor-excellent)
  - Create an Avg_Delay feature that averages two highly collinear features: Arrival_Delay, Departure_Delay
  - Create interaction term Quality_Int that is the log of the product of all quality survey response features
  - Create interaction term Quality_Sum that is the sum of all quality survey response features
  - Drop features: ID, Arrival_Delay, Departure_Delay
  
- Feature set 3:
  - Perform a mapping of categorical survey quality response data to a 0-5 scale (extremely poor-excellent)
  - Create an Avg_Delay feature that averages two highly collinear features: Arrival_Delay, Departure_Delay
  - Create interaction term Quality_Int that is the log of the product of all quality survey response features
  - Create interaction term Quality_Sum that is the sum of all quality survey response features
  - Transform Travel_Distance and Avg_Delay by taking the log of each
  - Drop features: ID, Arrival_Delay, Departure_Delay

- Test models, compare classification reports, visualize misclassifications:
  - Model 1:
    - Perform XGBoost classification with hyperparameter scan and feature set 1
  - Model 2: 
    - Perform XGBoost classification with hyperparameter scan and feature set 2
  - Model 3: 
    - Perform XGBoost classification with hyperparameter scan and feature set 3
  - Model 4: 
    - Perform XGBoost classification using Model 1 with more CV folds

- Make predictions on test dataset using best performing model (Model 4) and save to submissions directory

- Perform feature and misclassification analysis on Model 4
- List queries would like to follow up on

## Submissions
- Sample_Submission.csv is the example submission format provided by the MIT program office
- submission_1.csv is the first hackathon submission that achieved an accuracy = 89.34
- submission_2.csv is the second hackathon submission that achieved an accuracy = 94.96
- submission_3.csv is the third hackathon submission that achieved an accuracy = 95.44
- submission_4.csv is the fourth hackathon submission that achieved an accuracy = 95.58



