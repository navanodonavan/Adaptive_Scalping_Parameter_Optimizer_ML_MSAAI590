# Project Title : Adaptive Scalping Parameter Optimization System

This project is for the Capstone in the Applied Artificial Intelligence Program at the University of San Diego (USD). 

### Project Status: [In Progress]

## Instructions

TBD

## Project Intro/Objective

Retail traders face increasing competitive pressure in modern electronic markets, motivating the exploration of artificial intelligence (AI) methods to enhance adaptive trading performance. In recent years, financial markets have exhibited elevated volatility and sustained growth in trading volume across both institutional and retail participants. A critical challenge for retail traders competing with institutional and algorithmic systems is the ability to adapt execution strategies to shifting market conditions (regimes). Market conditions frequently transition across volatility and liquidity states within short time horizons, often spanning days to weeks. Delayed recognition of these transitions can result in parameter choices optimized for prior conditions, leading to performance degradation under the current regime. 


### Project Description

The study utilizes two years of 5-minute TSLA,COIN,NVDA,OKLO,PLTR price data. VWAP Reclaim Long trade opportunities were systematically identified, and a simulation engine evaluated a predefined grid of stop, target, and hold-time parameters to estimate historically optimal trade parameters for each trade opportunity. Rule based regime classification is defined based on volatility, volume impulse, and price structure. A transformer based deep learning model is then trained to classify regimes for real-time regime inference. Finally, a supervised optimization model maps regime predictions to the best performing trade parameter bins. 
