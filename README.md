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
 * Correlation matrixs and data visualizations 
 * Ensemble model RandomForestRegressor is used for Modeling
 * Model Evaluation is done by comparing predictions with actual data
 * Metrics used is Mean Squared Error, Max Error and R^2 Score

#### Results:
* Model prediction accuracy for both train and test samples is 99%

#### Outline of project
 - - - -
[Capstone Jupyter Notebook](https://github.com/rajsandilya/Capstone/blob/main/Capstone.ipynb)
- - - -

##### Contact and Further Information
* sandilya_raj@yahoo.com
