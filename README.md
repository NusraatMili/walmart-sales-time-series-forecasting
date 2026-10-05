## 📈 Walmart Sales Forecasting (Time Series Project)

## Why I built this

Companies like Walmart need to know how much they are likely to sell next month so they can plan staff, inventory, and budgets properly. If they guess wrong, they either run out of stock or waste money overstocking. I wanted to understand how that kind of prediction actually works behind the scenes, so I built a small project that predicts Walmart's sales for the next 12 months using real historical data.

I also wanted to test something most people assume without checking: that a more advanced model with more information always gives a better prediction. So I built four different models, from simple to advanced, and tested them against real data to see which one actually performed best. The answer surprised me, and that is the main finding of this project.

This project is useful for anyone trying to understand sales forecasting, retail planning, or just wants to see a complete data science project done from start to finish, from checking the raw data to testing and comparing models with real results.

I built this to practice real time series forecasting, not on a toy dataset, but on actual Walmart sales data with real seasonality, real noise, and real trade offs between model complexity and accuracy.

The goal was to take 2.7 years of weekly sales data, turn it into a monthly series, and forecast the next 12 months using four different approaches, then actually test which one works best instead of just assuming the fancier model wins.

## 📓 Open the notebook here

**The dataset**
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

Honestly, this was the most interesting part. I expected **SARIMAX** to win since it uses more information. It didn't.

Plain **ARIMA(0,1,1)** had the lowest error when tested against real held out months. SARIMAX had the highest error by a lot. The reason is that the extra variables I added, like CPI, unemployment, and fuel price, were all really correlated with each other, and I only had 27 months to train on. That's not enough data for the model to figure out which variable actually matters, so it ended up overfitting and producing a forecast that kept dropping unrealistically.

Lesson learned is that adding more variables doesn't automatically make a forecast better. If you don't test it on data the model hasn't seen, you won't catch this.

## 📁 Files in this repo

- `Walmart_Sales_Time_Series_Forecasting.ipynb` - the full notebook, already run so you can see all the charts and outputs without re running anything
How to run it yourself

You'll need Python with pandas, numpy, matplotlib, and statsmodels installed. Download train.csv and features.csv from the Kaggle page, put them in a data/ folder, and run the notebook from top to bottom.

## ▶️ How to run it yourself

You'll need Python with pandas, numpy, matplotlib, and statsmodels installed. Download **train.csv** and **features.csv** from the [Kaggle](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting/data) page, put them in a data/ folder, and run the notebook from top to bottom.

## 🧰 Tools used

Python, Pandas, Statsmodels, Matplotlib

## 👩‍💻 Author

**Nusrat Mili**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Nusrat%20Mili-blue?logo=linkedin)](https://www.linkedin.com/in/nusrat-mili-3a21a9162/)
[![GitHub](https://img.shields.io/badge/GitHub-NusraatMili-black?logo=github)](https://github.com/NusraatMili)
