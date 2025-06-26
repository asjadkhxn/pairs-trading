THE Z SCORE PAIRS TRADING STRAT

This strategy applies a classic z-score-based approach to pairs trading, targeting mean reversion in the spread between Bank Nifty and Nifty implied volatility. To ensure the integrity of the input data, we address missing values with a two-tiered method: short gaps are forward-filled, while persistent gaps are imputed using a GARCH(1,1) model, which is well-suited for capturing volatility clustering typical of financial time series. 

The spread is monitored using a rolling window to dynamically compute its mean and standard deviation, allowing us to standardize deviations as a z-score. Trades are triggered when the z-score breaches ±2.0, with positions closed as the spread mean-reverts within ±0.5, and all risk is kept intraday by mandating flat positions at the close. Profit and loss are calculated per trade, factoring in both spread changes and realistic transaction costs. 

It's assumed that trades execute at observed levels without slippage or liquidity constraints, and that our statistical imputation (GARCH(1,1)) preserves the essential properties of the volatility series.

THE COINTEGRATIONS PAIRS TRADING STRAT

This enhanced model replaces the static z-score approach with a cointegration-based framework. Instead of assuming a fixed relationship between the two assets, the strategy continuously tests for cointegration using a rolling window and only trades when a statistically significant long-term equilibrium exists. 

The hedge ratio between Bank Nifty and Nifty is recalibrated at each step via rolling OLS regression, ensuring the spread reflects the true mean-reverting relationship at that moment. Trading signals are then generated from the standardized residuals (spread) of this dynamic relationship, rather than a simple difference. 

This approach adapts to changing market regimes, minimizes spurious trades, and only takes positions when the underlying statistical justification is robust in nature.

OBSERVATIONS

The cointegration approach outperformed the z-score method across most key metrics: it delivered a higher total P&L (40.66 vs. 31.26), a much stronger Sharpe ratio (1.24 vs. -0.25), and a lower absolute maximum drawdown (-3.33 vs. -8.02). Despite executing fewer trades, the cointegration strategy achieved a better win rate (38% vs. 26%), highlighting its greater selectivity and efficiency!

Thank You!
