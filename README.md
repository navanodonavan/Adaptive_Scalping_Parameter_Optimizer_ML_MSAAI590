# Transformer-Based Follow-Through Prediction for Intraday Trading

This project develops a transformer-based framework that learns temporal patterns in intraday price action to predict follow-through for a defined VWAP reclaim long trade setup. The problem is framed as a supervised classification task at the time of trade entry, emphasizing trade selection and execution quality rather than direct price prediction.

Using two years of 5-minute data across COIN, NVDA, OKLO, PLTR, and TSLA, the pipeline engineers intraday features and pretrains a transformer encoder via masked reconstruction before fine-tuning it as a binary classifier. Rather than predicting overall market direction, the model focuses on improving trade management by identifying setups that justify extended holds versus short-term scalps.

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

A transformer-based framework to predict whether VWAP reclaim setups are likely to produce meaningful follow-through or require more conservative management.

Encoder architecture:
- Sequence Length: 48 Bars (Each 5M price data = 1 bar)
- Hidden Size: 64
- Attention Heads: 4
- Encoder Layers: 2
- Feedforward Network: 256

A transformer encoder is pretrained on the full set of unlabeled 5-minute price data. The input features consist of 16 engineered bar-level variables capturing returns, volatility, VWAP relative positioning, candle structure, and time of day effects. During fine-tuning, encoder is adapted to a supervised classification task using two-phase training strategy. Phase 1, encoder is frozen and only classification head is trained on a higher learning rate (1e-3). Phase 2, encoder is unfrozen and entire model is trained using learning rate (1e-4).

## Results

Model performance is evaluated from both a machine learning and trading perspective. In addition to prediction metrics, strategy performance is measured using cumulative profit and loss (P&L) through trade backtesting.

<img width="1170" height="664" alt="image" src="https://github.com/user-attachments/assets/f34ee086-e883-4218-bd13-cad10266e95b" />



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

## AI Usage Disclosure
This project was developed with the assistance of [ChatGPT and Claude Code] to help with code generation and debugging. All AI-generated code was manually reviewed, tested, and added to Jupyter Notebooks by myself. 
