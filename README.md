# Forecasting Stock Returns and Evaluating Trading Strategies

This repository contains the final presentation for a group project on short-horizon stock return forecasting and rule-based trading strategies.

We use daily US equity return and market factor data to build a simple predictive model for stock returns and evaluate a trading strategy on large-cap stocks.

---

## 🧠 Project Overview

**Click the link below to view the full presentation and analysis directly in your browser:**

* **[View Project: Data-Driven_Stock_Trading_Strategy.html](https://github.com/Anintony/Building-and-Backtesting-a-Data-Driven-Stock-Trading-Strategy/blob/main/Data-Driven_Stock_Trading_Strategy.html)**

The main goals of this project are:

1. **Clean and prepare** daily stock return data for individual stocks and market-wide factors.
2. **Build a forecasting model** for short-horizon (daily) returns using lagged returns and factor variables.
3. **Design a trading strategy** that takes model forecasts as signals.
4. **Evaluate performance** of the strategy using standard portfolio metrics and compare it to a buy-and-hold benchmark.

The analysis is presented in the HTML slide deck in this repository.

---

## 📊 Data

We work with daily return data for:

- **Individual stocks**: e.g., Apple (AAPL) and Microsoft (MSFT).
- **Market-level variables**: value-weighted and equal-weighted market returns, and a spread return series.

Typical columns in the raw data include:

- `PERMNO`, `date`, `TICKER`
- `PRC`, `OPENPRC`, `VOL`
- `RET` (individual stock return)
- `vwretx`, `ewretd`, `sprtrn` (market/factor returns)

> **Note:** The original CSV files (e.g., `AAPL.csv`, `MSFT.csv`) are not included in this repository due to data access and licensing.  
> To fully reproduce the analysis, you will need access to a similar daily returns database and align the column names to match the code used in the presentation.

---

## ⚙️ Methodology

The project is structured into four main parts, matching the sections of the presentation.

### Part 0. Cleaning

- Remove duplicate rows for each ticker.
- Handle missing values in returns and factor series.
- Ensure consistent date ranges and alignment across all series.
- Compute daily returns where necessary and confirm that columns are correctly typed.

### Part 1. Model

**Exploratory Data Analysis**

- Visualize price levels and returns over time for selected stocks.
- Plot return distributions and summary statistics.
- Inspect correlations between candidate predictors (lagged returns, factor variables) and next-day returns.

**Model Building**

- Construct a regression model where the dependent variable is next-day stock return.
- Candidate predictors include:
  - Lagged stock returns (e.g., 1-day, 2-day, 3-day lags).
  - Market/factor returns over recent windows.
- Use correlation screening / variable selection to choose a set of final factors.
- Estimate the model with ordinary least squares.

**Model Optimization**

- Evaluate in-sample fit and residual diagnostics.
- Adjust the set of predictors if necessary to avoid multicollinearity and overfitting.
- Generate out-of-sample **predicted returns** to be used as trading signals.

### Part 2. Trading Strategy

**Signal Construction**

- For each day, use the model-predicted return as a trading signal.
- Example rule:
  - Go **long** the stock when the predicted return is positive.
  - Stay **out of the market** (or reduce exposure) when the predicted return is negative or below a threshold.

**Bet Sizing**

- Translate signals into portfolio weights (position sizes).
- Ensure that position sizes are realistic and do not exceed reasonable leverage constraints.

**Portfolio Returns**

- Compute daily strategy returns based on:
  - The chosen position sizes.
  - The realized stock returns.
- Construct cumulative return series for:
  - The strategy.
  - A buy-and-hold benchmark in the same stock.

### Part 3. Performance Evaluation

- Use portfolio analytics tools to compute:
  - Cumulative returns.
  - Annualized mean excess return.
  - Volatility and **Sharpe ratio**.
  - Other standard risk–return metrics as needed.
- Plot and compare:
  - Strategy cumulative returns vs. buy-and-hold.
  - Drawdowns and performance in different market regimes.
- Discuss:
  - Where the strategy outperforms.
  - Periods where signals fail or underperform the benchmark.
  - Limitations of the model (e.g., transaction costs, overfitting, stability).

---

## 📁 Repository Structure


```text
.
├── Final-Presentation.html       # Final HTML slide deck
└── README.md
