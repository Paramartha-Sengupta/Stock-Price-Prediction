# What is the Stock Market?
The stock market refers to the collection of markets and exchanges where regular activities of buying, selling, and issuance of shares of publicly-held companies take place.
Such financial activities are conducted through institutionalized formal exchanges or over-the-counter (OTC) marketplaces which operate under a defined set of regulations. 
There can be multiple stock trading venues in a country or a region which allow transactions in stocks and other forms of securities.

![image](https://user-images.githubusercontent.com/68769656/157383467-289d526d-9bfb-4868-a8da-18b594001217.png)


# Understanding the Problem Statement
We’ll dive into the implementation part of this article soon, but first it’s important to establish what we’re aiming to solve. Broadly, stock market analysis is divided into two parts – Fundamental Analysis and Technical Analysis.

Fundamental Analysis involves analyzing the company’s future profitability on the basis of its current business environment and financial performance.
Technical Analysis, on the other hand, includes reading the charts and using statistical figures to identify the trends in the stock market.
As you might have guessed, our focus will be on the technical analysis part. We’ll be using the dataset of Microsoft stock prices from April 2015 to April 2021 to build a model capable of estimating the stock prices. Time to dive in!

![image](https://user-images.githubusercontent.com/68769656/157383488-123a69b1-dfb2-47a2-af48-2dfe81aa8f31.png)

# Major Points of Understanding

There are multiple variables in the dataset – Date, Open, High, Low, Close and volume. The columns Open and Close represent the starting and final price at which the stock is traded on a particular day.
High and Low represent the maximum and minimum price of the share for the day.
Volume is the number of shares bought or sold in the day. Another important thing to note is that the market is closed on weekends and public holidays.Notice the above table again, some date values are missing – 4/3/2015, 4/4/2015 and 4/5/2015. Of these dates, 3rd April 2015 was a public holiday due to the occasion of Good Friday, while 4th and 5th April were weekends.
The profit or loss calculation is usually determined by the closing price of a stock for the day, hence we will consider the closing price as the target variable. Let’s plot the target variable to understand how it’s shaping up in our data.

![image](https://user-images.githubusercontent.com/68769656/157383730-7d7081d8-be8d-4927-9814-0b7c72db509a.png)

# Getting an overall view of Microsoft Stock Prices over the Years

![image](https://user-images.githubusercontent.com/68769656/157383805-fa3b1711-af20-4224-8b4e-8fee482c6a68.png)


# Major concepts that we have followed in the Code [Pre-requisite Knowledge]

# 1. Moving Average

Average’ is easily one of the most common things we use in our day-to-day lives. For instance, calculating the average marks to determine overall performance, or finding the average temperature of the past few days to get an idea about today’s temperature – these all are routine tasks we do on a regular basis. So this is a good starting point to use on our dataset for making predictions.

The predicted closing price for each day will be the average of a set of previously observed values. Instead of using the simple average, we will be using the moving average technique which uses the latest set of values for each prediction. In other words, for each subsequent step, the predicted values are taken into consideration while removing the oldest observed value from the set. Here is a simple figure that will help you understand this with more clarity.

![image](https://user-images.githubusercontent.com/68769656/157384014-1c73f54c-dc3e-48b9-9282-7ce6dc0f49bc.png)

We will implement this technique on our dataset. The first step is to create a dataframe that contains only the Date and Close price columns, then split it into train and validation sets to verify our predictions.

**Results of our Analysis using the Moving Average Method:**

-----------------------------------------------------------
-----------STOCK PRICE PREDICTION BY MOVING AVERAGE--------
-----------------------------------------------------------
Shape of Training Set (1134, 1)  
Shape of Validation Set (377, 1)  
RMSE value on validation set: 76.62376749929759  
-----------------------------------------------------------
-----------------------------------------------------------

![image](https://user-images.githubusercontent.com/68769656/157384133-cbd3b158-6b24-452a-a693-b48c863d3f66.png)

# 2. Linear Regression

The most basic machine learning algorithm that can be implemented on this data is linear regression. The linear regression model returns an equation that determines the relationship between the independent variables and the dependent variable.
The equation for linear regression can be written as:

![image](https://user-images.githubusercontent.com/68769656/157384333-d4cbec58-1073-4d78-925c-38eed37a14d8.png)

Here, x1, x2,….xn represent the independent variables while the coefficients θ1, θ2, …. θn represent the weights. You can refer to the following article to study linear regression in more detail:

A comprehensive beginners guide for Linear, Ridge and Lasso Regression. For our problem statement, we do not have a set of independent variables. We have only the dates instead. Let us use the date column to extract features like – day, month, year, mon/fri etc. and then fit a linear regression model.

**Results of our Analysis using the Linear Regression Method:**

-----------------------------------------------------------------  
-----------STOCK PRICE PREDICTION BY LINEAR REGRESSION-----------  
-----------------------------------------------------------------  
Shape of Training Set (1134, 1)  
Shape of Validation Set (377, 1)  
RMSE value on validation set: 58.36609230803357  
-----------------------------------------------------------------  
-----------------------------------------------------------------  

![image](https://user-images.githubusercontent.com/68769656/157384511-2afa2e55-cdf5-4092-b16a-df6d72e19765.png)

# 3. K- Nearest Neighbors

Another interesting ML algorithm that one can use here is kNN (k nearest neighbours). Based on the independent variables, kNN finds the similarity between new data points and old data points. Let me explain this with a simple example.

Consider the height and age for 11 people. On the basis of given features (‘Age’ and ‘Height’), the table can be represented in a graphical format as shown below:

![image](https://user-images.githubusercontent.com/68769656/157384896-6ef0c4be-4e3b-44e8-bf40-09b75ddb9d0e.png)

**Results of our Analysis using the K-Nearest Neighbor Method:**

-------------------------------------------------------------------  
-----------STOCK PRICE PREDICTION BY K-NEAREST NEIGHBORS-----------  
-------------------------------------------------------------------  
Shape of Training Set (1134, 1)  
Shape of Validation Set (377, 1)  
RMSE value on validation set: 112.9467566922719  
-------------------------------------------------------------------  
-------------------------------------------------------------------  

![image](https://user-images.githubusercontent.com/68769656/157385227-9788dba5-91a7-4b77-8294-474122256511.png)

Observation- The RMSE value is almost similar to the linear regression model and the plot shows the same pattern. Like linear regression, kNN also identified a drop in January 2018 since that has been the pattern for the past years. We can safely say that regression algorithms have not performed well on this dataset.

Let’s go ahead and look at some time series forecasting techniques to find out how they perform when faced with this stock prices prediction challenge

# 4. Auto-ARIMA

ARIMA is a very popular statistical method for time series forecasting. ARIMA models take into account the past values to predict the future values. There are three important parameters in ARIMA:

1. p (past values used for forecasting the next value)
2. q (past forecast errors used to predict the future values)
3. d (order of differencing)

![image](https://user-images.githubusercontent.com/68769656/157435097-0776bb98-2bad-4fd5-a653-54548207fb22.png)

Parameter tuning for ARIMA consumes a lot of time. So we will use auto ARIMA which automatically selects the best combination of (p,q,d) that provides the least error. To read more about how auto ARIMA works, refer to this article: https://alkaline-ml.com/pmdarima/modules/generated/pmdarima.arima.auto_arima.html

**Results of our Analysis using the Auto-ARIMA Method:**

![image](https://user-images.githubusercontent.com/68769656/157435173-b79ac964-d41b-4440-83ee-437cb7567f6a.png)

**Observation:** As we saw earlier, an auto ARIMA model uses past data to understand the pattern in the time series. Using these values, the model captured an increasing trend in the series. Although the predictions using this technique are far better than that of the previously implemented machine learning models, these predictions are still not close to the real values.

As its evident from the plot, the model has captured a trend in the series, but does not focus on the seasonal part. In the next section, we will implement a time series model that takes both trend and seasonality of a series into account.

# 5. Prophet

![image](https://user-images.githubusercontent.com/68769656/157435334-68363696-92c2-40d6-95e4-7e7acef70ff8.png)

There are a number of time series techniques that can be implemented on the stock prediction dataset, but most of these techniques require a lot of data preprocessing before fitting the model. Prophet, designed and pioneered by Facebook, is a time series forecasting library that requires no data preprocessing and is extremely simple to implement. The input for Prophet is a dataframe with two columns: date and target (ds and y).

Prophet tries to capture the seasonality in the past data and works well when the dataset is large. Here is an interesting article that explains Prophet in a simple and intuitive manner: https://www.analyticsvidhya.com/blog/2018/05/generate-accurate-forecasts-facebook-prophet-python-r/

**Results of our Analysis using the FB-Prophet Method:**

----------------------------------------------------------  
-----------STOCK PRICE PREDICTION BY FB PROPHET-----------  
----------------------------------------------------------  
Shape of Training Set (1134, 2)  
Shape of Validation Set (377, 2)  
RMSE value on validation set: 69.19405269585594  
-----------------------------------------------------------  
-----------------------------------------------------------  

![image](https://user-images.githubusercontent.com/68769656/157435505-cade7ed6-b7c6-401e-823b-7b36f7f59854.png)

**Observation-** Prophet (like most time series forecasting techniques) tries to capture the trend and seasonality from past data. This model usually performs well on time series datasets, but fails to live up to it’s reputation in this case.

As it turns out, stock prices do not have a particular trend or seasonality. It highly depends on what is currently going on in the market and thus the prices rise and fall. Hence forecasting techniques like ARIMA, SARIMA and Prophet would not show good results for this particular problem.

Let us go ahead and try another advanced technique – **Long Short Term Memory (LSTM)**.

# 6. Long Short Term Memory

Introduction
LSTMs are widely used for sequence prediction problems and have proven to be extremely effective. The reason they work so well is because LSTM is able to store past information that is important, and forget the information that is not. LSTM has three gates:

![image](https://user-images.githubusercontent.com/68769656/157435663-b4a41883-e2da-4597-9d19-fcd8c66dbc0f.png)

The input gate: The input gate adds information to the cell state The forget gate: It removes the information that is no longer required by the model The output gate: Output Gate at LSTM selects the information to be shown as output For a more detailed understanding of LSTM and its architecture, you can go through the below article: https://colah.github.io/posts/2015-08-Understanding-LSTMs/

Introduction to Long Short Term Memory
For now, let us implement LSTM as a black box and check it’s performance on our particular data.

**Results of our Analysis using the LSTM Method:**

-----------------------------------------------------------------------------
-----------STOCK PRICE PREDICTION BY LONG SHORT TERM MEMORY (LSTM)-----------
-----------------------------------------------------------------------------
Shape of Training Set (1134, 1)
Shape of Validation Set (377, 1)
1094/1094 - 19s - loss: 4.5201e-04
RMSE value on validation set: Close    9.464954
dtype: float64
-----------------------------------------------------------------------------
-----------------------------------------------------------------------------

![image](https://user-images.githubusercontent.com/68769656/157435972-0e950a32-ebfd-41e2-ba5f-a5a3861f3160.png)

**Observation** Wow! The LSTM model can be tuned for various parameters such as changing the number of LSTM layers, adding dropout value or increasing the number of epochs. But are the predictions from LSTM enough to identify whether the stock price will increase or decrease? Certainly not!

As I mentioned at the start of the article, stock price is affected by the news about the company and other factors like demonetization or merger/demerger of the companies. There are certain intangible factors as well which can often be impossible to predict beforehand.

# Conclusion

Time series forecasting is a very intriguing field to work with, as I have realized during my time writing these articles. There is a perception in the community that it’s a complex field, and while there is a grain of truth in there, it’s not so difficult once you get the hang of the basic techniques.

I am interested in finding out how LSTM works on a different kind of time series problem and encourage you to try it out on your own as well. If you have any questions, feel free to connect with me.


