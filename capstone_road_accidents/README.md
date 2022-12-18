# Capstone Project - Predicting survival outcome in road accidents in France

# Introduction

Road accidents break lives and families. We want to evaluate what are the key factors invovled in survival rate, using data visualization and machine learning to communicate to all road users

## Executive Summary

The purpose of this project is to analyze the key features of road accidents to define a an communication strategy.

We have created and tested different models to predict the outcome of an accident for 3 types of road users:

1. Drivers
2. Passengers
3. Pedestrians

## Problem statement

Can we extract key accident features to protect future road users

## Dataset

Data came from french government open data  [data.gouv.fr]() (https://www.data.gouv.fr/fr/datasets/bases-de-donnees-annuelles-des-accidents-corporels-de-la-circulation-routiere-annees-de-2005-a-2021/)

Each year is represented by 4 tables (people, accident specificities, vehicle and location).

We have chosen years 2019-2021 as our timeframe, **representing 160k accidents and 350k people involved** 

The dataset is heavily imbalanced ( 80% of people being OK and 20% severely injured or dead)

# Project tools

For this project we have explored different data analysis tools

- Using a combination of **SQLite** to aggregate data and manipulate tables,
- **PowerBi** to visualize data before and after EDA
- **Python** for modeling and data manipulation
- **AWS** for to store and fetch our data

# EDA

EDA shown different risks factors depending on road user type, gender and age.

Recap table in PowerBi in the slides

# Features engineering

Lots of missing values

- Dropped

  - all the features with 90% missing values
  - records with less than 100 NaN
- Imputed Missing

  - records with more than 100 NaN
  - mainly using mode ad the visualizations show 95% of the data under 1 class
  - (not extremely informative features)
- Added

  - Date/time
  - Adding public holidays
  - Creating age buckets
  - Creating vehicle type buckets
  - Creating speed limit buckets

# Modeling

We have evaluated 4 classifiers to predict the survival of a given road user.

The choice for these models was

- Relatively easy implementation
- limited choice of parameters for Gridsearch and tuning
- Computationally reasonable
- Models bringing good results

Models evaluated:

1. Logistic regression
2. AdaBoost
3. XGBoost
4. Linear SVC

These 4 models were fitted 3 different datasets (3x4 = 12 ) before and after hypothesis testing and feature selection ( 12 x 2 = 24)

We ended up with 24 fits, evaluated on specificity (how specific are we on the minority class, the precision, and overall accuracy )

# Conclusion

## Recommendations

Drivers

- As expected, safety features and speed limits play a huge part in survival.
- Current debate in France to reduce speed limits on highways to save energy and lives seems perfectly justified
- Debate around driving license validity should happen for drivers beyond age of 60 as we see survival rate decreasing with age

Passengers

- Follow the same recommendations as Drivers
- Younger children are less likely to survive an addicent. Safety features are a must
- Public transport remains the safest option

Pedestrians

- Survival rate is mainly a function of the age
- Accidents almost always happen at crossings.

## Limitations

**Data:** limited view over 3 years. Change in data collection prior 2019 made the data aggregation too difficult. 2020 is not a representative year as accidents and deaths were divided by 1.5 with curfews and lockdowns

**Models** : more models could be evaluated, leveraging Pycaret and cloud computing

**Features** : more features could be collected (speed at point of impact, blood test results (every time someone dies or ends up in hospital, a blood test is conducted on driver).
