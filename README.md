# GROUP59_CENG313 — Hull Tactical Market Prediction

Course project for **CENG313 – Introduction to Data Science**.

## Team

| Name | Student ID | GitHub |
|------|------------|--------|
| Sadık Onur Hayta | 23118080046 | [@onurhayta](https://github.com/onurhayta) |

- **Group ID:** 59
- **Competition level:** Light (1 student)
- **Modality:** Time series

## Competition

- **Kaggle competition:** [Hull Tactical – Market Prediction](https://www.kaggle.com/competitions/hull-tactical-market-prediction)
- **Task:** For each trading day, choose an allocation to the S&P 500 in the range **[0, 2]**
  (0 = fully in cash / risk-free asset, 1 = fully invested, 2 = 2x leveraged). The rest of the
  capital earns the risk-free rate.
- **Evaluation metric:** A modified (volatility-adjusted) Sharpe ratio. The score is penalised when
  the strategy's volatility exceeds **1.2×** the market's volatility, and when the strategy's return
  falls below the market's return.
- **Competition format:** Code competition (predictions are served through Kaggle's evaluation API).
  Timeline: started 15 Sep 2025, final submission deadline 15 Dec 2025, ended 16 Jun 2026.

## Dataset

Daily, anonymised (`date_id`) tabular data that combines public market information with
Hull Tactical's proprietary signals.

| Prefix | Feature group |
|--------|---------------|
| `M*`   | Market dynamics / technical |
| `E*`   | Macro-economic |
| `I*`   | Interest rates |
| `P*`   | Price / valuation |
| `V*`   | Volatility |
| `S*`   | Sentiment |
| `MOM*` | Momentum |
| `D*`   | Binary / dummy indicators |

Targets in `train.csv`:

- `forward_returns` – next-day S&P 500 return
- `risk_free_rate` – federal funds rate
- `market_forward_excess_returns` – forward return relative to expectations

`test.csv` has the same features plus lagged target columns and an `is_scored` flag.

> The data files are **not** stored in this repository (see `.gitignore`).
> Download them from the competition's *Data* tab (see *How to run*).

## Repository structure

```
GROUP59_CENG313/
├── README.md
├── requirements.txt
├── assignment1_eda_baseline.ipynb   # Assignment 1: EDA + baseline models
├── assignment2_solution.ipynb       # Assignment 2: proposed solution (to be added)
├── data/                            # local data folder (git-ignored)
└── src/
    ├── __init__.py
    ├── data.py      # loading data, feature groups, time-series splits
    ├── models.py    # baseline and proposed models
    └── utils.py     # competition metric and evaluation helpers
```

## Approach

### Assignment 1 – EDA and baselines *(in progress)*

- Exploratory data analysis: missing-value structure over time, target distribution
  (fat tails, volatility clustering), feature–target relationships per feature group,
  stability of relationships over time.
- Validation: time-ordered **walk-forward** splits (no random shuffling, no look-ahead).
- Baselines:
  1. Constant allocation (buy-and-hold, `allocation = 1.0`)
  2. Constant extremes (`0.0`, `2.0`) as sanity checks
  3. Linear model (Ridge / Lasso) on features + simple allocation rule
  4. Gradient boosting (LightGBM) + simple allocation rule

### Assignment 2 – Proposed solution *(planned)*

To be defined after Assignment 1 (e.g. combining return and volatility forecasts to size positions).

## Results

| Model | Mean CV score | Notes |
|-------|---------------|-------|
| _to be filled_ | | |

## How to run

1. Open the notebook in Google Colab (*File → Open notebook → GitHub*, paste this repository's URL).
2. The first cell clones this repository so that the `src/` modules can be imported.
3. Download the competition data (`train.csv`, `test.csv`) from the
   [competition data page](https://www.kaggle.com/competitions/hull-tactical-market-prediction/data)
   and upload them to the `data/` folder in Colab.
4. Run all cells.

Locally:

```bash
git clone https://github.com/onurhayta/GROUP59_CENG313.git
cd GROUP59_CENG313
pip install -r requirements.txt
# put train.csv and test.csv into data/
jupyter notebook assignment1_eda_baseline.ipynb
```

## Progress log

| Date | Work done |
|------|-----------|
| 2026-10-29 | Repository created; README, project structure and `src/` modules added. Competition metric implemented in `src/utils.py`. Assignment 1 notebook skeleton added. |

## Kaggle submission history

| Date | Model / notebook version | Public score | Private score | Notes |
|------|--------------------------|--------------|---------------|-------|
| _none yet_ | | | | |