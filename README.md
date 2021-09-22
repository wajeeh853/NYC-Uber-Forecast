# NYC-Uber-Forecast

## Forecasting Uber Demand in NYC

The overall process for this project is shown in this flowchart:

![This is an image](https://github.com/wajeeh853/NYC-Uber-Forecast/blob/main/flowchart.png)

The notebooks and data are separated into their own folders.

## Project Overview:

 I wanted to work on something that spanned across the following interests of mine:

-Urban transportation
-Geographic visualizations
-Timeseries forecasting

Therefore, I decided to see if I could forecast hourly Uber demand across NYC neighborhoods. In addition to time-lagged features (such as previous week’s demand), I added information specific to each neighborhood to improve my predictions. As a final result, I obtained relatively accurate unique forecasts for all neighborhoods in NYC.


# Data

- The Uber data for this project came from FiveThirtyEight (https://github.com/fivethirtyeight/uber-tlc-foil-response), who obtained the data from the NYC Taxi & - Limousine Commission (TLC) by submitting a Freedom of Information Law request on July 20, 2015.
- NYC’s Citibike data is provided on their website.
- The NYC subway station locations can be downloaded from data.ny.gov.
- The neighborhood geoJSON file was the same one used by Adrian Meyers’ excellent NYC taxi trips analysis.
This was a lot of data and to process it quickly, I relied upon using PySpark on a Google Cloud Dataproc cluster. Fortunately, Google’s tools make it easy to get up and running quickly. I used a mix of this tutorial from Google and this writeup by Charles Bochet to get Jupyter notebook running on a cluster with 1 master node and 3 worker nodes. Finally, I uploaded all my data to a Google Cloud Storage bucket which made it easy to access from multiple instances as well as avoided the headache of manually setting up a distributed filesystem (HDFS).

# Modeling

For baseline modeling, I created forecasts using only time-lagged features. I used the following three techniques, with the goal of progressing further with the most promising forecast.

-Linear Regression
-Seasonal AutoRegressive Integrated Moving Average with eXogenous regressors (SARIMAX)
-Facebook Prophet
Models were evaluated using root-mean squared error (RMSE). This way, the error metric would be easily understandable as “number of pickups” the forecast was off by.
