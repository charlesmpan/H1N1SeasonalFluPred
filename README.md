# Flatiron Phase 3 Project
Charles Pan


## Project Overview

In this project we have been tasked to analyze a data set and come up with our own business problem. The data set I have chosen to tackle was the Seasonal/H1N1 Flu dataset. The business problem I have come up with was to create a predictive model to tell whether a person who has filled out a questionnaire has H1N1 Flu Vaccination or the Seasonal Flu Vaccination. Since the purpose of the project was to use a predictive model over an inferential one, the scenario was that we would be collecting questionnaires and soliciting to those who have filled out the questionnaire and are not predicted to have been vaccinated.


### Approach

We will go attempt to achieve our primary objective in 3 steps.

1. Exploratory Data Analysis (EDA): We will look and analayze the entire data set, and explore the purpose and relation each column has with each other as well as the primary objective. Afterwards, we will trim the unnecessary information, remove or fill null values, investigate correlation through a heat map to see if there were any issues of multicollinearity, and create necessary charts to visually check for anything interesting.

2. Model Testing: We will start creating the pipelines on how to run our data for scalar,  imputating, and encoding. Afterwards, we will start creating the actual models through the pipelines and testing them for their scores, aka precision, recall, accuracy, F-1. The three models I have chosen to test them on for classification were LogisticRegression, KNearestNeighbors, and RandomForests. For those three models, through EDA I was able to see that our data was very skewed on people who were H1N1 vaccinated compared to those who were not; I would say the distribution was around a 20/80 split. Due to that, for the H1N1 prediction models I have also chosen to run another set of test with SMOTE in the pipeline as to represent the minority better. Unfortunately, the models that did not utilize SMOTE performed better than those who did use SMOTE. As for Seasonal Flu prediction models, those did not have any SMOTE as the split was 50/50 for those who were vaccinated and those who ere not. For Seasonal Flu, we also chose to use the same exact prediction modes.

3. Model Selection: At the end, we chose the best performing models for H1N1 and Seasonal Flu prediction and it turned out just LogisticRegression models for both of them. The models used for H1N1 had a lot more differences between them while the models for Seasonal Flu performed quite similarly. For the models we chose, for the sake of the business problem, we focused on precision score over recall score as it was better for the model to predict those who were not vaccinated more accurately as supposed to having false negatives. While False Negatives are generally bad, in this scenario, it would have meant that we were only soliciting to those who were flagged as unvaccinated but were indeed vaccinated. Better safe than sorry.


### The Data

This project used three datasets from the website that this was a competition for. The datasets were test_set_features, training_set_features, and training_set_labels. While the project ahd already pretty much given out a train test split, I wanted to work a bit backwards and also there was no test_set_labels. The labels were crucial in identifying whether the data set output was actually someone who was vaccinated or not. I chose to drop the test_set_features, and just merge the training_set_feature and the training_set_labels into one and run a train-test-split afterwards on it.

The following is the data itself and what it conveys; most of the multicollinearity was between the opinion section.

 0   h1n1_concern                 26615 non-null  float64 - A rating of how concerned someone was of H1N1
 
 1   h1n1_knowledge               26591 non-null  float64 - A rating of how knowledgable someone was of H1N1
 
 2   behavioral_antiviral_meds    26636 non-null  float64 - Whether a person used antiviral meds
 
 3   behavioral_avoidance         26499 non-null  float64 - Whether a person practiced avoidance
 
 4   behavioral_face_mask         26688 non-null  float64 - Whether a person wore a face mask
 
 5   behavioral_wash_hands        26665 non-null  float64 - Whether a person actively washed their hands
 
 6   behavioral_large_gatherings  26620 non-null  float64 - Whether a person attended large gatherings
 
 7   behavioral_outside_home      26625 non-null  float64 - Whether a person goes outside regularly
 
 8   behavioral_touch_face        26579 non-null  float64 - Whether a person touches their face regularly
 
 9   doctor_recc_h1n1             24547 non-null  float64 - Whether a person was recommended H1N1 vaccination by their doctor
 
 10  doctor_recc_seasonal         24547 non-null  float64 - Whether a person was recommended seasonal vaccination by their doctor
 
 11  chronic_med_condition        25736 non-null  float64 - If they have a chronic medical condition
 
 12  child_under_6_months         25887 non-null  float64 - If they have a child under 6 months old
 
 13  health_worker                25903 non-null  float64 - If the person is a health worker
 
 14  health_insurance             14433 non-null  float64 - If the person has health insurance
 
 15  opinion_h1n1_vacc_effective  26316 non-null  float64 - The person's opinion on H1N1 vaccination effectiveness
 
 16  opinion_h1n1_risk            26319 non-null  float64 - The person's opinion on H1N1 vaccionation risk
 
 17  opinion_h1n1_sick_from_vacc  26312 non-null  float64 - The person's opinion whether H1N1 vaccination causes sickness
 
 18  opinion_seas_vacc_effective  26245 non-null  float64 - The person's opinion seasonal flu vaccination effectiveness
 
 19  opinion_seas_risk            26193 non-null  float64 - The person's opinon on seasonal flu vaccination risk
 
 20  opinion_seas_sick_from_vacc  26170 non-null  float64 - The perosn's opinon whether seasonal vaccination causes sickness
 
 21  age_group                    26707 non-null  object - The age group at which they fall under
 
 22  education                    25300 non-null  object - The education which they have received
 
 23  race                         26707 non-null  object - A person's race
 
 24  sex                          26707 non-null  object - A person's sex 
 
 25  income_poverty               22284 non-null  object - A person's income level
 
 26  marital_status               25299 non-null  object - Whether a person is married or not
 
 27  rent_or_own                  24665 non-null  object - Whether a person rents or owns their property
 
 28  employment_status            25244 non-null  object - Whether a person is employed or not
 
 29  hhs_geo_region               26707 non-null  object - Unclear data due to no identifier [Dropped]
 
 30  census_msa                   26707 non-null  object  - Unclear data due to no identifier [Dropped]
 
 31  household_adults             26458 non-null  float64 - How many adults are in the household
 
 32  household_children           26458 non-null  float64 - How many children are in the household
 
 33  employment_industry          13377 non-null  object - Unclear data due to no identifier [Dropped]
 
 34  employment_occupation        13237 non-null  object - Unclear data due to no identifier [Dropped]
 
 35  h1n1_vaccine                 26707 non-null  int64 - Whether a person is H1N1 vaccinated or not
 
 36  seasonal_vaccine             26707 non-null  int64 - Whether a person is seasonal flu vaccinated or not
 


### Findings and Conclusion on the Models

Pipeline Setup: This is to set up the data that will end up becoming essential to creating the models afterwards.

Subpipe_Num = Num_Imputate/StandardScaler [Populates empty values for all columns with numbers and scales]

Subpipe_Cat = Cat_Imputate/OneHotEncoder [Populates empty values for all columns with objects and then encodes it afterwards]

CT = ColumTransformer to Combine the Two Subpipes into One


The H1N1 Logistic Regression Model. [Smote performed worse so it will not be shown]

The following were the gridsearches done to test different outcomes.

params['ct__subpipe_num__num_impute__strategy'] = ['mean', 'median', 'most_frequent']

params['logreg__penalty'] = ['none','l2', 'l1','elasticnet']
params['logreg__solver'] = ['newton-cg','lbfgs','liblinear','sag','saga']
params['logreg__C'] = [100, 10, 1.0, 0.1, 0.01]
The following was the best combination.
{'ct__subpipe_num__num_impute__strategy': 'most_frequent', 'logreg__C': 1.0, 'logreg__penalty': 'l1', 'logreg__solver': 'saga'}
The following is how the model performed. 
Our final model's accuracy on the test set is 0.83. 
Our final model's recall on the test set is 0.42 
Our final model's precision on the test set is 0.68 
Our final model's f1-score on the test is 0.52.

The H1N1 K-Nearest Neighbors Model. [Smote performed worse so it will not be shown]
The following were the gridsearches done to test different outcomes.
params['ct__subpipe_num__num_impute__strategy'] = ['mean', 'median', 'most_frequent']
params['knn__n_neighbors'] = [1,3,5,7,9,11,13,15,17,19,21]
params['knn__weights'] = ['uniform','distance']
params['knn__metric'] = ['euclidean', 'manhattan', 'minkowski']
The following was the best combination.
{'ct__subpipe_num__num_impute__strategy': 'median', 'knn__metric': 'euclidean', 'knn__n_neighbors': 21, 'knn__weights': 'distance'}
The following is how the model performed. 
Our final model's accuracy on the test set is 0.82. 
Our final model's recall on the test set is 0.29 
Our final model's precision on the test set is 0.67 
Our final model's f1-score on the test is 0.41.

The H1N1 Random Forest Classfier Model. [Smote performed worse so it will not be shown]
The following were the gridsearches done to test different outcomes.
params['ct__subpipe_num__num_impute__strategy'] = ['mean', 'median', 'most_frequent']
params['rfc__n_estimators'] = [10,100,1000]
params['rfc__max_features'] = [1,5,10,15,20,'sqrt','log2']
The following was the best combination.
{'ct__subpipe_num__num_impute__strategy': 'median', 'rfc__max_features': 'sqrt', 'rfc__n_estimators': 1000}
The following is how the model performed. 
Our final model's accuracy on the test set is 0.83. 
Our final model's recall on the test set is 0.37 
Our final model's precision on the test set is 0.67 
Our final model's f1-score on the test is 0.48.

The Seasonal Flu Logistic Regression Model.
The following were the gridsearches done to test different outcomes.
params['ct__subpipe_num__num_impute__strategy'] = ['mean', 'median', 'most_frequent']
params['logreg2__penalty'] = ['none','l2', 'l1', 'elasticnet']
params['logreg2__solver'] = ['newton-cg','lbfgs','liblinear','sag','saga']
params['logreg2__C'] = [100, 10, 1.0, 0.1, 0.01]
The following was the best combination.
{'ct__subpipe_num__num_impute__strategy': 'most_frequent', 'logreg2__C': 0.1, 'logreg2__penalty': 'l1', 'logreg2__solver': 'liblinear'}
The following is how the model performed. 
Our final model's accuracy on the test set is 0.77. 
Our final model's recall on the test set is 0.73 
Our final model's precision on the test set is 0.77 
Our final model's f1-score on the test is 0.75.

The Seasonal Flu K-Nearest Neighbors Model.
The following were the gridsearches done to test different outcomes.
params['ct__subpipe_num__num_impute__strategy'] = ['mean', 'median', 'most_frequent']
params['knn__n_neighbors'] = [1,3,5,7,9,11,13,15,17,19,21]
params['knn__weights'] = ['uniform','distance']
params['knn__metric'] = ['euclidean', 'manhattan', 'minkowski']
The following was the best combination.
{'ct__subpipe_num__num_impute__strategy': 'median', 'knn__metric': 'manhattan', 'knn__n_neighbors': 21, 'knn__weights': 'distance'}
The following is how the model performed. 
Our final model's accuracy on the test set is 0.75. 
Our final model's recall on the test set is 0.72 
Our final model's precision on the test set is 0.73 
Our final model's f1-score on the test is 0.73.

The Seasonal Flu Random Forest Classifier.
The following were the gridsearches done to test different outcomes.
params['ct__subpipe_num__num_impute__strategy'] = ['mean', 'median', 'most_frequent']
params['rfc__n_estimators'] = [10,100,1000]
params['rfc__max_features'] = [1,5,10,15,20,'sqrt','log2']
The following was the best combination.
{'ct__subpipe_num__num_impute__strategy': 'most_frequent', 'rfc__max_features': 'log2', 'rfc__n_estimators': 1000}
The following is how the model performed. 
Our final model's accuracy on the test set is 0.77. 
Our final model's recall on the test set is 0.73 
Our final model's precision on the test set is 0.76 
Our final model's f1-score on the test is 0.74.

The Logistic Regression models performed the best and would be the hypothetical ones used in the supposed self-made business problem.

### Wanting to contribute or have any new insights:

If you are interested in contributing to our study (Please don't):
Feel free to give any insights or advice on how things could have been done better or what is misleading/incorrect.

Fork this repository\
Clone your forked repository\
Add your scripts\
Commit and push\
Create a pull request\
Star this repository\
Wait for pull request to merge\
Allow us to review your contribution\

Repository Structure

├── README.md <- The README for this project\
├── Workbook <- Workbook/code for the project
├── P3 <- Presentation for the project
└── Data <- Externally sourced data
