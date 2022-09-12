### Pharmacy Retailer Baseline Price Recommendation System
**Author: Raj Ponukumati**
- - - -
![picture alt](https://github.com/rajsandilya/Capstone/blob/main/images/drug_supply_chain.png "Pharmacy buyer prices")
Reference: https://www.fda.gov/drugs/drug-shortages/graphic-drug-supply-chain-example
- - - -
#### Executive Summary:
 This ML System is developed to help Drug Wholesaler's Sales Representatives or Retail Pharmacy Purchasing Team to analyse drug prices by comparing them to baseline (Medicaid). Medicaid.gov collects approximate invoice prices payed by retail pharmacies for Medicaid patents (Senior citizens, disabled, Pregnant etc), it is called National Average Drug Acquisition Cost (NADAC) dataset.
 These prices are not actual prices payed by patents that are not eligible for Medicaid, but this data helps to draw a baseline for comparitive purpuses.
 In addition to NADAC dataset, a subset of Master Drug Data Base (MDDB) is brought here for cross referring GPID & GPPC grouping and also Wholesale Acquisition Cost (WAC), Awerage Wholesale Price (AWP).
    * A fine tuned RandomForestRegression model is created to predict prices and utility functions were created to generate reports based on drug groupings GPID & GPPC. 
    RandomForestRegression model scored 87%.
    * Found prices changing with time, hence created a ARIMA time series model to forcast the prices. Since NADAC dataset is a mixed bag, Time Series alaysis was done on specific groups with good results.


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

* Time Series ARIMA Model predictions were done on specific groups:
    * Results for GPID 65100080100305 (Oxymorphone HCl Tab 5 MG)
        * Historical average predicted invoice price:  0.11
        * Historical average actual invoice price:  0.11
        * Future average forecasted invoice price:  0.11
        * Actual Future average invoice price:  0.1
        * Mean Squared Error: 0.0004266289208173572

    *  Results for GPPC 00959003 Thyroid Tab 15 MG (1/4 Grain) 
        * Historical average predicted invoice price:  0.64
        * Historical average actual invoice price:  0.64
        * Future average forecasted invoice price:  0.56
        * Actual Future average invoice price:  0.52
        * Mean Squared Error: 0.00197842293869437

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
