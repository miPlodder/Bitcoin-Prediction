# Bitcoin Price Prediction 

Time-Series datasets is best way to predict bitcoins price in future, for our research work. Now, a simple Regression-based Supervised Learning Algorithm can be used here. But they wouldn’t lead to better prediction and hence lead to poor accuracy. After going through many Time-Series related Research Papers, we came up with a conclusion that Statistical model can are a better way to analyse Time-Series dataset.  

Below are the steps,  

### Step - 1) Dataset Used [(Link)](https://www.kaggle.com/mczielinski/bitcoin-historical-data#bitstampUSD_1-min_data_2012-01-01_to_2018-06-27.csv)

We have taken our dataset from Kaggle website. Bitcoin exchanges are for the time period of Jan 2012 to July 2018, with minute to minute updates of OHLC (Open, High, Low, Close), Volume in BTC and indicated currency, and weighted bitcoin price. Time-stamps are in Unix time. Time-stamps without any trades or activity have their data fields forward filled from the last valid time period. 

### Step -2) Converting Dataset into Workable Schema

The dataset used in our research is in indexed by time-stamps (minute by minute for 7 years), this leads to very large number of transaction (around 3405857 rows). We tried to converted them to Day-to-Day indexed dataset, Monthly indexed dataset, Quarterly indexed dataset, and yearly dataset by taking Statistical Average of the Time-stamped value for the desired period. After analysing these newly created dataset, we concluded that Monthy-indexed dataset is perfect for our research as it don’t lose any granular pattern and doesn’t over emphasize any irrelevant variation in our dataset.

### Step -3) Stationarizing the Dataset

Now, in order to produce good results from our Statistical ARIMA model, we need to stationarize our dataset. This data pre-processing work can be done by performing various transforms on our dataset. Moreover, in order to validate whether our dataset is stationary or not, we have used Dickey–Fuller test. 
Dickey–Fuller test tests the null hypothesis that a unit root is present inan autoregressive model. The alternative hypothesis is different depending on which version of the test is used, but is usually stationarity or trend-stationarity.

In order to stationarize the dataset, we have used a variety of transforms. We can use many transform like Cox-Box, Seasonal differentiation, and Regular Differentiation for this purpose. In our research, we applied them in the sequence mentioned above and we were able to successfully Stationarize our dataset with a Dicky Fuller test value of 0.003063.

### Step -4) Training ARIMA model

The statistical ARIMA model, accepts 3 parameters which are defined below,
1) *Lag Order (p)*- Number of lag observations included in the model
2) *Degree Of Differencing (d)*- Number of times that the raw observations are differenced
3) *Order Of Moving Average (q)*- Size of the moving average window 

In order to get the best model for our research, we trained our model for various values of (p,d,q) and then chosen the model according to AIC value. 

Akaike Information Criterion (AIC) is an estimator of the relative quality of statistical models for a given set of data. Given a collection of models for the data, AIC estimates the quality of each model, relative to each of the other models. Thus, AIC provides a means for model selection.

Given a set of candidate models for the data, the preferred model is the one with the minimum AIC value. Thus, AIC rewards goodness of fit, but it also includes a penalty that is an increasing function of the number of estimated parameters. The penalty discourages overfitting, because increasing the number of parameters in the model almost always improves the goodness of the fit.
Hence, the trained model for our research has the lowest Akaike Information Criterion value.

### Step -5) Prediction of Bitcoins

The value predicted by our model, will be in another value-range because we have done 3 transformation on it. Now, in order to get the value in the required range we need to inverse those transforms and the value outputted by the inverse transforms is the predict value of the model.