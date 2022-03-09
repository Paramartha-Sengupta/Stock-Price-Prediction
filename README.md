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

**Results of our Analysis using the Moving Avergae Method:**

-----------------------------------------------------------
-----------STOCK PRICE PREDICTION BY MOVING AVERAGE--------
-----------------------------------------------------------
Shape of Training Set (1134, 1)
Shape of Validation Set (377, 1)
RMSE value on validation set: 76.62376749929759
-----------------------------------------------------------
-----------------------------------------------------------

![image](https://user-images.githubusercontent.com/68769656/157384133-cbd3b158-6b24-452a-a693-b48c863d3f66.png)

