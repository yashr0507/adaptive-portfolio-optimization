# Adaptive Portfolio Optimization

A quantitative finance project investigating how **dynamic portfolio optimization and rebalancing** affect portfolio risk and performance.

The project combines rolling risk estimation, constrained optimization, walk-forward backtesting, market-regime analysis, transaction costs, and robustness testing across approximately 10 years of historical market data.

## Research Question

> Can dynamically re-optimized portfolios improve risk-adjusted performance while controlling volatility, concentration, and transaction costs?

## Asset Universe

The portfolio contains 10 investable assets:

**AAPL (Apple), NVDA (NVIDIA), JPM (JP Morgan), KO (Coca-Cola), XOM (Exxon Mobil), MC.PA (LVMH / Louis Vuitton Moët Hennessy), AMZN (Amazon), GC=F (Gold Futures), TLT (Long-Term Treasury Bond ETF), JNJ (Johnson & Johnson)**

The **S&P 500 (`^GSPC`)** is used as the benchmark, while **13-week Treasury Bills (`^IRX`)** provide the risk-free-rate proxy.

## Methodology

### Dynamic Risk Estimation

* 30-day rolling covariance and correlation
* Rolling portfolio volatility
* Dynamic risk estimates used by the optimization engine

### Constrained Optimization

Portfolio weights are optimized using **SLSQP** to maximize the Sharpe ratio subject to:

* Long-only positions
* Maximum 20% individual asset weight
* AAPL + NVDA ≤ 35%
* JPM ≤ 25%
* Annualized volatility target ≤ 20%

### Walk-Forward Backtesting

The portfolio is re-optimized using only information available at each point in time, avoiding look-ahead bias.

Two strategies are tested:

* Monthly rebalancing
* Quarterly rebalancing

Portfolio drift and turnover are tracked between rebalancing dates.

### Risk & Performance

Strategies are evaluated using:

* CAGR
* Annualized volatility
* Sharpe ratio
* Maximum drawdown
* Calmar ratio
* Downside risk
* Rolling Sharpe ratio
* Portfolio turnover

Transaction costs are also incorporated and tested across multiple cost assumptions.

### Market Regimes

S&P 500 30-day rolling volatility is used to classify periods into:

**Low | Normal | High volatility**

Portfolio performance and allocation changes are then compared across regimes.

### Robustness Testing

The optimization is tested under different:

* Volatility targets: **15%, 20%, 25%**
* Maximum asset weights: **15%, 20%, 25%**
* Transaction costs: **1–50 bps**

## Key Results

The backtest found that **Equal Weight produced the highest raw CAGR**, while **Adaptive Monthly produced the strongest risk-adjusted performance**.

| Strategy           |   CAGR | Volatility | Sharpe | Max Drawdown |
| ------------------ | -----: | ---------: | -----: | -----------: |
| S&P 500            | 13.79% |     18.14% |   0.68 |      -33.93% |
| Equal Weight       | 21.94% |     14.86% |   1.27 |      -24.99% |
| Adaptive Monthly   | 20.59% |     12.85% |   1.36 |      -17.07% |
| Adaptive Quarterly | 16.55% |     13.53% |   1.04 |      -22.96% |

**Main finding:** Adaptive Monthly achieved the highest Sharpe ratio and lowest volatility and maximum drawdown among the strategies tested.

## Visualizations

The project includes visualizations of:

* Portfolio wealth and drawdowns
* Rolling correlation
* Rolling volatility
* Rolling Sharpe ratios
* Adaptive portfolio allocations
* Market-regime allocations
* Robustness analysis
* Transaction-cost sensitivity

## Technology

**Python · Pandas · NumPy · SciPy · Matplotlib · Seaborn · yfinance**

## Limitations

This is a historical backtest and does not guarantee future performance. Transaction costs, market impact, taxes, slippage, and liquidity constraints are simplified. Optimization results may also depend on the chosen estimation window and constraints.

## Project Structure

```text
project8-adaptive-portfolio-optimization/
├── portfolio_optimization.ipynb
├── rolling_correlation.png
├── wealth_comparison.png
├── drawdown_comparison.png
├── monthly_adaptive_allocation.png
├── monthly_weights_by_regime.png
├── quarterly_weights_by_regime.png
├── robustness_sharpe.png
├── transaction_cost_sensitivity.png
├── rolling_volatility_comparison.png
└── rolling_sharpe_comparison.png
```
