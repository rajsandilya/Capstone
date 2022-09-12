### Pharmacy Retailer Baseline Price Recommendation System
**Author: Raj Ponukumati**
- - - -
![picture alt](https://github.com/rajsandilya/Capstone/blob/main/images/drug_supply_chain.png "Pharmacy buyer prices")
Reference: https://www.fda.gov/drugs/drug-shortages/graphic-drug-supply-chain-example
- - - -
#### Executive Summary:
 This ML System is developed to help Drug Wholesaler's Sales Representatives or Retail Pharmacy Purchasing Team to analyse drug prices by comparing them to baseline (Medicaid). Medicaid.gov collects approximate invoice prices payed by retail pharmacies for Medicaid patents (Senior citizens, disabled, Pregnant etc), it is called National Average Drug Acquisition Cost (NADAC) dataset.<br>
    These prices are not actual prices payed by patents that are not eligible for Medicaid, which is why this data helps to draw a baseline for comparitive purpuses.In addition to NADAC dataset, a subset of Master Drug Data Base (MDDB) is brought here for cross referring GPID & GPPC grouping and also Wholesale Acquisition Cost (WAC), Average Wholesale Price (AWP).

 * A fine tuned RandomForestRegression model is created to predict prices and utility functions were created to generate reports based on drug groupings GPID & GPPC.  RandomForestRegression model scored 87%.
* Found prices changing with time, hence created a ARIMA time series model to forcast the prices. Since  NADAC dataset is a mixed bag, Time Series alaysis was done on specific groups with good results.

A Drug Wholesaler or retailer can introduce their actual Invoice prices (non-medicaid) and compare with the contry-wide baseline or create models against their actual Invoice prices (non-medicaid). These models will help Wholesaler's while onboarding a retailer and vice versa.

#### Terminology:
 * Types of drugs available:
    * Brands: Patented drugs from manufacturers 
    * Generics: Generic equivalents to brands
    * OTCs (Brands or Generics) : Available Over The Counter without prescription   
 * Prices involved between Manufacturer to Wholesaler
    * Wholesale Acquisition Cost (WAC)
    * Retail Price (To be Sold price to Retailer)
 * Prices involved between Wholesaler to Retailer/ Pharmacy
    * Average Wholesale Price (AWP)
    * Invoice Price (After aplying discounts to Retail Price)
 * What is the difference between GPID and GPPC grouping from MDDB dataset?
    * GPPC is a subset of GPID group ( A group of NDCs )
    * Both GPID and GPPC represent the same Generic drug, it's form and strength.
    * The only difference is GPPC contians package size.
    * A GPID can contain many NDCs with different GPPCs.

#### Rationale:
 Pricing calculations are extremely complex in Pharma world. During the customer onboarding process a Wholesaler is lacking a baseline price predicting model.

#### Research Question:
 Here, I will be creating a baseline price prediction model that will help Wholesaler's sales representatives while onboarding the customers (retail pharmacies).

#### Data Sources:
 * National Average Drug Acquisition Cost (NADAC) from Medicaid.gov 
 * Master Drug Data Base (MDDB)
 ##### Data Preperation for Regression Model:
    * NADAC dataset is split into three Generics, Brands and OTCs subsets 
    * Major analysis is done on Generics subset and MDDB is cross referenced
    * NAN/ NULL colums were dropped from Generics dataset
    * NADAC_Per_Unit is identified as the target column 
    * Feature Collinearity is checked using:
        * Variance Infation Factor, Calculating p-values and checking auto-correlation plots
 - - - -
![picture alt](https://github.com/rajsandilya/Capstone/blob/main/images/feature-correlation.png "Feature Correlation")
- - - -
    * These colums were identified as possible features:
        * NDC Description
        * NADAC_Per_Unit
        * Effective_Date
        * Pricing_Unit
        * Explanation_Code
    * Duplicates columns were dropped from the Generics dataset
    * Data visualizations are used to understand the data 
    

 ##### Data Preperation for Time Series Model:
    * NADAC dataset is split into three Generics, Brands and OTCs subsets 
    * Major analysis is done on Generics subset and MDDB is cross referenced
    * Featues of NADAC dataset used for Time Series ARIMA model are:
        * Effective_Date: Date in MM/DD/YYYY format
        * NADAC_Per_Unit: Invoice price of a given drug identified by NDC
    * Data visualizations are used to understand the time series data and to select AR(p) and MA(q) values
        * Auto correlation
        * Partial auto correlation
        * Seasonal decomposition

#### Methodology:  
 * Modelling is done on large Generics subset
 * Regression Model
    * Ensemble bagging model RandomForestRegressor is used for Modeling
    * Model tuning is done using RandomizedSearchCV
    * Model Evaluation is done by comparing predictions with actual data
    * Metrics used are Mean Squared Error, Max Error and R^2 Score
 * Time Series ARIMA Model:
    * Based on Generic drug grouping GPPC or GPID, Time series analysis is also performed 
    * Stationary datasets were chosen by using Augmented Dickey-Fuller test 
    * Metrics used are Mean Squred Error and Mean Absolute Percentage Error

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
        * Mean Absolute Percentage Error is 18% means model is 82% accurate

    *  Results for GPPC 00959003 Thyroid Tab 15 MG (1/4 Grain) 
        * Historical average predicted invoice price:  0.64
        * Historical average actual invoice price:  0.64
        * Future average forecasted invoice price:  0.56
        * Actual Future average invoice price:  0.52
        * Mean Squared Error: 0.00197842293869437
        * Mean Absolute Percentage Error is 7.7% means model is 92% accurate

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
