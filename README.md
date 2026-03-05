## Quantitative Developer Assignment – Financial Data Extraction, Processing, and Analysis

This repository contains a Jupyter notebook, `main.ipynb`, that implements the **\"Quantitative Developer Assignment: Python, Financial Data Extraction, Processing, and Analysis\"** based on Yahoo Finance market data.

The notebook follows a professional, end‑to‑end workflow: **data extraction, cleaning and preprocessing, feature engineering, analytics, visualisation**, and an optional **moving‑average crossover strategy**.

---

## Project Structure

- **`main.ipynb`**: Core analysis notebook (data fetching, cleaning, feature engineering, analytics, visualisations, and strategy evaluation).
- **`README.md`**: This documentation file describing how to set up, run, and interpret the project.
- *(Optional)* Additional data or configuration files can be added as needed (the notebook can fetch data directly from Yahoo Finance at runtime).

---

## Assignment Mapping

The notebook is organised to address the assignment parts as follows:

- **Part 1 – Data Extraction**: Uses `yfinance` to download at least 3 years of daily OHLCV data (Open, High, Low, Close, Volume) for three stock tickers and load them into `pandas` DataFrames.
- **Part 2 – Data Cleaning and Preprocessing**: Converts the date column to a proper datetime index, aligns all tickers to a common trading period, and prepares tidy DataFrames for analysis.
- **Part 3 – Feature Engineering**: Computes daily returns, log returns, 20‑day and 50‑day simple moving averages, and rolling 30‑day volatility of returns for each stock and stores them as additional columns.
- **Part 4 – Basic Analytics**: Derives summary statistics (mean daily return, standard deviation of returns, approximate annualised volatility) and a correlation matrix of daily returns across all tickers.
- **Part 5 – Visualisation**: Produces plots for price history (closing price vs. date), moving averages overlaid on price, and a correlation heatmap of daily returns.
- **Part 6 – (Optional) Strategy Evaluation**: Implements a simple 20/50‑day moving‑average crossover strategy for one stock and compares its cumulative return to a buy‑and‑hold benchmark.

Refer to the top markdown cells in `main.ipynb` for a more detailed narrative description of each step.

---

## Requirements

You will need Python 3.x and the following Python packages:

- `yfinance`
- `pandas`
- `numpy`
- `matplotlib`
- `seaborn` (if you want enhanced styling for plots)

Install dependencies with:

```bash
pip install yfinance pandas numpy matplotlib seaborn
```

If you prefer, you can create a virtual environment first:

```bash
python -m venv .venv
source .venv/Scripts/activate  # On Windows (bash)
```

---

## How to Run the Notebook

1. **Clone or download** this project folder to your local machine.
2. **Create and activate** a Python virtual environment (recommended).
3. **Install dependencies** as shown in the section above.
4. **Open** `main.ipynb` in Jupyter Lab, VS Code, or any compatible Jupyter environment.
5. **Run all cells in order**, from top to bottom:
   - Review the **Introduction** and **Environment Setup & Data Download** sections.
   - Adjust the list of tickers, date range, and interval parameters if required.
   - Execute the entire notebook to regenerate all results and plots.

When exporting or presenting the work (e.g. as HTML or PDF), ensure all cells have been run so that **tables, summary statistics, and charts appear inline under their markdown explanations**.

---

## Handling Missing Values and Data Quality

Yahoo Finance data is generally well‑behaved, but gaps can appear due to market holidays or symbol‑specific issues. In this implementation:

- **Primary assumption**: For the chosen tickers and 3‑year window, the core OHLCV data is mostly complete and aligned on trading days.\
- Where necessary, rows that contain missing values after alignment can be safely **dropped** before computing returns and summary statistics, to avoid propagating `NaN` into downstream calculations.\
- If you want more robust handling (e.g. forward‑filling or interpolation), you can extend the preprocessing section in `main.ipynb` and clearly mark the strategy used (e.g. `ffill` for short gaps).

You should document any additional cleaning logic you add, especially if you decide to fill or interpolate missing values instead of dropping them.

---

## Moving Average Strategy (Optional Part 6)

The optional strategy component implements a **simple moving‑average crossover strategy** for one selected stock (for example, NVDA):

- **Signals**:
  - Go **long** when the 20‑day simple moving average (`SMA_20`) crosses above the 50‑day simple moving average (`SMA_50`).
  - Exit (or go to cash) when `SMA_20` crosses back below `SMA_50`.
  - A `crossover` indicator column is used to encode whether the short‑term average is above or below the long‑term average.
- **Performance**:
  - Strategy returns are computed based on these signals and compared against a **buy‑and‑hold** benchmark over the same period.
  - Cumulative returns for both strategies can be plotted and/or printed in the notebook to allow visual and numerical comparison.

This satisfies the optional **Part 6** requirements from the assignment brief.

---

## Assumptions

- **Ticker choice**: The default configuration uses three large, liquid US equities (e.g. `AAPL`, `TSLA`, `NVDA`) to satisfy the \"three stock tickers\" requirement, but you can substitute any valid Yahoo Finance symbols.
- **Time horizon**: The default download window covers at least **3 years** of daily data as required; you can adjust this via the period/date parameters.
- **Trading costs**: The moving‑average strategy ignores transaction costs, slippage, and taxes; it is meant purely as a conceptual demonstration.
- **Data source**: All prices and volumes are pulled directly from **Yahoo Finance** via `yfinance`, and are assumed to be accurate for the purposes of this assignment.

If you deviate from these assumptions (e.g. different tickers, longer horizons, alternative cleaning), update this section to reflect your choices.

---

## Customisation

- **Change tickers**: Update the `symbols` list near the top of the notebook to analyse different stocks or instruments.
- **Change time horizon**: Modify the `data_period`, `start`, or `end` parameters used in the download helper to focus on different time windows.
- **Change interval**: Adjust the `interval` argument (e.g. `1d`, `1wk`, `1mo`) depending on the granularity required.

---

## Summary

This project demonstrates the full pipeline expected of a quantitative developer for this assignment: **programmatic data extraction**, **time‑series preprocessing**, **feature engineering**, **basic quantitative analytics**, **clear visualisations**, and an **interpretable trading strategy prototype**, all documented in a single, reproducible Jupyter notebook.

