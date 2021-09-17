# Pump it Up Challenge

Github Link: https://github.com/Meenu1997/Drivendata_PumpitUp

Competition Link:  https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/

This repo contains the code used for submissions made on the competition Pump it Up: Data Mining the Water Table, hosted on DrivenData.

**Accuracy of best model  : 0.8160**

**Final Rank              : 1781(As of 17th September 2021)**

Following are the steps followed to tackle this problem.

***

## 1) Exploratory Data Analysis
Data was explored initally using the *Pandas* library. 

Then I carried out the analysis as below.
- finding the datatypes of all columns. 7-int columns 3-float columns others are objects
- 7 columns contained missing values
- There were several derived columns
  - quantity / quantity group 
  - water_quality / quality_group
  - payment / pay_type
  - source / source_type / source_class --source has more features
  - management / management_group --management_group has more features
  - extraction_type_class / extraction_type_group / extraction_type
- The recorded_by column only contained one value *GeoData Consultants Ltd* for all ids.
- Longitude column contains null values
- permit and public_meeting column contains boolean value.

***

## 2) Pre-processing and Feature Engineering
The pre-processing steps can be abtracted in the following categories.
- Dropping grouped columns(due to data redundancy and unwanted data) The following columns were dropped.
  - 'region','extraction_type_group','extraction_type_class','management_group','payment','quality_group', 'quantity', 'source_type','source_class',    'waterpoint_type_group',id
- Handling Missing Values and 0 values
  - In the longitude column, the 0 values were replace by the means of the remaining longitude values.
  - The  values of permit and public_meeting were filled with the string values.
  - Overall null values in categorical not filled columns were filled with 'n/a'
  
- Encoding catecorical data columns
- Date columns were replaced with the corresponding epoch values
- recorded by column dropped due to same data for all ids
- id column is dropped as it is unique for all
- Standardize numerical data columns.

***

## 3) Model and Fine-tuning
H2O and CatBoost were tried out.
-  is used to train the data.
- Random-forest was tried with the following parameters,
  - split the training set with 7:3 for training and testing set to check the accuracy.
  - Model was trained with parameters: max_depth=25, n_estimators = 42*5, criterion = 'entropy', random_state = 0
- Note: XGBoost and CatBoost were tried out but did not give good accuracies.

***

## 4) Post-processing

Defined a method plot_features_importances( model, train_data_set)  which  were used to study feature importance. You can refer the notebook in the repo to view the important_features visuals in the notebook



## Proof of submission

DrivenData username: moracse_170620P

![submission](https://github.com/Meenu1997/Drivendata_PumpitUp/blob/main/Proof_of_submission.png)


