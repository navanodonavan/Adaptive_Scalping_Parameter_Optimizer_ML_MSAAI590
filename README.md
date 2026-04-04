# Transformer-Based Follow-Through Prediction for Intraday Trading

This project develops a transformer-based deep learning framework for predicting trade follow-through in intraday trading. Rather than forecasting price direction, the model estimates the probability that a trade setup will achieve meaningful follow-through after entry. The goal is to improve trade selection by filtering out lower-quality setups and supporting more consistent execution in rapidly changing market conditions.

The study focuses on five high-liquidity equities: TSLA, NVDA, COIN, OKLO, and PLTR. Using two years of 5-minute OHLCV data from Alpaca Markets, VWAP Reclaim Long opportunities were identified and labeled through forward trade simulation. A transformer model was then trained on recent intraday price and volume sequences to predict follow-through probability at the time of entry.

## Repository Structure

- **0.0 Stock Data Extraction.ipynb** – retrieves 5-minute OHLCV data from Alpaca Markets (Historical Bars REST API)
- **0.1 EDA Feature Engineering.ipynb** – performs exploratory analysis, builds intraday features, systematically identifies all VWAP Reclaim trade entries, and simulates Oracle hindsight best trade outcomes for all VWAP Reclaim setups.  
- **0.2 Self Supervised Transformer PreTrain.ipynb** – pretrains the transformer on sequential market data  
- **0.3 Transformer Fine Tuning.ipynb** – fine-tunes the encoder model for follow-through prediction, including training a classification head, and evaluates model predictions
- **0.4 In-Sample Backtesting.ipynb** – backtests trading performance on held-out test dataset using model predictions
- **0.5 Out-of-Sample Backtesting.ipynb** – backtests trading performance on unseen out of sample dataset using model predictions

## Workflow

1. Extract intraday stock data from Alpaca Markets  
2. Consolidate and clean the dataset  
3. Engineer price, volatility, momentum, and volume-based features  
4. Identify VWAP Reclaim Long trade opportunities  
5. Label trade outcomes using forward simulation  
6. Train and fine-tune a transformer model  
7. Evaluate prediction quality and trading performance  

## Data

The dataset consists of two years of 5-minute OHLCV data for TSLA, NVDA, COIN, OKLO, and PLTR, for a combined total of 401,473 records. These securities were selected due to their high liquidity, strong retail participation, and meaningful intraday price movement.

Engineered features include:
- Volume impulse
- Average True Range (ATR)
- Multi-horizon returns
- Realized volatility

The project centers on the **VWAP Reclaim Long** setup, where price reclaims VWAP with elevated relative volume. Trade outcomes are labeled based on whether the setup reaches a profit target before hitting a stop-loss or timing out.

## Model Approach

The transformer model is trained on sequences of recent intraday price and volume features to predict the probability of trade follow-through at entry. This allows the model to capture temporal dependencies in price action leading up to each signal.

Instead of predicting whether price will go up or down, the model is designed to support **trade selection**, helping filter trades based on estimated quality.

## Results

Model performance is evaluated from both a machine learning and trading perspective. In addition to prediction metrics, strategy performance is measured using cumulative profit and loss (P&L) through trade backtesting.

<img width="1069" height="600" alt="image" src="https://github.com/user-attachments/assets/29dfe174-b411-49a0-9475-5125deaffc1b" />


## How to Run

Run the notebooks in this order:

1. `0.1 EDA Feature Engineering.ipynb`
2. `0.2 Self Supervised Transformer PreTrain.ipynb`
3. `0.3 Transformer Fine Tuning.ipynb`
4. `0.4 In-Sample Backtesting.ipynb`
5. `0.5 Out-of-Sample Backtesting.ipynb`

Stock OHLCV Data CSV files can be found in artifacts folder.

## Future Improvements

- Expand to a larger stock universe  
- Add real-time inference using broker API data  
- Test additional trade setups beyond VWAP Reclaim Long  
- Improve model tuning and threshold optimization  

## Disclaimer

This project is for educational and research purposes only. It is not financial advice.
