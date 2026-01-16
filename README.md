# Apple-Stock-Price-Predictions
Overview

This project focuses on building a time-series forecasting model to predict the future closing prices of Apple Inc. (AAPL) using historical stock market data. The model is trained on 10 years of daily OHLCV data and deployed through a Streamlit web application for interactive predictions.

The goal is not short-term trading signals, but to demonstrate a robust end-to-end machine learning pipeline for financial time-series forecasting — from data acquisition and preprocessing to model training and deployment.

Problem Statement

Given historical daily stock data for Apple Inc., can we use past market behavior to predict the next few trading days’ closing prices?

Key constraints:

Financial data is sequential and time-dependent

Future market data (Open, High, Low, Volume) is unknown at prediction time

Predictions must be evaluated after market close

Dataset

Source: Yahoo Finance (via yfinance)

Ticker: AAPL

Period: January 15, 2016 – January 15, 2026

Frequency: Daily (trading days only)

Features Used

Open

High

Low

Close

Volume

Target Variable

Close Price (end-of-day price)

Note: The dataset does not explicitly contain Adj Close. Stock splits are implicitly reflected in the Close price, while dividends are provided separately but not used directly in training.

Modeling Approach
Model Architecture

Long Short-Term Memory (LSTM) neural network

Designed to capture temporal dependencies in financial time-series data

Sequence Construction

Lookback window: 60 trading days

Each training sample uses the previous 60 days of OHLCV data to predict the next day’s Close price

Scaling

MinMaxScaler applied separately to:

Feature matrix (OHLCV)

Target variable (Close price)

This ensures numerical stability and consistent predictions during deployment.

Training Pipeline

Data retrieval

Feature and target scaling

Sequence generation for time-series learning

Chronological train / validation / test split

LSTM model training

Model evaluation using:

RMSE (Root Mean Squared Error)

Visual comparison of predicted vs actual prices

Saving trained artifacts:

Model (.keras)

Feature scaler (feature_scaler.pkl)

Target scaler (target_scaler.pkl)

Multi-Day Forecasting Strategy

The model is trained for one-step-ahead prediction.
To forecast multiple future days, a recursive (autoregressive) strategy is used:

Predict the next trading day’s Close price

Insert the prediction back into the input sequence

Slide the time window forward

Repeat for the desired number of days

This approach is standard in real-world forecasting systems but comes with known limitations, such as error accumulation over longer horizons.

Interpretation of Predictions

All predictions represent future Close prices

A prediction for “Day 1” corresponds to the next trading day

Predictions can only be evaluated after the market closes

Weekends and market holidays are automatically skipped

Limitations

Open, High, Low, and Volume are assumed to remain similar to the last observed values during future prediction

The model does not account for:

News events

Earnings announcements

Macroeconomic indicators

Error increases as the forecast horizon extends

This project is intended for educational and analytical purposes, not live trading.

Possible Improvements

Predict returns instead of raw prices

Multi-output prediction of OHLC values

Incorporation of market indices (S&P 500, NASDAQ)

Probabilistic forecasting with confidence intervals

Walk-forward validation

Disclaimer

This project does not constitute financial advice, for educational purposes only.
Predictions are based purely on historical price patterns and should not be used for real-world investment decisions.

Author 

Chukwuma Samuel Ifeanyichukwu

chukwumasamuel27@gmail.com


