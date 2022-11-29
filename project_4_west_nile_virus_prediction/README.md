# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 4: Predicting Presence of West Nile Virus

## Executive Summary
This study seeks to develop a model capable of predicting West Nile virus outbreaks in the city Chicago, as well as formulate measures that will aid the City Council in combating the virus. Through the study, we created a classification model with a Test AUC of 0.828, and devise measures that would be helpful in curbing the outbreak of said virus going forward.

## Background

West Nile virus (WNV) emerged in the United States in the New York metropolitan area in the fall of 1999 ([source](https://dph.illinois.gov/topics-services/diseases-and-conditions/west-nile-virus.html)), since then, it is the leading cause of mosquito-borne disease in the continental United States ([source](https://www.cdc.gov/westnile/)). It is most commonly spread to humans through the bite of an infected female mosquito. Cases of WNV occur during mosquito season, which starts in the summer and continues through fall. About 1 in 5 people who are infected develop symptoms ranging from mild, flu-like symptoms, to neurological illnesses such as Encephalitis, Meningitis, Meningoencephalitis that may result in death ([source](https://www.hopkinsmedicine.org/health/conditions-and-diseases/west-nile-virus)).

In Illinois, West Nile virus was first identified in September 2001 when laboratory tests confirmed its presence in two dead crows found in the Chicago area. The following year, the state's first human cases and deaths from West Nile disease were recorded, and all but two of the state's 102 counties eventually reported a positive human, bird, mosquito or horse. By the end of 2002, Illinois had counted more human cases (884) and deaths (64) than any other state in the United States ([source](https://dph.illinois.gov/topics-services/diseases-and-conditions/west-nile-virus.html)). To this day, Illinois has continued to suffer from multiple outbreaks of the West Nile Virus. In 2022 alone, there are 1830 (22.6%) number of positive pools detected, highlighting the need for continuously tracking and identifying WNV presence.

## Problem Statement

As data scientist, we are tasked to develop a model to predict outbreaks of West Nile virus in mosquitos in order to help the City of Chicago and CPHD more efficiently and effectively allocate resources towards preventing transmission of this potentially deadly virus. Specifically, our model will use a combination of weather, time and location features to predict the presence of WNV within mosquito traps set up throughout Chicago.

Furthermore, given the use of public funds to finance the spraying of pesticide in order to reduce the number of WNV cases, coupled with the potentially high cost of spraying pesticide over large areas, it is imperative for this project to bring focus to where and when pesticides should be sprayed that would effectively combat the WNV problem.

## Datasets

The datasets used for this analysis are obtained from [Kaggle](https://www.kaggle.com/c/predict-west-nile-virus/):

| Dataset | Description |
|---|---|
| train.csv | Contains data relating to Date, Address, Species, Traps, No.of Mosquito Caught, and Presence of WNV from year 2007, 2009, 2011, and 2013 |
| test.csv | Contains data relating to Date, Address, Species, Traps from year 2008, 2010, 2012, and 2014 |
| spray.csv | Contains GIS data of spraying efforts in 2011 and 2013 |
| weather.csv | Contains weather data collected from 2 Weather Stations from 1st May 2007 to 31st October 2014 |

## _This project has been organised into multiple notebooks for ease of navigation and better readability._

## **I. EDA**

### **Overview**
This section covers both descriptive and inferential analysis into the datasets provided for the study.

[**(i) Train Dataset**](./1a_EDA_Train_Dataset.ipynb)

There are 7 species of mosquitos in this dataset: CULEX PIPIENS/RESTUANS, CULEX RESTUANS, CULEX PIPIENS, CULEX TERRITANS, CULEX SALINARIUS, CULEX TARSALIS, CULEX ERRATICUS. CULEX PIPIENS/RESTUANS, CULEX RESTUANS and CULEX PIPIENS are 3 species caught the most. West Nile virus is only detected in mosquito species CULEX PIPIENS/RESTUANS, CULEX RESTUANS and CULEX PIPIENS. Out of all the mosquito caught, only 5% contained West Nile virus.

A rise in the West Nile Virus among the trapped mosquitos are observed in the month of August every year. There are 136 mosquito traps set up in the city of Chicago. T900 trap has the highest numbers of traps at 750. This is followed by T115 and T138 as the second and third traps at 542 and 314 respectively.

[**(ii) Weather Dataset**](./1b_EDA_Weather_Dataset.ipynb)  

There are 2 stations in the weather dataset: Station 1 (O'HARE INTERNATIONAL AIRPORT) and Station 2 (MIDWAY INTL ARPT). They are located 30miles apart (~48km). Data are collected From May - October (6 months) every year from 2007 to 2014. It is observed that Station 2 have higher Tavg, DewPoint & WetBulb as compared to Station 1. These gap increases with time. However, it can be observed that the both stations have the same rain pattern but the intensity of the rain are quite different. It is also observed that DewPoint and Tmax; DewPoint and Tmin; Tmax and Tmin have linear relationship.

[**(iii) Spray Dataset**](./1c_EDA_Spray_Dataset.ipynb)

As per CDC the lifecycle of a mosquito, from an egg to an adult takes approximately 7-10 days. The effect of fogging will last around 30 days. Thus, we will look into the number of mosquitos 7 days before the spray and 30 days after the after the spray. From the same CDC article, it mentioned that Culex mosquitos do not fly long distances which is up to 3.2km. In our calculation we take the radius of 3km from the spray.

After plotting the graphs, it is observed that there is not a clear trend on the effect of the spray on the number of mosquitos. Some of the spray managed to bring down the number of mosquitos after a certain period of time, whereas some trend upwards on the number of mosquitos.
This would mean that there other external factors that might have contributed to the number of mosquitos.

## [**II. Data Cleaning & Pre-Processing Part I**](./2_Data_Preprocessing_I.ipynb)

### **Overview**
This section prepares the datasets for further analysis through a combination of (i) removal of irrelevant data, (ii) imputing of missing data, (iii) engineering of new features / simplification of existing features from existing data, (iv) synergising of Train, Test, and Weather datasets to form a single dataframe (for further model training).

**The outputs from this section is stored in the [Processed Data folder](./assets/Processed_Data)**.

### Key Pre-Processing Steps Performed
**Train & Test Dataset**
- "NumMosquitos": In the absence of such data in the test set, we believed that said information is also effectively captured through the dummification of the 'Trap' variable. We therefore do not see a need to maintain this column.
- "Traps": To simplify our model, extra trap characters are removed and the satellite traps are defaulted to their parent satellite
- "Species": 'UNSPECIFIED CULEX' are found in test dataset but not in train dataset. It is prescribed to the majority class 'CULEX PIPIENS/RESTUANS', which account for >99% observations (together with CULEX PIPIENS + CULEX RESTUANS) in the train set.
- "Address", "Block", "Street", "AddressNumberAndStreet", "AddressAccuracy" are dropped as they are correlated to "Traps"

**Weather Dataset**
- "Heat", "Cool", "Depart": As they are irrelevant, these data are removed from our analysis.
- "Tavg": Missing values are calculated based on the average between Tmax & Tmin.
- "Depth", "Water1", "Snowfall": These features are removed since the values are only 0 or M(issing).
- "Sunrise" and "SunSet": These 2 features are streamlined into 1 as "Daylight Hours", which is simply Sunset-Sunrise time
- "CodeSum": This feature can Be engineered into a new feature as it provides great details into the actual weather conditions. There is a large amount of designation for CodeSum variables, for the many types of special weather conditions. We will attempt to classify them into more manageable number of classes, and characterise each observation accordingly.
- "Wetbulb", "PrecipTotal", "StnPressure", "SeaLevel", "AvgSpeed": Missing value are imputed from alternate Weather Station.
- By plotting heatmap on weather features, we found that "DewPoint" & "WetBulb" are highly correlated with "Tavg", "SeaLevel" are highly correlated with "StnPressure", and "ResultSpeed" are highly correlated with "AvgSpeed", hence we will drop them from the analysis.

**Combining Train, Test & Weather Dataset**\
We have two weather stations providing two disparate set of weather information. We need a systematic approach to decide how should the weather conditions surrounding a trap be determined. We propose a weighted approach whereby the relative weightage for each weather station is calculated as the inverse-squared-distance of a trap from each weather station. The pair of weights for each trap is then normalised against each other, and the relative proportion of the data drawn from each weather station's data point.

## [**III. Data Cleaning & Pre-Processing Part II**](./3_Data_Preprocessing_II.ipynb)
A critical step towards our feature engineering process, this section further prepares the dataset by computing the rolling averages of weather-related variables for each observation in the test and train datasets. Critically, the computation of said variables reflect our theory that peak mosquito activity demands a certain duration of conducive weather conditions for the mosquitoes (i.e. not just one day of conducive weather).

**The outputs from this section is stored in the [Modelling Data folder](./assets/Modelling_Data)**.

## [**IV. Broad Scan of Classification Models**](./4a_Model_Scan_Pycaret.ipynb)
This section uses the PyCaret API to perform a broad scan of the different Classification algorithms, towards shortlisting suitable algorithms for our classification tasks. Using AUC as as measure, the Logistics Regression, Gradient Boosting Classifier, and Light Gradient Boosting Classifier were selected for further modelling.

**A summary of the outputs from PyCaret is stored in the [PyCaret folder](./assets/Pycaret)**.

## [**V. Modelling of Classification Model**](./4b_Modelling.ipynb)
This section uses Gridsearch to optimise the hyperparameters for the shortlisted classification models, towards determining the production model of choice for our classification task. The Logistic Regression model (with 30-days rolling averages for the weather-related variables), with a Train and Test AUCs of 0.867 and 0.828 respectively was chosen as our production model. Critically, despite having an AUC performance marginally lower than that of competing candidate models, the Logistic Regression was chosen for its explainability towards a non-technical audience.

## [**VI. Cost Benefits Analysis**](./5_Cost_benefit_analysis.ipynb)
**The Cost-Benefits Analysis spans into 3 segments**:

(1) The first section explains that spraying costs are far lower than the medical/opportunity costs due to WNV. As a blunt recommendation, an approach to solving the WNV involves a liberal use of mosquito spray.

(2) The section explains that, in a scenario limited resources are available, the model developed could be used to identify observations with the highest probability of WNV cases, following which intervention measures (spray, public education, stronger enforcement, etc.) could be applied surgically to such areas.

(3) The final section examines how a optimal prediction threshold can be established from the classification model we have developed. In practice, said prediction threshold will help the city council by serving as an indicator signalling if a particular observation would require intervention.

## [**VII. Conclusion and Recommendations**](./6_Conclusion_and_Recommendations.ipynb)

### Conclusion
(1) The Logistic Regression Model using a 30-day rolling average for weather-related model was chosen as our production model. The model yields a Train AUC of 0.867 and a Test AUC of 0.827. The Chosen Model did not Exhibit the Best Train and Test AUC Among all our Candidate Models, but was chosen for its explainability. We also uncovered that the most important factors influencing WNV onset are precipitation (such as drizzle and rain; largest contributor to increase in WNV onset) and fog (largest deterrence to onset of WNV).

(2) The rolling averages of weather-related variables were engineered with due consideration to the fact that peak mosquito activity will require a conducive climate over a certain period of time. Compared to models that relied on a single day weather (i.e. 1 day rolling average), model employing a rolling average of weather-related variables showed drastically superior results.

### Recommendations
(1) Our production model can be applied to identify (1) high WNV-probability areas where finite spraying and monetary resources could be directed towards, and (2) the optimal threshold whereby a firm and pre-emptive intervention point can be established. 

(2) Broadly, the performance of models improves with as the number of rolling averages increases. We recommend further studies into the hibernation behavior of mosquitos, towards developing a better model.

(3) We note that Spraying alone is a very blunt instrument against mosquitos. More effective and pre-emptive comes in the form public education, improvements to drainage systems, and strict enforcement of fines for public violators.
