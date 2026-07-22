# Price Elasticity of Demand Analysis

A Jupyter notebook that estimates how beef demand responds to price, using linear regression in statsmodels.

## What it does

Price elasticity of demand measures how much quantity sold changes when price changes. This notebook fits a regression of quantity on price against 91 quarters of U.S. beef data (1977–1999) and reads the elasticity off the slope.

The workflow:

1. Load `beef.csv` and check for missing values.
2. Fit an Ordinary Least Squares (OLS) model, `Quantity ~ Price`.
3. Inspect the fit with statsmodels diagnostic plots — partial regression, CCPR, and regression-vs-exog grids.
4. Re-run the fit as a Recursive Least Squares (RLS) model over time to check whether the price coefficient is stable across the sample, using recursive-coefficient and CUSUM plots.

### Result from the notebook run

OLS gives:

```
Quantity = 30.05 - 0.0465 * Price     R-squared = 0.901
```

The price coefficient is -0.0465 (p < 0.001): each unit of price is associated with about 0.047 less quantity. R-squared of 0.90 means price alone explains most of the variation in quantity. The CUSUM statistic stays inside the 5% bands, so the relationship looks stable over the whole 1977–1999 period — no evidence the parameters drift.

## Data

`beef.csv` — quarterly observations with columns `Year`, `Quarter`, `Quantity`, `Price`.

```
Year  Quarter  Quantity   Price
1977  1        22.9976    142.1667
1977  2        22.6131    143.9333
1977  3        23.4054    146.5000
...
```

Note: the CSV is not committed in this folder. The notebook expects `beef.csv` alongside it. It's a standard statsmodels demo dataset (U.S. beef consumption); drop the file in this directory before running.

## Stack

- Python 3
- pandas, numpy
- statsmodels (OLS, `RecursiveLS`, and the `sm.graphics` diagnostic plots)
- matplotlib

The imports (`from __future__ import print_function`, `statsmodels.compat.lzip`) date the notebook to an older Python 2/3 era; it was last run on statsmodels ~2018.

## Run it

```bash
pip install jupyter pandas numpy statsmodels matplotlib
jupyter notebook price-elasticity-of-demand.ipynb
```

Then run the cells top to bottom. Make sure `beef.csv` is in the same directory first.

## Notable details

- **RLS as a stability check.** OLS gives one coefficient for the whole sample. RLS re-estimates the coefficients as each new datapoint arrives, so the recursive-coefficient plot shows whether elasticity shifted over 22 years. The final RLS estimate matches OLS exactly (`-0.0465`), as expected.
- **CUSUM test.** The `plot_cusum` output is the formal version of "did the parameters stay stable?" — staying inside the bands means you can't reject stability at the 5% level.
- **Date handling.** `Year` and `Quarter` are combined into a proper quarterly `DatetimeIndex` (`BQuarterBegin`) before the time-series RLS step.

## Scope

A learning notebook working through statsmodels regression and diagnostics on one dataset. It demonstrates the tools; it isn't a general elasticity library.
