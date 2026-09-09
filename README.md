## 📈 Walmart Sales Forecasting (Time Series Project)

I built this project to practice real time series forecasting, on actual Walmart sales data with real seasonality, real noise, and real trade offs between model complexity and accuracy.

The goal was to take 2.7 years of weekly sales data, turn it into a monthly series, and forecast the next 12 months using four different approaches - plain ARIMA, SARIMA, decomposition + ARIMA, and SARIMAX with exogenous macro/weather regressors, then actually test which one works best instead of just assuming the fancier model wins.

## 📚 Dataset Information

I used the [Walmart Recruiting Store Sales Forecasting](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting) dataset from Kaggle. It has weekly sales for 45 stores from February 2010 to October 2012, plus some extra info per store like temperature, fuel prices, CPI, and unemployment rate.

Since the data comes in weekly, I summed it up across all stores to get one total number per week, then grouped that into months. That left me with 33 monthly data points to work with.

## 🔍 What I actually did

1. Loaded the data and turned it into a proper time series
2. Plotted it and looked for trend, seasonality, and anything unusual
3. Ran ADF and KPSS tests to check if the series was stationary
4. Looked at ACF and PACF plots to figure out what ARIMA settings made sense
5. Tried out 8 different ARIMA models and compared them using AIC and BIC
6. Checked the residuals of the best model to make sure it wasn't missing anything
7. Forecast the next 12 months using four different methods:
     - Plain ARIMA
     - SARIMA, which handles seasonality on its own
     - ARIMA on a deseasonalized version of the data
     - SARIMAX, same as SARIMA but with extra variables like fuel price and unemployment added in
8. Held out the last 6 months of real data and tested all four models against it, to see which one actually predicts better instead of just looking good on paper

## 💡 What I found

Honestly, this was the most interesting part. I expected SARIMAX to win since it uses more information. It didn't.

Plain ARIMA(0,1,1) had the lowest error when tested against real held out months. SARIMAX had the highest error by a lot. The reason is that the extra variables I added, like CPI, unemployment, and fuel price, were all really correlated with each other, and I only had 27 months to train on. That's not enough data for the model to figure out which variable actually matters, so it ended up overfitting and producing a forecast that kept dropping unrealistically.

Lesson learned is that adding more variables doesn't automatically make a forecast better. If you don't test it on data the model hasn't seen, you won't catch this.

## 📁 Files in this repo

"Walmart_Sales_Time_Series_Forecasting.ipynb" - the full notebook, already run so you can see all the charts and outputs without re running anything.

## ▶️ How to run it yourself

You'll need Python with pandas, numpy, matplotlib, and statsmodels installed. Download **train.csv** and **features.csv** from the [Kaggle](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting/data) page, put them in a data/ folder, and run the notebook from top to bottom.

## 🧰 Tools used

Python, Pandas, Statsmodels, Matplotlib
