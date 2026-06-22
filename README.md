# Markowitz vs . Hierarchical Risk Parity (HRP)

This is a Python project comparing three portfolio optimization methods: traditional mean variance optimization (Markowitz), optimization for Conditional value at risk (Cvar) and Hierarchical Risk Parity (HRP). 

The goal is to test how models perform in an out of sample walk forward backtest, specifically looking at how sensitive they are to parameter changes (overfitting).

## What it does

* **Data collection:** Pulls historical data for a mix of ETFs (equities, bonds, smart beta, commodities) using `yfinance`.
* **Markowitz optimization:** Uses `cvxpy` to maximize risk adjusted returns. Includes strict constraints (max 70% per asset, min 3% per asset) to force a realistic, tradeable portfolio.
* **CVar optimization:** Same as Markowitz, but instead of mean variance the model penalizes Conditional value at risk
* **HRP optimization:** Uses `scipy` to group assets based on correlation. It maps correlations to distances, builds a dendrogram (hierarchical clustering), and allocates weights using recursive bisection based on inverse variance. It does not require expected returns.
* **Walk forward backtesting:** Simulates actual trading. Trains the model on a past window (lookback), holds the portfolio for a set period (step), and then rebalances.
* **Grid search:** Runs both algorithms through multiple combinations of lookback and rebalancing windows. Outputs heatmaps to visualize parameter sensitivity.
