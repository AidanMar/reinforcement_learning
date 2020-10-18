# reinforcement_learning
Research repo for the RL team.

# Reinforcement Learning 

Using deep reinforcement learning to generate trading signals for US Equities and Futures.
Backtesting will be done on Quantopian using self-serve data feature. 


## Resources and skills invovled 


Python: Tensorflow/PyTorch, Ray, OpenAI gym, 
Database: MongoDB 


## Data Sources 

Alpaca daily/minute bar data for US Equities 
https://alpaca.markets/docs/api-documentation/api-v2/market-data/

In-sample: 2008-01-01 to 2018-12-31
Out-of-sample: 2019-01-01 to 2020-09-30
Live out-of-sample: 


## Project stages 

Stage 1: Build a gym environment 

Build a gym environment to simulate rebalancing (daily/minute) for US Equities 
Design input space [Timestamp * features * n_assets] 
Design action space [n_assets] 
Find a suitable transaction cost model (fixed cost or depend on volatility of asset) 

The output from RL models is considered to be asset weights for rebalancing

The input space is log change of price and volume. 
At day T, the value stored is the log price[T] - log price[T-1] 

At the end of day T, we compute the target asset weights using OHLCV data up to day T,
the log return used for rebalancing is the log return of open price from day T+1 to day T+2. 
This corresponds to rebalancing on market open implemented on Quantopian 

Stage 2: Build RL models 

Build deep RL models using RLlib and Tensorflow to 
Store results in Quantopian-compatible format https://www.quantopian.com/docs/user-guide/tools/self-serve
Write a simple algo on Quantopian which runs a portfolio using these signals directly with recommended risk constraints 
