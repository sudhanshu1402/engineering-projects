# Housing Price Prediction

A worked-through Jupyter notebook that predicts California district median house values from census data. It follows the end-to-end regression project from *Hands-On Machine Learning with Scikit-Learn & TensorFlow* (Chapter 2), start to finish.

## What this is

A learning notebook, not a product. It walks the full supervised-learning workflow on the California Housing dataset (20,640 districts, 10 columns) and explains each step in markdown as it goes:

1. Load the data and inspect types, stats, and missing values.
2. Explore with boxplots, histograms, geographic scatter plots, and correlation analysis.
3. Split into train/test using both random and stratified sampling (stratified on an income category), and compare which better matches the population distribution.
4. Engineer combined features: `rooms_per_household`, `bedrooms_per_room`, `population_per_household`.
5. Clean and transform: median imputation for missing `total_bedrooms`, one-hot encoding for `ocean_proximity`, standard scaling, all wired into a Scikit-Learn `Pipeline` + `FeatureUnion`.
6. Train and compare three models: Linear Regression, Decision Tree, Random Forest.
7. Validate with 10-fold cross-validation, tune the Random Forest with `GridSearchCV`, read off feature importances, and report final RMSE on the held-out test set.

The dataset itself is not in this folder — the notebook reads it from `../input/housing.csv` (plus `../input/anscombe.csv` for one illustration), matching the Kaggle kernel layout it was written in.

## Files

| File | Notes |
|------|-------|
| `housing-prices-prediction.ipynb` | The notebook, code + explanatory markdown, no saved output |
| `housing-prices-prediction-with-output.ipynb` | Same notebook with all cell outputs and plots rendered (~1 MB) |

If you just want to read it, open the `-with-output` version — the charts and results are already there, no need to run anything.

## Stack

- Python 3
- NumPy, pandas
- Scikit-Learn
- Matplotlib, Seaborn

## Running it

Heads up: this was written against an older Scikit-Learn (roughly pre-0.20) and will not run as-is on a current install. Known breakages:

- `from sklearn.preprocessing import Imputer` — moved to `sklearn.impute.SimpleImputer`.
- `from pandas.tools.plotting import scatter_matrix` — now `pandas.plotting.scatter_matrix`.
- `sns.barplot(op_count.index, op_count.values, ...)` — positional args, needs `x=`/`y=` on modern Seaborn.
- `sns.lmplot(..., size=4)` — `size` was renamed to `height`.
- A hand-rolled `CategoricalEncoder` class is included (copied from a Scikit-Learn PR at the time) to work around `LabelBinarizer` not fitting inside a pipeline; modern code would just use `OneHotEncoder` / `ColumnTransformer`.

To run the original as-is, pin an old environment:

```bash
pip install "scikit-learn<0.20" "pandas<0.23" numpy matplotlib seaborn jupyter
jupyter notebook housing-prices-prediction.ipynb
```

Then place `housing.csv` and `anscombe.csv` in an `input/` directory one level up from the notebook.

## What the model actually does

The end product is a `RandomForestRegressor` tuned by grid search over `n_estimators` and `max_features` (18 combinations, 5-fold CV). Predicting a few sample districts:

```python
some_data_prepared = full_pipeline.transform(some_data)
final_model.predict(some_data_prepared)
```

Rough results the notebook lands on (numbers move a little each run since some estimators aren't seeded):

- Linear Regression: ~68,600 training RMSE, ~69,000 CV RMSE — underfitting.
- Decision Tree: 0 training RMSE, ~71,500 CV RMSE — textbook overfitting.
- Random Forest: best of the three; lowest cross-validation RMSE, carried through to the final test-set evaluation.

Given median house values run into the hundreds of thousands, an RMSE in the tens of thousands is mediocre — the notebook is honest about that and treats it as a starting point, not a finished model.

## Worth pointing out

- The stratified vs. random sampling comparison is the most useful takeaway: it shows random splits can skew a feature's distribution and why stratifying on income fixes it.
- `bedrooms_per_room` (the engineered ratio) correlates with price far more strongly than raw room or bedroom counts — a small feature-engineering win the notebook calls out explicitly.
- Everything lives in one pipeline, so the exact same transforms applied to training data are applied to the test set with `transform` (never `fit_transform`) — the correct way to avoid leaking test statistics.

## Scope

Practice project for learning the Scikit-Learn workflow. No CLI, no saved model, no tests. The value is in reading it, not deploying it.
