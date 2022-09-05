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
 * Given NADAC dataset was split into three Generic, Brand and OTC, major analysis is done on Generics 
 * Correlation matrixs and data visualizations 
 * Ensemble model RandomForestRegressor is used for Modeling
 * Model Evaluation is done by comparing predictions with actual data
 * Metrics used is Mean Squared Error, Max Error and R^2 Score
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
[Capstone Jupyter Notebook](https://github.com/rajsandilya/Capstone/blob/main/Capstone.ipynb)
- - - -

##### Contact and Further Information
* sandilya_raj@yahoo.com
