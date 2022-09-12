### Pharmacy Retailer Baseline Price Recommendation System
**Author: Raj Ponukumati**
- - - -
![picture alt](https://github.com/rajsandilya/Capstone/blob/main/images/drug_supply_chain.png "Pharmacy buyer prices")
Reference: https://www.fda.gov/drugs/drug-shortages/graphic-drug-supply-chain-example
- - - -
#### Executive Summary:
 This ML System is developed to help Drug Wholesaler's Sales Representatives or Retail Pharmacy Purchasing Team to analyse drug prices by comparing them to baseline (Medicaid). Medicaid.gov collects approximate invoice prices payed by retail pharmacies for Medicaid patients (Senior citizens, disabled, Pregnant etc), it is called National Average Drug Acquisition Cost (NADAC) dataset.<br>
    These prices are not actual prices payed by patents that are not eligible for Medicaid, which is why this data helps to draw a baseline for comparitive purpuses. In addition to NADAC dataset, a subset of Master Drug Data Base (MDDB) is brought here for cross referring GPID & GPPC grouping and also Wholesale Acquisition Cost (WAC), Average Wholesale Price (AWP).

 * A fine tuned ensemble bagging RandomForestRegression model is developed to predict prices and utility functions were created to generate reports based on drug groupings GPID & GPPC.  RandomForestRegression model scored 87%.
 * Identified specific drug groups, whose prices were changing over time, hence created a ARIMA time series model to forcast the prices. Since NADAC dataset is a mixed bag, Time Series analysis was done on specific groups and obtained good results.

A Drug Wholesaler or Retailer can introduce their actual Invoice prices (non-medicaid) and compare with the country-wide baseline prices or create similar regression models against their actual Invoice prices (non-medicaid). These regression models will help Wholesaler while onboarding a Retailer/Customer and vice versa in contract negotiations. The Time Series model will help Wholesalers and Retailers to forcast prices.

#### Pharma Terminology:
 * Types of drugs available:
    * Brands: Patented drugs from manufacturers 
    * Generics: Generic equivalents of brands
    * OTCs (Brands or Generics) : Available Over The Counter without prescription  
 * NDC : National Drug Code 
    * (11-digit code maintained by the FDA that includes labeler code(first 4-5 digits), product code & package code (last 5 to 6 digits)
 * GPID : Generic Product Identifier
    * 14 Character GPID consists of heirarchy of Drug Group (first 2 chars), Drug Class (first 4 chars), Drug Subclass (first 6 chars), Drug Name(first 8 chars), Drug Name Ext (first 10 chars), Dosage Form (first 12 chars) & Strength (total 14 chars)
 * GPPC : Generic Product Packaging Code
    * 8 character code, The first five characters are random and last three represent Package Description, Package Size, Package Size unit of Measure, Package Quantity and Unit Dose / Unit of Use Packaging Code
 * What is the difference between GPID and GPPC grouping from MDDB dataset?
    * GPPC is a subset of GPID group ( A group of drugs with unique NDCs )
    * Both GPID and GPPC represent the same Generic drug, it's form and strength.
    * The only difference is GPPC contians packing information: size & codes.
    * A GPID can contain many NDCs with different GPPCs.
 * Prices involved between Manufacturer to Wholesaler
    * Wholesale Acquisition Cost (WAC)
    * Retail Price (To be Sold price to Retailer)
 * Prices involved between Wholesaler to Retailer/ Pharmacy
    * Average Wholesale Price (AWP)
    * Invoice Price (After aplying discounts to Retail Price)
 * References:
    * https://data.medicaid.gov/dataset/dfa2ab14-06c2-457a-9e36-5cb6d80f8d93
    * https://dhhr.wv.gov/bms/BMS%20Pharmacy/Documents/NADAC%20Survey.pdf
    * https://github.com/rajsandilya/Capstone/blob/main/docs/nadacdatadefinitions.pdf
    * https://github.com/rajsandilya/Capstone/blob/main/docs/BUS_fact_sheet.pdf
    * https://github.com/rajsandilya/Capstone/blob/main/docs/nadacmethodology.pdf


#### Rationale:
 Pricing calculations are extremely complex in Pharma world. During the customer onboarding process a Wholesaler is lacking a baseline price predicting model.

#### Research Question:
 In this project, I will be creating a baseline price prediction model that will help Wholesaler's sales representatives in contract negotiations while onboarding the customers (retail pharmacies).

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
    * Effective_Date
    * Pricing_Unit
    * Explanation_Code
 * Duplicates columns were dropped from the Generics dataset
 * Data visualizations are used to understand the data 
 * OneHot Encoder created many columns of NDC Description, hence Label Encoder is used to encode the non-numeric features: 
    * NDC Description, Effective_Date, Explanation_Code, Pricing_Unit 

 ##### Data Preperation for Time Series Model:<br>
 * NADAC dataset is split into three Generics, Brands and OTCs subsets. 
 * Major analysis is done on Generics subset and MDDB is cross referenced.
 * Featues of NADAC dataset used for Time Series ARIMA model are:
    * Effective_Date: Date in MM/DD/YYYY format
    * NADAC_Per_Unit: Invoice price of a given drug identified by NDC.
    * Data visualizations are used to understand the time series data and to select AR(p) and MA(q) values:
        * Auto correlation
        * Partial auto correlation
        * Seasonal decomposition

#### Methodology:  
 * Modelling is done on Generics subset.
 * Sequencial Feature Selection and Column permutation Imporatance are used to select features.
 * Regression Model
    * Linear Regression, Lasso and Ridge models gave very low scores. 
    * Ensemble bagging model RandomForestRegressor is used for Modeling.
    * Model tuning is done using RandomizedSearchCV.
    * Model Evaluation is done by comparing predictions with actual data.
    * Metrics used are Mean Squared Error, Max Error and R^2 Score.
 * Time Series ARIMA Model:
    * Based on Generic drug grouping GPPC or GPID, Time series analysis is also performed .
    * Stationary datasets were chosen by using Augmented Dickey-Fuller test. 
    * Metrics used are Mean Squred Error and Mean Absolute Percentage Error.

#### Results:
* RandomForestRegressor Model prediction score is 87%
* RandomForestRegressor Model Metrics:
    * Mean Squared Error: 24.9
    * Max Error: 278.03
    * r2_score : 0.88

* Time Series ARIMA Model predictions were done on specific groups:
    * Results for GPID 65100075102005 Oxycodone HCl Soln 5 MG/5ML
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
* Email: sandilya_raj@yahoo.com

##### Moving on to Next Steps:
* Create two reusable python classses 1) For Regression model 2) For Time Series Model and bring in all functions mentioned in the notebooks
* Natural Language Processing:
    * Work on NADAF dataset by splitting NDC description column into new columns Generic name, Strength & Form, NLP can be utilized for this task. These new columns might increase our regression model score.
    * To create Chat bot that recommends medication when illness is entered (Use NLP & Classification)
* Classification:
    * Convert this into a classification model by bringing Therapuetic categories
        * This Classification model should classify a drug name to its theraputic category
        * Example: Metformin or Biguanides (Group) -> Diabetis type 2 (Illness)
* For Time Series analysis:
    * Split the Effective_Date column into Year, Month and Day columns, so that Time Series analysis can be done on a granular level.
    * Explore LSTM models