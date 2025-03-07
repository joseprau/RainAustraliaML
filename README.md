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
In this section we will go thorugh some analysis on the data. 

![alt text](./figs/Rainy_days_distr.png)

**Observations:**
- As observed, non rainy days are more often than rainy days. In this case, roughly 80% of the dataset are non rainy days.
- From here we can sense the presence of unbalanced data. 

We proceed to analyze how the different numerical attriubtes distribute. 

![alt text](./figs/distributions.png)

**Observations:**
- Most of the variables follow a normal distribution.
- Rainfall variable appear to have some issues when ploting, most likely due to the presence of outliers. Outliers may also be affecting Evaporation as it appears skewed in the plot.
- Due to Australia's variety of climates, we can see wide ranges in MinTemps and MaxTemps. Territories such as Victoria, are usually colder than tropical territories like Northern Territory. Therefore, these differences of climates across regions make the distributions much wider.
- Humidity columns presnet also a curious distribution with peaks of humidity to 100% at 9am. 

How rain distributes across Locations can be useful to identify which regions are more rainy. 

![alt text](./figs/rain_by_locations.png)

**Observations:**
- As observed, Portland is the city with most Rainy days over the last years and Uluru presents the lowest rain levels of all locations.
- This chart provides us with the sense that Location may be a very relevant feature when making predictions. 


It is also interesting to analyze the rain distribution from a time perspective.

![alt text](./figs/rain_trend_year.png)
![alt text](./figs/rain_trend_months.png)

**Observations:**
- As it can be observed in the first graph, rainy days have slightly decreased since 2007 and has mantained a rain rate around 20% and 24% over the last years. 

- The second plot suggests that rain in australia has a certain degree of seasonality. Rain days are more common between May and September, and they drop after October. This seasonality can strongly be noted in northern regions, where they experience a dry and wet season.

Lastly, it is  good idea to see how the variables correlate with each other. 

![alt text](./figs/corr_matrix.png)

**Observations:**
- With this graph we are able to see the correlations between variables. We observe strong positive correlations and relatively strong negative correlations.
- Temperatures are highly correlated with their correlative variables. For instance, Temp9am is strongly correlated with MinTemp (0.9) an Temp3pm with MaxTemp (0.98).
- As for negative strong correlations, Cloud9am and Cloud3pm outstand from the rest. These two variables are strongly correlated with Sunshine (0.68 and 0.7 respectively) suggesting that the presence of clouds at 9am and 3pm reduce Sunshine.

## Modelling
Now that the data has been scaled, we can proceed to the modelling phase. We are dealing with a binary classification problem where the data is already labelled, therefore we will work with supervised methods such as:

- Logistic Regression
- Decision Tree
- Random Forest
- CNN

### Logistic Regression
-----------------

The results for a base Logistic Regression Models are: 

Metrics: \
Test Accuracy: 0.8445\
Train Accuracy: 0.8482\
Sensitivity: 0.5089\
Specificity: 0.9409\
ROC-AUC: 0.8669\
F1-Score: 0.5935

![alt-text](./figs/logreg_base_conf_matr.png)
![alt-text](./figs/logreg_base_roc.png)

**Observations:**
- Accuracy is consistent across test and training data, meaning there is no overfitting. The accuracy for test data is 84% which is quite satosfactory for a base model. 
- The model seems to predict better the negative class, hence days with no rain. This is identifiable from the high specificity value (90%).
- Recall is quite low (50%) meaning the model only captures 1 out of 2 positive classes. 
- AUC value is pretty decent, and shows that the model performs well on differentiating between classes.
- F1 score relates accuracy and recall and it is a good measure to harmonize the mean of these two metrics. In this scenario, the F1 Score is weak, mainly because of the low Recall value obtained. 


After applying some Hyperparameter tunning, the results show no major significant changes at all, probably due to the parameters tunned not being core for the model's performance (I would need to look deep into it)

### Decision Tree
-----------------

The results of using a base Classification Tree Model are:

Metrics: 
Test Accuracy: 0.7893\
Train Accuracy: 1.0000\
Sensitivity: 0.5458\
Specificity: 0.8591\
ROC-AUC: 0.7025\
F1-Score: 0.5360

![alt-text](./figs/clf_conf_matr.png)
![alt-text](./figs/clf_roc.png)

**Observations:**
- As observed, train accuracy obtained is 1, and is much larger than test accuracy. This is a clear indicator that the model suffers from overfitting. 


After applying some hyperparameter tunning, the results are:

Metrics: 
Test Accuracy: 0.8399\
Train Accuracy: 0.8465\
Sensitivity: 0.4431\
Specificity: 0.9538\
ROC-AUC: 0.8421\
F1-Score: 0.5524

![alt-text](./figs/clf_gs_conf_matr.png)
![alt-text](./figs/clf_gs_roc.png)

**Observations:**
- The model is not overfitted anymore.
- The accuracy score for test set is slightly worse than Logistic Regression, but still is satisfactory (84%)
- Recall value has decrease, indicating that the Decision Tree is not good when predicting the positive class. 
- Since Recall has gone down, the F Score has as well been reduced to 0.55.
- The AUC value is still decent, bus has been reduced by 2 ppt.


# Results
Finally the results obtained are as follows:

|                        |      auc |   accuracy_train |   accuracy_test |   recall |   specificity |   F1_Score |
|:-----------------------|---------:|-----------------:|----------------:|---------:|--------------:|-----------:|
| LogReg (Base)          | 0.866874 |         0.848225 |        0.844544 | 0.50891  |      0.940854 |   0.593471 |
| LogReg (Tunned)        | 0.866876 |         0.848234 |        0.844544 | 0.50891  |      0.940854 |   0.593471 |
| Decision Tree (Base)   | 0.70247  |         0.999991 |        0.789268 | 0.545813 |      0.859128 |   0.535966 |
| Decision Tree (Tunned) | 0.842076 |         0.846537 |        0.839903 | 0.443148 |      0.953751 |   0.552443 |
| Random Forest (Base)   | 0.881457 |         0.999974 |        0.853898 | 0.499448 |      0.955607 |   0.603871 |



**Observations:**
- When comparing these results we can exclude the base Decision Tree model and RandomForest model since we found they were overfit.
- As per the rest of the models, Logistic Regression shows the best results, with a test accuracy of 84% (base and tunned) and a decent AUC (86%), indicating that the model generalizes well. 
- Despite the results in accuracy and specificity are satisfactory, all the models are weak for predicting the positive class correctly. All models show around 50% recall value, meaning that is only capable to predict correctly the 50% of the rainy days. 


# Final Considerations and improvements *

As a general conclusion, I am aware this project need much further improvements, specially in the modelling section. These improvements include:
- **Performing hyperparameter tunning for Random Forest**. Due to the time it was taking in my computer, I decided to skip it for now until I have time again. The idea would be to create an instance in Google Collab and make use of the free GPU in order to speed things up. 
- **Comparing with more advanced ML algorithms.** In this project I used only the very basic ML algorithms such as Logistic Regression and Classification Tree. I also used RandomForest as an ensamble technique. As future improvements, I would like to apply more modern and advanced models such as Cascading and Boosting ensambles or neural networks for more deep learning approach.
- **Check for feature importance.** Ensambling techniques allow for feature importance analysis, so would be a good idea to see which attributes influence the most for making the predictions. 
- **Null and Outliers.** For the purpose of this project I used simple techniques for null and outlier's imputations. In the futre I would like to try newer and more efficient methods and see what effect do they have on the final results. 
- **More in depth EDA.** Extend the EDA section and gain more knowledge in the dataset.
- **Class Imbalance Treatment.** The dataset is imbalanced and may be affecting the results and the model capacity to predict the minority class, in this case rainy days. It would be greate to explore oversampling techniques such as SMOTE or ADASYN to balance the data and see if it brings any improvements. 
- **Colinearity.** The heatmap used to plot the correlation matrix shows high correlation coeficients between some variables. Therefore, we could further study this event and apply the adequate techniques and see if they have any impact on the results. 


*Because the Master's semester is starting back again and I am working full-time, I have had to stop the project before I wished.