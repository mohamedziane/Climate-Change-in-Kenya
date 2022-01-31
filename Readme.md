# Investigating the relationship between energy and mining consumption in Nairobi, Kenya and how it affects climate change.


<p align="center">
  <img width="1000" height="400" src="https://raw.githubusercontent.com/mohamedziane/Climate-Change-in-Kenya/main/images/GeneralPicKenya.png">
</p>

## 1. Introduction

By using data from varied sources (The World Bank, The Humanitarian Data Exchange, and Meteo Blue), a global understanding of relationships between potential climate change factors that could explain some key variables such as Temperature and Precipitation could be drawn for Africa as a whole and Kenya more specifically. 

This project will be investigating the relationship between energy and mining consumption in Nairobi, Kenya and how it affects climate change. Analysis will be briefly global (Africa) before focusing specifically on Kenya.

Even though most of the project was centered around Nairobi, two other African cities (Algiers and Cape Town) were added to initially compare whether some trends in Nairobi’s temperature could also be correlated with other parts in Africa. However, temperature variation is challenging to rely on to extract an obvious trend as temperature varies throughout seasons.

Eventually, using machine learning, a forecast prediction was achieved for the precipitation and temperature for Nairobi from 1985 to 2019.

The six steps that this project followed are:

- Context & Problem Identification
- Data Wrangling
- Exploratory Data Analysis (EDA)
- Pre-Processing and Training Data Development
- Modeling

**Data Sources**

<p align="center">
  <img width="400" height="300" src="https://static.meteoblue.com/assets/images/logo/launcher-icon-4x.png">
  <img width="400" height="300" src="https://ceowatermandate.org/wp-content/uploads/2019/04/World-bank-logo-1.jpg">
  <img width="400" height="300" src="https://data.humdata.org/images/hxl_fb-01.png">
</p>


Stemming from different sources from the [World Bank Open Data (WBOD)](https://data.worldbank.org/), the [Humanitarian Data Exchange (HDE)](https://data.humdata.org/) and [Meteo Blue (meteorological service created at the University of Basel, Switzerland in 2006)](https://www.meteoblue.com/en/weather/week/princeton_united-states_5102922), several climate-related data were collected to extract insights into possible correlations between causes and consequences of climate change in Kenya. 20+ years of daily data were analyzed and, using machine learning, a prediction of main climate consequences were simulated.


## 1. Context

Climate risks pose serious threats to Kenya’s sustainable development goals. With the largest economy in East Africa and a population of 48.5 million, Kenya serves as the regions financial, trade and communications hub.

The country’s economy is largely dependent on rainfed agriculture and tourism, each susceptible to climate variability and change and extreme weather events. Increasing interseason variability, increasing temperatures, heavy rainfall events and sea level rise lead to severe crop and livestock losses, famine and displacement. High population growth in urban areas is leading to expanding informal settlements, which are at risk from water scarcity, flooding and heat.


Most of the country’s coast is low-lying, with coastal plains, islands, beaches, wetlands and estuaries at risk from sea level rise. A sea level rise of 30cm is estimated to threaten 17 percent (4,600 hectares) of Mombasa with inundation. Models estimate that by 2030 climate variability and extremes will lead to losses equivalent to 2.6 percent of GDP annually.

Kenya’s geography is dominated by arid and semi-arid plains, with a temperate highland plateau (reaching over
5,000 m) in the center, and a hotter, wetter climate along the coast and the shores of Lake Victoria. Two-thirds
of the country receive less than 500 mm (19.6 in) of rainfall per year; coastal and highland areas receive annual
averages upwards of 1,100 mm (43 in) and 2,000 mm (78 in), respectively.

## 2. Data Wrangling

This step focuses on collecting data, organizing it and making sure it is well defined. Some data cleanings are also carried out in this stage.
A total of 8 different raw tables were sourced. 5 of them, from WBOD and HDE contained possible climate change causes for the entire African region, that ended up being merged into a single table while the three remaining ones, sourced from Meteo Blue, contained possible consequences from climate change in Nairobi (Kenya), but also from Algiers (Algeria) and Cape Town (South Africa).

Even though most of the project was centered around Nairobi, the two other African cities were added to initially compare whether some trends in Nairobi could also be correlated with other parts in Africa.

**Possible Consequences of Climate Change for Algeria, Kenya and South Africa (from Meteo Blue)**

For each of those cities, the 12 following possible related consequences were selected:

- Temperature
- Precipitation
- Snowfall amount
- Relative humidity
- Wind speed
- Wind Dominant direction
- Total cloud covering
- Sunshine duration
- Shortwave radiation
- Mean sea level pressure
- Soil temperature
- Soil Moisture

<p align="center">
  <img width="1000" height="500" src="https://raw.githubusercontent.com/mohamedziane/Climate-Change-in-Kenya/main/images/FIG2.png">
</p>

The figure above displays the top 12 list containing the old vs.new variables after re-naming (bottom 12). The additional column “timestamp” is the time-series column dating from 1985 to 2019. There are 13150 rows of datasets as they are daily records sourced from Meteo Blue.

**Possible Causes of Climate Change for Algeria, Kenya and South Africa (from WBOD and HDE)**

A total of 72 different features were initially sourced as possible causes and 26 were retained as possibly most significant.

<p align="center">
  <img width="1000" height="500" src="https://raw.githubusercontent.com/mohamedziane/Climate-Change-in-Kenya/main/images/FIG3.png">
</p>

The figure above shows the Python output of the 26 possible related causes of climate change in Nairobi (Kenya). The additional column “timestamp” is the time-series column dating from 1985 to 2019. There are 12540 rows of datasets as they are daily records sourced from the World Bank and the Humanitarian Data Exchange.


## 3. Exploratory Data Analysis (EDA)

EDA is an approach for summarizing and visualizing the important characteristics and statistical properties of a dataset. Visualizing the data will help make sense of it to identify emerging themes.

The first step was to load the merged data that contained possible causes of climate change in Africa versus consequences in Kenya (Labeled with “_N” for Nairobi), Algeria (Labeled with “_A” for Algiers) and South Africa (Labeled with “_CT” for Cape Town).

The merged table was also filtered to only contain data ranging from 1985/31/12 until 2019/31/12 on a daily basis and a yearly version of the table was also created using a resampling option.

The temperature variation above 1985 to 2019 is consistent throughout the three cities (North to South). However, temperature variation is very hard to extract an obvious trend as temperature varies throughout seasons. Can we identify which other factors may have had a more significant increase from 1985 to 2019? The remaining of the project fosuced only on Nairobi, Kenya.

<p align="center">
  <img width="1000" height="500" src="https://raw.githubusercontent.com/mohamedziane/Climate-Change-in-Kenya/main/images/FIG5.png">
</p>

**Top 10 Climate-related causes and consequences in Nairobi. Kenya from 1985 to 2019**

The yearly final merged table was used as the input after removing datasets from South Africa and Algeria. Then, a simple ratio of values belonging to 2019 was divided by the 1985 ones to evaluate the biggest increase in that time period. An initial test was performed on one variable only (Temperature) before creating a loop over all the other variables (causes and consequences).

The top three possible causes and consequences that saw the biggest increase from 1985 to 2019 are displayed in the two histograms below. The biggest cause was the foreign direct investment (by percentage of GDP), followed closely by the C02 emissions, while the precipitation dominated the top possible leading consequence of climate change in Nairobi during this time period. Quick relationship plots show that:

- The temperature is still very hard to link with C02 emissions even though a direct relationship trend can be noticeable
- The precipitation seems to go hand in hand with the CO2 emissions and foreign direct investments

<p align="center">
  <img width="1000" height="500" src="https://raw.githubusercontent.com/mohamedziane/Climate-Change-in-Kenya/main/images/FIG7.png">
  <img width="1000" height="500" src="https://raw.githubusercontent.com/mohamedziane/Climate-Change-in-Kenya/main/images/FIG8.png">
</p>

**Correlation Matrix to identify global relationship trends between all those parameters**

One way to identify relationships between all those variables is to use the Pearson coefficient which is a measure of linear association between variables. It has a value between -1 and 1 where: -1 indicates a perfectly negative linear correlation while +1 would reflect a perfectly positive correlation instead.

- C02 seems to be more correlated with the following: the Total& Urban Population & Methane emissions. Interestingly, it is also related to the mortality rate (for children under 5 years old). The latter may be surprising, but it may be explained by the fact that infants do not spend as much time as do adults or
older kids?

- Nitrous oxide emissions appear to have more correlations than CO2 does: Agricultural land, Methane emissions, populations in urban agglomerations and the total population. Like CO2, it is also inversely related with the mortality rate for infants under five years old.

- Precipitation seems to be related to Ores & metal exports, agricultural land, CO2 emissions, foreign direct investments, Methane & Nitrous Oxide emissions, population in urban agglomerations, the total population, the total cloud cover and the soil moisture.

<p align="center">
  <img width="600" height="300" src="https://raw.githubusercontent.com/mohamedziane/Climate-Change-in-Kenya/main/images/FIG9.png">
</p>


## 4. Pre-Processing, Training Data Development and Modeling

This last part focuses on leveraging the cleaned and processed dataset to make predictive insights. Machine learning is used to assess the biggest positive correlations between causes and consequences for Temperature and precipitation changes for the last 30 years in Kenya.

**Machine Learning Background**

With the field of machine learning, there are two main types of tasks: supervised and unsupervised. The main difference between the two types is that supervised learning hails from having prior knowledge of what the output values for our samples should be. Therefore, the goal of supervised learning is to learn a function that, given a sample of data and desired outputs, best approximates the relationship between input and output observable in the data. Unsupervised learning, on the other hand, does not have labeled outputs, so its goal is to infer the natural structure present within a set of data points. Two supervised-based models were used: Ordinary Least Squares Regression and Random Forest.

**Data Input for Predictions using Ordinary Least Squares (OLS)**

<p align="center">
  <img width="1000" height="500" src="https://desktop.arcgis.com/en/arcmap/10.3/tools/spatial-statistics-toolbox/GUID-8278E3D7-7E53-4DEF-B0B8-8BE33F969BEA-web.png>
</p>


A total of eight different features were selected to predict temperature and precipitation from 1985 to 2019. While, both of those two variables will be assessed independently, the features remained the same. Those 8 features were selected based on the Pearson correlation matrix seen in the previous part and are:

- CO2 emissions
- Methane emissions
- Nitrous oxide emissions
- Total population
- Urban population
- Relative Humidity
- Mean sea level pressure
- Soil moisture

The OLS, is a type of linear least squares method for estimating the unknown parameters in a linear regression model. OLS chooses the parameters of a linear function of a set of explanatory variables by the principle of least squares: minimizing the sum of the differences between the observed features and those predicted by the linear function of the two independent variables (Precipitation and Temperature).

**Results of predictions of Temperature and Precipitation**

For a very simple model such as OLS, the accuracy results does not seem too bad, but after several iterations, the score seemed to still hover around a 61% accuracy. 

<p align="center">
  <img width="1000" height="500" src="https://raw.githubusercontent.com/mohamedziane/Climate-Change-in-Kenya/main/images/FIG11.png">
</p>

**Random Regressor with Random Forest**

<p align="center">
  <img width="1000" height="500" src="https://www.tibco.com/sites/tibco/files/media_entity/2021-05/random-forest-diagram.svg">
</p>

A model that can work very well in a lot of cases is the Random Forest. For regression, this is provided by Sklearn’s RandomForestRegressor class. A pipeline was designed to assess the performance using cross-validation. The latter was performing the fitting as part of the process. I first used the default settings for the random forest and then went on to investigate some different hyperparameters. The cross validation mean absolute error for the Temperature and the Precipitation were: 0.84 Deg F and 0.03 in respectively. Similarly, the mean absolute error for both variables were lower from the Random Forest than from the Linear Regression results

<p align="center">
  <img width="1000" height="500" src="https://raw.githubusercontent.com/mohamedziane/Climate-Change-in-Kenya/main/images/FIG12.png">
  <img width="1000" height="500" src="https://raw.githubusercontent.com/mohamedziane/Climate-Change-in-Kenya/main/images/3aFIG12.png">
  <img width="1000" height="500" src="https://raw.githubusercontent.com/mohamedziane/Climate-Change-in-Kenya/main/images/3bFIG12.png">
</p>


## 4. Conclusion

- This project, far from being exhaustive, used limited information and used the assumption that data from capitals (in that case Nairobi) could be extrapolated to a whole country. As such, more work should be done to gather more data from other cities for a single country and enhance the machine learning by increasing the number of training dataset.

- The first step in developing a model was to examine performance by using the mean of temperature and precipitation individually. This proved to be helpful in establishing a baseline for comparison, however it was not as useful or as accurate as a linear model or random forest model. If I predicted those variables by using the mean, on average we would be off by about 3 Deg F and 0.27 in for the Temperature and Precipitation respectively.

- In the process of building the linear model, missing values were imputed with the median and mean values. However, the initial linear model was overfitting and needed to be adjusted by the number of features. Through cross-validation, the value of k was set to focus on: Soil Temperature and CO2 emissions for the Temperature. Similarly, the value of k was set to focus on: Soil Moisture, Sunshine Duration, Shortwave radiation, Mean sea level pressure, Fuel Imports and CO2 emissions. These features fit our initial assumptions from the EDA.

- After testing both the linear model and random forest model, the best performance was from using the forest regression model. Comparison of the two demonstrated that performance on the test set was consistent cross-validation results. Additionally, the cross-validation mean absolute error was lower using the random forest regressor.

- Despite the limitationsin data availability, the Data Science Method has proven to be a very useful tool to extract key information that could be used to gain quick insights and lead the ground for future more detailed research work.


