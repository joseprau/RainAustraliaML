# Rain in Australia Prediction

## Introduction & Context
This is the last activity of the subject 02.584 - Data Mining from the Data Science Master's at UOC. In this project we are required to identify and define a business requirement for which we will perform some data analysis, data preprocessing and apply basic ML algorithms. 

Knowing whether or not it will rain the next day is vital for many companies working in the more rural areas of Australia. On the one hand, in the southern regions where most of the rainfall is found, it is essential for farm workers to know for sure whether or not it will rain the next day in order to leave the field ready for the following day. On the other hand, the northern and north-western regions, where many mining companies have camps and carry out their mining activities in these areas. For these companies it is important to know if there will be rainfall the following day, as this hinders mining activities, especially in open-pit mines. Hence, this project intends to predict wether or not the next day is going to rain or not.

## Dataset

The data with which we will work contain daily meteorological information of the last 10 years of the Austrian territories. We have continuous variables such as humidity levels, maximum temperature, minimum temperature, etc. We also have categorical variables such as territory and wind direction, and binary variables. The data have been extracted from Kagle (https://www.kaggle.com/datasets/jsphyg/weather-dataset-rattle-package/data) and at the moment these are fed from the Australian weather website (http://www.bom.gov.au/).

The data we have are raw, and therefore a previous cleaning will be necessary before processing them and applying the model. Therefore, before applying our classification model, we will have to deal with blank spaces, null values, outliers and other facts that may appear. In both supervised and unsupervised models it is important to treat outliers correctly as they can bias the results towards false conclusions. However, it is worth mentioning that we have models that are not affected by outliers, as is the case of the forest of openings in classification models and the DBSCAN algorithm for unsupervised models.

We present the columns of the set of data.

- **Date:** Date of the observation.
- **Location:** Location of the meteorological station.
- **MinTemp:** Minimum temperature (Celsius).
- **MaxTemp:** Maximum Temperature (Celsius)
- **Rainfall:** Amount of rainfall collected that day (mm)
- **Evaporation:** Evaporation class A (mm) For more information: https://en.wikipedia.org/wiki Pan_evaporation
- **Sunshine:** Hours of sunshine per day.
- **WindGustDir:** The direction of the strongest wind gust in the last 24 to midday.
- **WindGustSpeed:** The speed of the strongest wind gust in the last 24 hours until midday (km/h).
- **WindDir9am:** Wind direction at 9am.
- **WindDir3pm:** Wind direction at 3pm.
- **WindSpeed9am:** Wind speed averaged for 10 minutes before 9am (km/h).
- **WindSpeed3pm:** Wind speed forecasted for 10 minutes before 3pm (km/h)
- **Humidity9am:** Humidity at 9am (%).
- **Humidity3pm:** Humidity at 3pm (%).
- **Pressure9am:** Atmospheric pressure reduced at sea level at 9am (hPa).
- **Pressure3pm:** Reduced atmospheric pressure at sea level at 3pm (hPa)
- **Cloud9am:** Cloud-covered sky fraction at 9am (oktas*).
- **Cloud3pm:** Cloud cover at 3pm (oktas).
- **Temp9am:** Temperature at 9am (Celsius).
- **Temp3pm:** Temperature at 3pm (Celsius).
- **RainyToday:** Categorical variable that indicates if it has rained today or not.
- **RainyTomorrow:** Categorical variable indicating whether it will rain the next day or not.
 

## Exploratory Data Analysis

## Modelling

## Results
