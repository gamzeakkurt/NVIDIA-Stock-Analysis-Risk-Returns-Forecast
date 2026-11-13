
#  NVIDIA Stock Analysis:  Risk, Returns & Forecast

A data-driven look at NVIDIA (NVDA) stock over 25+ years: returns, risk, technical indicators, strategy backtests, walk-forward forecasting and Monte Carlo simulation, all with interactive Plotly charts.

> ⚠️ **Educational purpose only. This is not financial advice.** Past performance does not predict future results.

## What's inside

| # | Section | Question it answers |
|---|---------|---------------------|
| 1 | Data | Daily, split-adjusted prices from `yfinance` |
| 2 | The big picture | How did NVDA compare with the S&P 500, Nasdaq and chip peers? |
| 3 | Annotated timeline | Which events moved the stock? |
| 4 | Returns & risk | Volatility, drawdowns, Sharpe/Sortino, tail days |
| 5 | Technical indicators | SMA 50/200, RSI, MACD, Bollinger Bands |
| 6 | Backtest | Do popular technical strategies beat buy & hold? |
| 7 | Correlations & beta | How tied is NVDA to semiconductors and the market? |
| 8 | Seasonality | Best months and weekdays |
| 9 | Earnings reactions | How big are the moves around earnings? |
| 10 | Forecasting | Naive vs ARIMA vs LightGBM, walk-forward validated |
| 11 | Monte Carlo | A 1-year range of outcomes (10,000 paths) |
| 12 | Takeaways | Summary and limitations |

**Peers and benchmarks:** AMD, Intel, TSMC, Microsoft, S&P 500, Nasdaq Composite, PHLX Semiconductor Index (SOX).

## Key findings

*(Data through 13 Nov 2026. Re-running pulls fresh data, so numbers will drift.)*

- **Extraordinary compounding:** USD 1,000 in Feb 1999 grew to about USD 4.4M, versus about USD 6k for the S&P 500 and about USD 10k for the Nasdaq (price-only). Since 2015: 63.5% CAGR and a Sharpe ratio of 1.28 (S&P 500: 0.54).
- **A brutal ride:** drawdowns of -90% (2002), -85% (2008), -66% (2022) and -56% (2018). About 12% of all days moved more than ±5%.
- **Technical signals are not magic:** an SMA 50/200 trend filter beat buy & hold on Sharpe (0.69 vs 0.55); RSI mean-reversion and MACD lagged far behind.
- **Earnings are the big event:** average move of about 6.5% versus about 2% on a normal day, but the stock rose only about 54% of the time.
- **Forecasting daily moves is mostly noise:** LightGBM got the direction right 54% of the time against a 51% "always up" baseline, which is not statistically significant (p ≈ 0.10).
- **Think in ranges:** even with +15% annual drift assumed, the Monte Carlo gives about a 46% chance of being down after a year.

## Methodology notes

- **No look-ahead:** backtest signals are traded on the next day's return, with 0.05% transaction cost per position change.
- **Forecasting:** the target is the next-day return (not price level). Models are retrained on an expanding window and always predict unseen data. The baseline is a random walk.
- **Monte Carlo:** Geometric Brownian Motion with volatility from the last 3 years and three drift scenarios (bear, base, bull), since the drift is unknowable.

## Run it

You can run this code on [Kaggle](https://www.kaggle.com/code/gamzeakkurt/nvidia-stock-analysis-risk-returns-forecast)

**Locally:**

```bash
python -m venv .venv && source .venv/bin/activate
pip install yfinance plotly pandas numpy scipy scikit-learn lightgbm statsmodels matplotlib jupyter
jupyter notebook NVIDIA_Stock_Analysis.ipynb
```

Tested with Python 3.12.

## Limitations

- Single-stock, in-hindsight analysis: NVIDIA is a survivor and a winner, which flatters every buy & hold number.
- GBM assumes constant volatility and normal shocks; real returns have fat tails and volatility clusters.
- Backtests ignore taxes, slippage on large orders and dividends beyond the adjusted close.
- The timeline's event dates were entered by hand. Check them before relying on them.

## Ideas to extend

GARCH volatility models, options-implied volatility, news and earnings-call sentiment, regime-switching models, portfolio construction with the peers.

## Data

Yahoo Finance via [`yfinance`](https://github.com/ranaroussi/yfinance). Yahoo's terms apply to the underlying data.
