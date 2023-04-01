# Short-Term-Electricity-Price-Forecasting-at-the-Polish-Power-Exchange-Day-Ahead-Market


## Table of Contents

+ [Overview](#overview)
+ [Modeled time series of electricity prices at the Polish Power Exchange Day-Ahead-Market ](#modeled_time_series_of_electricity_prices)
+ [Features](#features)
+ [Results](#results)
+ [Run the Codes](#run_the_codes)
+ [Development Environment](#development_environment)

## Overview <a name = "overview"></a>

This repository contains the experimental source code for short term electricity price forecasting at the Polish SPOT market (Power Exchange Day-Ahead Market)  including RNN, LSTM, GRU, MLP and Prophet models. 


## Modeled time series of electricity prices at the Polish Power Exchange Day-Ahead-Market <a name = "modeled_time_series_of_electricity_prices"></a>

The analysis is based on a series of over 26.200 hourly observations of fixing I prices (PLN/MWh) from January 2018 to December 2020. The figure below shows the time series with electricity prices during this period.
<img width="740" height="420" src = img/fig_1.png/>


The analysis of the time series of electricity prices confirmed the one described in the literature auto-regressive nature of this process. Shown in the figure below
graph of the autocorrelation function of the modeled time series, on which you can note that the price of electricity at a given hour is significantly affected by the value of the electricity price from the past corresponding to a delay of multiples of **24 hours**.
<img width="850" height="350" src = img/fig_6.png/>

A specific feature of electricity prices resulting from the daily, weekly
and annual rhythm is the variability of its level over time. The annual cycle follows
from differences in energy demand in different seasons of the year, which makes
that energy demand is higher in winter and lower in winter
summer months. Electricity prices within the weekly cycle varies with
energy demand on weekdays and weekends. In the figure below showing the weekly course of electricity prices under the 1st fixing, there are visible differences in the level of energy prices on Saturdays and Sundays
compared to other days of the week, where the course of electricity prices is similar.
<img width="740" height="420" src = img/fig_7.png/>


The daily volatility of electricity prices is influenced by the increased demand for energy,
which occurs between 6 am and 9 pm and translates into a higher price of electricity in
this time (figure below). Short-term fluctuations in electricity prices can
result from weather factors that determine the scale of energy production in renewable energy sources.
<img width="740" height="420" src = img/fig_8.png/>


## Results <a name = "results"></a>
According to the table below, **RNN** outperformed the other models.

| Model | MAE [PLN/MWh] ↓ | RMSE [PLN/MWh] ↓ | MAPE [%]↓ | R Squared [-] ↑ |
|:---:|:---:|:---:|:---:|:---:|
| Prophet | 16.9 | 21.8 | 7.54 | 0.86 |
| MLP | 16.61 | 21.23 | 7.32 | 0.87 |
| **RNN (Vanilla)** | **16.15** | **20.84** | **6.94** | **0.87** |
| LSTM | 17.15 | 22.5 | 7.26 | 0.85 | 
| GRU | 17 | 22.12 | 7.32 | 0.86 |


In the figures below shows the actual and forecast electricity price at the Polish Power Exchange Day Ahead Market in the sample period from test set. Forecasts have been generated by the model based on the Vanilla RNN, which was characterized by
the highest accuracy of electricity price predictions in the test period.

The course of the actual and forecast electricity price generated by the Vanilla RNN in October 2020.
<img width="680" height="420" src = img/fig_2.png/>

The course of the actual and forecast electricity price generated by the Vanilla RNN in November 2020.
<img width="680" height="420" src = img/fig_3.png/>

The course of the actual and forecast electricity price generated by the Vanilla RNN in December 2020.
<img width="680" height="420" src = img/fig_4.png/>

The course of the actual and forecast electricity price generated by the Vanilla RNN in the 48th week of 2020.
<img width="680" height="420" src = img/fig_5.png/>


## Run the Codes <a name = "run_the_codes"></a>

If you want to train *RNN*, 

```
python main.py --model 'rnn'
```

If you want to train *GRU* with 2 hidden layers and a learning rate of 0.05

```
python main.py --model 'gru' --num_layers 2 --lr 0.05
```


## Development Environment <a name = "development_environment"></a>
```
- Windows 10 Home
- Python 3.7.3
- torch 1.8.1
- NVIDIA GFORCE RTX 2060

