# Project 2 - Ames Housing Data and Kaggle Challenge

## Problem Statement

To assist potential house owner, house investors or property agents to find out key variables that will affect the price of homes for the Ames Iowa Housing

- The key idea is to find out what are the key variables to collect for valuation of the houses.
- The original dataset contains 80 features describing the house. 
- The most important features that determine the Sale Price: Living Area Above Gound, The Neighbourhood, The Overall (Quality and Condition) of the house, The Garage Score(Garage Finish, Garage Cars and Garage Area) and  The Basement Score (Types of Finishes on the Basement, The Square Footage and The Quality)
- We will be using Linear Regression, Ridge, Lasso, Elastic Net Models which will be evaluated using R^2  and RMSE metrics.

### Target Audience
We are group of property valuators, specialising in valuating property prices in the City of Ames. Be it potential house owner, house investors or property agents, using this tool will ensure that the buyers and sellers receives fair valuation on the house based on the required variables. This will also allow them to know the key indicators that will affect the valuation of the houses.

## Datasets

- There are two datasets train.csv which will be used to build our model and test.csv which will be used solely on getting a prediction with our model.
- There are total of 81 columns in the train.csv file which includes the SalePrice and 80 columns in the test.csv file which does not have the SalePrice column.
- The data dictionary for the datasets could be found [here.](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt)


## Summary of Data Cleaning - Train Dataset

|No.| Columns with Missing Data |Remedy |Reason|
|---|---|---|---|
|1.|Lot Frontage| Mode Imputing|16.09% Of Missing Data
|2.|Alley| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Alley'|
|3.|Mas Vnr Type| Mode Imputing|1.07% Of Missing Data
|4.|Mas Vnr Area| Mode Imputing|1.07% Of Missing Data
|5.|Bsmt Qual| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Basement'|
|6.|Bsmt Cond| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Basement'|
|7.|Bsmt Exposure| Renaming from 'NA' to 'None', Drop Row #1456, #1547, #1997|As Per Dataset Description, NA means 'No Basement', Rows of missing data is dropped|
|8.|BsmtFin Type 1| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Basement'|
|9.|BsmtFin SF 1| Drop Row #1327|Missing Data in Column Resolved|
|10.|BsmtFin Type 2| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Basement'|
|11.|BsmtFin SF 2| Drop Row #1327|Missing Data in Column Resolved|
|12.|Bsmt Unf SF| Drop Row #1327|Missing Data in Column Resolved|
|13.|Total Bsmt SF| Drop Row #1327|Missing Data in Column Resolved|
|14.|Bsmt Full Bath| Drop Row #616, #1327|Missing Data in Column Resolved|
|15.|Bsmt Half Bath| Drop Row #616, #1327|Missing Data in Column Resolved|
|16.|Fireplace Qu| Renaming from 'NA' to 'None'| As Per Dataset Description, NA means 'No Fireplace'|
|17.|Garage Type| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Garage'|
|18.|Garage Yr Blt| Renaming from 'NA' to '0', Drop Row #1712, Drop Row #1699|As Per Dataset Description, NA means 'No Garage',Missing data in Row #1712, Wrong year in Row #1699|
|19.|Garage Finish| Renaming from 'NA' to 'None', Drop Row #1712|As Per Dataset Description, NA means 'No Garage'|
|20.|Garage Cars| Drop Row #1712|Missing Data in Column Resolved|
|21.|Garage Area| Drop Row #1712|Missing Data in Column Resolved|
|22.|Garage Qual| Renaming from 'NA' to 'None', Drop Row #1712|As Per Dataset Description, NA means 'No Garage'|
|23.|Garage Cond| Renaming from 'NA' to 'None', Drop Row #1712|As Per Dataset Description, NA means 'No Garage'|
|24.|Pool QC| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Pool'|
|25.|Fence| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Fence'|
|26.|Misc Feature|Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Misc Feature'|

## Summary of Data Cleaning - Test Dataset

|No.| Columns with Missing Data | Remedy |Reason|
|---|---|---|---|
|1.|Lot Frontage| Imputation using Mode| Rebuilding of Data|
|2.|Alley| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Alley'|
|3.|Mas Vnr Type| Using SimpleImpute - Mode for Row #864| Variable is not normally distributed|
|4.|Mas Vnr Area| Using SimpleImpute - Mode for Row #864| Variable is not normally distributed|
|5.|Bsmt Qual| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Basement'|
|6.|Bsmt Cond| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Basement'|
|7.|Bsmt Exposure| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Basement'|
|8.|BsmtFin Type 1| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Basement'|
|9.|BsmtFin Type 2| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Basement'|
|10.|Electrical| Using SimpleImputing - Mode for Row #634| Missing Data - 1 Row|
|11.|Fireplace Qu| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Fireplace'|
|12.|Garage Type| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Garage'|
|13.|Garage Yr Blt|Missing Data are all '0' + For Row #764 use 1983|As Per Dataset Description, 0 means 'No Garage' + Assume that Year the house remodeled is Year Garage was built|
|14.|Garage Finish| Renaming from 'NA' to 'None', For Row #764 use 'Unf' |As Per Dataset Description, NA means 'No Garage', Use Mode with similar garage type|
|15.|Garage Qual| Renaming from 'NA' to 'None' + For Row #764 use 'TA' |As Per Dataset Description, NA means 'No Garage', Use Mode with similar garage type|
|16.|Garage Cond| Renaming from 'NA' to 'None' + For Row #764 use 'TA'|As Per Dataset Description, NA means 'No Garage', Use Mode with similar garage type|
|17.|Pool QC| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Pool'|
|18.|Fence| Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Fence'|
|19.|Misc Feature|Renaming from 'NA' to 'None'|As Per Dataset Description, NA means 'No Misc Feature'|

## EDA

The distribution of house prices is right-skewed with the average price of houses being \$181,402. 50\% of the houses are priced between \$129,725 and $214,000.

Continuous Variables

- 'Gr Liv Area' is the summation of '1st Flr SF', '2nd Flr SF' and 'Low Qual Fin SF'.
- The 1st Floor SF(0.621) has good correlation with Sale price and 2nd Floor SF(0.250) and Low Qual Fin SF(-0.04) has some correlation with the the Sale price.

- Looking into the individual correlation values, 'Full Bath'(0.538) has the highest correlation with the sales price, however the other variables such as 'Bsmt Full Bath'(0.285), Bsmt Half Bath'(-0.045), 'Half Bath'(0.283) has poor or no correlation.

- 'Total Bsmt SF' is the summation of 'BsmtFin SF 1' and 'BsmtFin SF 2'.
- Only 'Total Bsmt SF'(0.632) has good correlation with the 'SalePrice'.
- The is some correlation of the 'BsmtFin SF 1'(0.425) with 'SalePrice' and almost no correlation with 'Bsmt Unf SF'(0.190) and 'BsmtFin SF 2'(0.017) the 'SalePrice'.

- 'Garage Cars'(0.642) and 'Garage Area'(0.650) has good correlation with the SalePrice.

- 'Wood Deck SF'(0.327) and 'Open Porch SF'(0.333) have a poor correlation with the SalePrice.
- 'Enclosed Porch'(-0.135), '3Ssn Porch'(0.489) and 'Screen Porch'(0.135) have almost no correlation with Sale Price

- Looking into the dates relation with the SalePrice, 'Year Built'(0.572) and 'Year Remod/Add'(0.550) has some correlation with the SalePrice but not for 'Mo Sold'(0.032) and 'Yr Sold'(-0.015). 

Some Continuous varaibles have similar relation with each other which should be eliminated and some should be combined with categorical variables.

Categorical Variables
Nominal Variables 
- Most of the nominal variables has some variety in the spread of data versus Sale Price. This would be suitable to see the difference with encoding (Get_dummies) applied.

Ordinal Variables
- Most of the ordinal variables seems to indicate there is a relationship with the Sale Price with the order.
- There are three columns that does not have much variation.
- Lot Shape
- Utilities
- Fence
- The Ordinal Variables will be encoded using OrdinalEncoder which put the variables into types with order.

## Feature Engineering
- Some of the features should be combined due to multicollinearity which should be combined to prevent overfitting
- Outliers were also identified and removed from the dataset to improve the linearity of the model.

1. Overall - Overall Qual * Overall Cond
- This will give the overall score for the house. Correlation: 0.565
2. Above Area - 1st Flr SF + 2nd Flr SF + 0.5 * Low Qual Fin SF. Correlation: 0.703
- The low quality finish SF is given a penalty value of 0.5.
- This new variable will replace the Gr Liv Area
3. TotalBath - Bsmt Full Bath + 0.5 * Bsmt Half Bath + Full Bath + 0.5 * Half Bath. Correlation: 0.632
- Half bath are considered half of full bath, thus penalty value of 0.5.
4. Basement - (BsmtFin Type 1 * BsmtFin SF 1 + BsmtFin Type 2 * BsmtFin SF 2 + Bsmt Unf SF) * Bsmt Qual * Bsmt Cond
- Since the Basement Finishes have been coded to follow and Ordinal Order, thus 'Bsmt Unf SF' by the order would have a value of 1. We then multiply it with Quality and Condition to give it an overall score of the Basement.
5. Garage - Garage Finish * Garage Qual * Garage Cond * Garage Area. Correlation: 0.658
- Since Garage Cars and Garage Area mesures the area of the garage, we can drop either of them. In this case 'Garage Cars' will be dropped.
- This new variable will give an overall score on the Garage.
6. Outdoor - Wood Deck SF + Open Porch SF + Enclosed Porch + 3Ssn Porch + Screen Porch. Correlation: 0.410
- The size of the outdoor area are added together since invidually they do not provide much correlation with the Sale Price. 
7. Age  
a) The age of the house shall be recomputed by using 'Yr Sold' - 'Year Built'.
- Correlation value of age vs SalePrice: -0.572  
b) The years since remodelling, additions or constructed can be taken into account by taking 'Yr Sold' - 'Year Remod/Add'
- Correlation value of years since Remod/Add vs SalePrice: -0.551
- 'Yr Sold' and 'Mo Sold' shall be changed to categorical variables. This is due to in economic crisis years, house prices could be lower.  
c) Garage Yr Blt does not value add much to the output and this only has a correlation value of 0.259.  
From the Garage Score we have computed earlier takes into account of the size of the 'Garage Area' it would not be wise to have another penalty term for Garage Yr Blt = 0. Thus this variable shall be dropped.


## Single Variable Dominated variables

- Since these columns have more than 80% of a single feature, there will not be much variation to the sale price.
- Thus the following columns have been dropped: Alley, Land Contour, Utilities, Land Slope, Condition 1, Condition 2, Bldg Type, Exter Cond, Heating, Central Air, Electrical, Functional, Paved Drive, Pool QC, Fence, Misc Feature, Sale Type

## Identifier Columns cannot be used in computation, thus they will be removed
| Columns (Identifier) | Remedy |Reason|
|---|---|---|
|Id| Drop Column|Identifier|
|PID| Drop Column|Identifier|


## Model Evaluation and Selection

We will be using regression models since Sale Price is a continuous variable. The models that we will evaluate are the Linear Regression, Ridge and Lasso models. We will utilise a RMSE and R-squared metric score to identify the best regression model between the four.

**Summary of Scores of Model**

|Base Model | R^2 - Train| R^2 - Test |RMSE|Alpha|L1|
|---|---|---|---|---|---|
|Linear Regression|0.928 |-4.95e+23|5.27e+16|-|-|
|RidgeCV|0.927|0.901|23581.64|58.57|-|
|LassoCV|0.929|0.891|24712.15|1|-|
|ElasticCV|0.926|0.901|23489.14|0.980|0.955|

Linear Regression model did not work in our modelling case due to no regulariation in this model and due to the large number of features (134 variables) which is able to penalise the variables that distortes the linearlity.
Thus we will evaluate using the other 3 Models (RidgeCV, LassoCV and ElasticCV) have rather similar metric scores, we will use all 3 for our Actual Data.

## Conclusion

Even though all 3 Regression models have rather similar score, we can use ElasticNetCV in predicting the Sale Prices in Ames as it has the lowest RMSE score of 27409 on the test dataset. 

The most important features of the house in determining the Sale Price by looking at the coefficient from ElasticNetCV is the living area above gound, the neighbourhood, the overall (quality and condition) of the house, the garage (garage finish, garage cars and garage area) combination  and followed by the basement (types of finishes on the basement, the square footage and the quality).

Limitations
This dataset has only 5 years of sales transactions which also coincides with the subprime mortgage crisis that happened during then. This might have caused the home prices to be depressed.

## Recommendation

[Source 1](https://www.investopedia.com/articles/mortages-real-estate/11/factors-affecting-real-estate-market.asp)
[Source 2](https://www.investopedia.com/ask/answers/040215/how-does-law-supply-and-demand-affect-housing-market.asp)

There are other factors which may affect the Sale Price which are not included in the dataset that might assist are: 
- Economy status: Is the Economy facing a boom or bust
- Interest Rates: Lower interest rates tend to have more buyers (Demand and Supply)
- Demographics: Potential Homebuyers or 2nd Vacation Home, the price of rental in the neighbourhood.
- National and State Policies: Government Subsidies or Tax Incentives to attact more people to stay there.