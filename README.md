### Pharmacy Retailer baseline Invoice Price Recommendation System
**Author: Raj Ponukumati**
- - - -
![picture alt](https://github.com/rajsandilya/Capstone/blob/main/images/drug_supply_chain.png "Pharmacy buyer prices")
Reference: https://www.fda.gov/drugs/drug-shortages/graphic-drug-supply-chain-example
- - - -
#### Executive Summary: This System is developed to help Wholesaler's Sales Representatives or Retail Pharmacy Purchasing Team to analyse drug prices by comparing them to baseline (Medicaid)

#### Rationale: Pricing calculations are extremely complex in Pharma world. During the customer onboarding process a Wholesaler is lacking a baseline price predicting model.

#### Research Question: Here, I will be creating a baseline price prediction model that will help Wholesaler's sales representatives while onboarding the customers (retail pharmacies).

#### Data Sources: NADAC from Medicaid.gov and Master Drug Data Base (MDDB)

#### Methodology:  
 * Modeling is done on NADAC (National Average Drug Acquisition Cost) Dataset from Medicaid.gov
 * Exploratory Data Analysis
 * Given NADAC dataset is split into three Generics, Brands and OTCs subsets
 * Major analysis is done on Generics subset
 * Data visualizations are used to understand the data 
 * Ensemble bagging model RandomForestRegressor is used for Modeling
 * Model tuning is done using RandomizedSearchCV
 * Model Evaluation is done by comparing predictions with actual data
 * Metrics used are Mean Squared Error, Max Error and R^2 Score
 * Based on Generic drug grouping GPPC or GPID, Time sereis analysis is also performed 

#### Results:
* RandomForestRegressor Model prediction scores against training set is 99% and test set is 87%
* RandomForestRegressor Model Metrics:
    * Mean Squared Error: 24.9
    * Max Error: 278.03
    * r2_score : 0.88

* Time Series ARIMA Model predictions were done on specific groups
    * Results on GPID 65100080100305 (Oxymorphone HCl Tab 5 MG)
        * Historical average invoice price:  0.512721087985516 
        * Future average invoice price:  0.5395697904917949
        * Mean Squared Error 0.0007334907676462974

#### Outline of project
 - - - -
[Capstone Main Jupyter Notebook](https://github.com/rajsandilya/Capstone/blob/main/Capstone.ipynb)
<br>
[Time Series Jupyter Notebook](https://github.com/rajsandilya/Capstone/blob/main/Timeseries.ipynb)
- - - -

##### Contact and Further Information
##### Next Steps:
* Create two reusable python classses 1) For Regression model 2) For Time Series Model and bring in all functions mentioned in the notebooks
* Work on NADAF dataset by splitting NDC description column into new columns Generic name, Strength & Form, NLP Can be used for this task. These new columns might help our regression model.
* To create chat bot that recommends medication when illness is entered (Use NLP)
* Convert this into a classification model by bringing Therapuetic categories
    * This Classification model should classify a drug name to its theraputic category
    * Example: Metformin -> Diabetis

* sandilya_raj@yahoo.com
