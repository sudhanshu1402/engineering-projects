# Fake News Detection

Text classifier that labels a news article as real or fake, trained on the Kaggle Fake/True news dataset. A learning project done in a single Jupyter notebook.

## What it does

Takes the body text of a news article and predicts whether it's fake (`0`) or real (`1`). The pipeline is the standard NLP-classification flow:

1. Load the fake and true CSVs, tag each with a `class` label.
2. Clean the text (lowercase, strip punctuation, URLs, HTML tags, bracketed text, and words containing digits) with a regex-based `wordopt` function.
3. Convert text to TF-IDF vectors.
4. Train four scikit-learn classifiers and compare them.
5. Feed in your own text for a manual prediction from all four models.

Only the article `text` column is used — `title`, `subject`, and `date` are dropped, so the model learns from article body alone.

## Data

Two CSVs from the Kaggle "Fake and real news" dataset, expected at `../input/fake-news-detection/`:

- `Fake.csv` — ~23,481 fake articles
- `True.csv` — ~21,417 real articles

The last 10 rows of each are pulled aside before training and saved to `manual_testing.csv` for out-of-sample sanity checks. The rest is merged, shuffled, and split 75/25 into train/test (~11,220 test rows).

## Models and results

TF-IDF features, default scikit-learn hyperparameters (except `random_state`). Accuracy on the held-out test set from the executed run:

| Model | Test accuracy |
|---|---|
| Logistic Regression | 98.88% |
| Decision Tree | 99.62% |
| Gradient Boosting | 99.50% |
| Random Forest | 99.13% |

These numbers are high because this dataset is known to be easy — fake and real articles come from different sources with distinct stylistic tells, so the models pick up on source signal, not just "truthfulness." Treat the accuracy as a property of the dataset, not proof of a general fake-news detector.

## Stack

- Python, Jupyter
- pandas, numpy
- scikit-learn (`TfidfVectorizer`, `LogisticRegression`, `DecisionTreeClassifier`, `GradientBoostingClassifier`, `RandomForestClassifier`)
- matplotlib, seaborn (imported; plotting is minimal)

## Run it

Install deps:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn jupyter
```

Download the dataset from Kaggle ("Fake and real news dataset") and place `Fake.csv` and `True.csv` under `../input/fake-news-detection/` relative to the notebook, or edit the two `pd.read_csv` paths in the import cell.

Then:

```bash
jupyter notebook fake-news-detection.ipynb
```

Run the cells top to bottom. Gradient Boosting is the slow one — training takes a while on the full set.

## Manual testing

The last cells let you paste article text and see what each model predicts:

```python
news = str(input())
manual_testing(news)
```

Output:

```
LR Prediction: Not A Fake News
DT Prediction: Not A Fake News
GBC Prediction: Not A Fake News
RFC Prediction: Not A Fake News
```

`manual_testing` reuses the same `wordopt` cleaning and the fitted TF-IDF vectorizer, so input is transformed exactly like the training data.

## Files

- `fake-news-detection.ipynb` — the notebook (code only)
- `fake-news-detection-with-output.ipynb` — same notebook with cell outputs saved

## Scope

Practice project for learning the TF-IDF + classic-classifier workflow. No hyperparameter tuning, no cross-validation, no model persistence, and no train/test source separation to guard against leakage. Good for understanding the pipeline; not a production fact-checker.
