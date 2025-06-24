# PA11_2: Project on Used Car Price Prediction & Dealership Inventory Management

_Link to corresponding Jupyter notebook:_
https://github.com/pamelakhalaf/PA11_2/blob/main/code/prompt_II_usedcarprices_PK_Final.ipynb

## Problem Statement 
This project is aimed at understanding what customers value in used car and accordingly put forth recommendations to the client - used car dealership - that is finetuning inventory. With the used car price being the target variable, we run multiple predictive algorithms to understand factors that are most impactful to the used car price. 

## EDA 
### Data Understanding 
The dataset used to address this question is a used car dataset from kaggle consisting of 18 columns/features and 426880 entries. Majority of the features in the dataset are categorical with some including only ~ 3 unique values (e.g. car transmission) whereas others include ~ 30k unique entries (e.g. car model). There are missing values across the dataset with % of missing values for a given feature ranging from none to 72%! The target variable "price" is spread across a wide range with several outliers. 
### Data Cleaning and Preparation
Given that we will be running regression models to predict car prices, we took the following measures to prepare the data for modeling: 
- Eliminated columns that are not relevant to the predictive model or that carry too many values (e.g. car ID, VIN, model and region)
- Eliminated columns with more than 20% of missing values such as cylinder type, size & type of car, paint color etc.
- Renamed column "title_status" to "car_condition" to be more informative.
- Imputed missing values from each feature with the value that made most sense based on the feature characteristics. For example, the odometer & year features are concentrated around the 50% with multiple outliers that can skew the dataset mean, as such we used the median of each feature to impute missing data. Categorical features such as fuel, transmission type and car condition had an apparent most frequent categorical value that was used to impute missing data for each. Lastly, we explored in depth missing data for the manufacturer feature and saw that they are much more likely to be diesel cars with higher probability of them being manufactured by "Ford" vs other manufacturers. As such we imputed the missing values in the manufacturer feature with "Ford".
- Converted categorical features to numerical one so that we can run regression algorithms on them. One hot encoding was used for features with fewer values (car condition, fuel and transmission type) and frequency encoding was used for variables with numerous unique values (manufacturer and state).
- Eliminated rows with price value of 0 as the car can't be free. 
- Converted the price feature to a log scale which took care of the outlier spread.
As a result of all these transformations, the dataset was only reduced down to ~ 390k entries with price as target variable, and 10 features for analysis.  

## Predictive Modeling

## Model Assessment
### Model Evaluation and Comparison 
### Limitations
One could explore increasing treshod 

## Findings & Recommendations 



