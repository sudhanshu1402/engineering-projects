# Machine Learning Basics

> Part of my public learning archive. For active, production-grade work see the pinned repositories on my [GitHub profile](https://github.com/sudhanshu1402).

Code written during college and self-study while learning foundational machine learning. It's kept public for transparency — a record of where I started. These are practice projects, not production systems: mostly Jupyter notebooks doing classification, regression, and statistical analysis with scikit-learn and statsmodels, plus one OpenCV image script.

The notebooks read data from Kaggle-style `../input/` paths, so they run as-is on Kaggle; locally you point the read paths at your own copy of the datasets.

## Projects

| Project | What it does | Stack |
|---|---|---|
| [fake-news-detection](./fake-news-detection) | Classifies news articles as real or fake. Cleans text with regex, vectorizes with TF-IDF, then trains and compares Logistic Regression, Decision Tree, Random Forest, and Gradient Boosting. Holds out 10 rows per class for manual testing. | pandas, scikit-learn |
| [housing-prices-prediction](./housing-prices-prediction) | Exploratory analysis of the California housing dataset — info/describe, boxplots and histograms, then train/test splitting including stratified sampling on an income-category bucket. | pandas, seaborn, scikit-learn |
| [price-elasticity-of-demand-analysis](./price-elasticity-of-demand-analysis) | OLS regression of beef quantity on price to estimate price elasticity, with regression diagnostic plots and a recursive least-squares / CUSUM stability check over time. | statsmodels, pandas |
| [cartoonify-image](./cartoonify-image) | Tkinter desktop app that turns a photo into a cartoon: grayscale → median blur → adaptive-threshold edges → bilateral color filter, masked together. Shows the 6-step transition and saves the result. | OpenCV, NumPy, matplotlib, Tkinter |

## Running these

The three notebooks:

```bash
pip install pandas numpy scikit-learn seaborn matplotlib statsmodels
jupyter notebook
```

Each has a `*-with-output.ipynb` companion so you can read the results without running anything.

The cartoonify script:

```bash
pip install opencv-python numpy matplotlib pillow imageio easygui
python cartoonify-image/cartoonify_image.py
```

Note: `cartoonify_image.py` has a hardcoded Windows `ImagePath` in the `upload()` function — edit it to point at `bros.jpg` (included) or your own image before running.

## Overview
- **Focus:** regression, classification, and statistical analysis
- **Core tools:** scikit-learn, statsmodels, pandas, OpenCV
- **Timeframe:** college / early self-study
