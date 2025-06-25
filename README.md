# PA11_2: Project on Used Car Price Prediction & Dealership Inventory Management

_Link to corresponding Jupyter notebook:_
https://github.com/pamelakhalaf/PA11_2/blob/main/code/prompt_II_usedcarprices_PK_Final.ipynb

## Problem Statement 
This project is aimed at understanding what customers value in used car and accordingly put forth recommendations to the client - used car dealership - that is fine-tuning inventory. With the used car price being the target variable, we run multiple predictive algorithms to understand factors that are most impactful to the used car price. 

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
Prior to running regression models, the data was scaled with the exception of price (already transformed to log scale) and the one hot encoded features as they were already binary. 
The data was split into training and testing subsets (with test size being 30%). Then three regression algorithms were explored separatly: linear regression, ridge regression and lasso regression. For the ridge and lasso regression models, gridsearchCV was leveraged for parameter tuning and identifying the optimal alpha. 

## Model Assessment
### Model Evaluation and Comparison 
The optimal alpha values returned by the ridge and lasso regression models were very small (0 for lasso) suggesting that the models were behaving as linear regression models. This was further confirmed when exploring the performance of these models and comparing train and test RMSE, test MAE and R2 score for each model. The models performed very similarly suggesting that regularization in the case of this dataset does not add value to the performance of the model. As such, we anchored to the linear regression model and explored the output coefficients of the fitted model to evaluate the impact of each used car feature on its price. 

## Findings & Recommendations 
As our client (used car dealership) is looking to fine tune their inventory, we will first highlight used car features that were identified through the model to impact the price of a car (positively and negatively). We then accordingly, recommend few strategies to fine tune their inventory assuming they want to focus on cars that will sell at higher prices. 

_What impacts the price of a car?_

Factors that increase the price of a car include:
- Year of production: for every additional year in the car's model year, the price of the used car increases by ~ 28%
- Transmission type (other than automatic and manual): these cars are 76% more expensive than cars with more common transmission types
- Manufacturer frequency: cars of more frequent manufacturers are 7% more expensive
- Car condition lien: these financed cars tend to be 24% more expensive when compared to clean cars 

Factors that decrease the price of a car include:
- Certain car conditions relative to clean cars: cars with parts only are 83% cheaper, those with missing parts are 55% cheaper, salvage cars are 39% cheaper and rebuilt cars are 15% cheaper relative to clean cars
- Fuel type: hybrid, gas and electric cars are 61%, 57% and 48% cheaper respectively relative to diesel cars
- Odometer: Higher mileage reduces price by 12% of each mileage increase
- State: states with more frequent cars tend to drive prices slightly lower by 3%

Biggest swing factors in the price of a used car include cars that have used parts only or missing parts (relative to clean cars), those with transmission type other than manual/automatic, and having fuel type other than diesel. 

_Final Recommendation:_
From an inventory management perspective, and to maximise value for your cars, focus on newer used cars especially those with "clean" condition. Other car conditions will significantly reduce sale value.
Mileage is impactful and it is recommended to keep cars with lower mileage.
Lastly, keep in mind that transmission types other than automatic & manual could signficantly raise the sale price while hybrid and electric cars have been selling at lower price (compared to diesel). 
