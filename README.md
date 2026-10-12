# Telecom Customer Churn Prediction

Predicting which customers may cancel their service to help a telecom company plan retention efforts.

**Project type:** Classification | **Tools:** Python, Pandas, NumPy, scikit-learn, Matplotlib, Seaborn

## Main result

Gradient Boosting was selected as the final model. At the default 0.50 classification threshold, the notebook reports these test results:

| Metric | Result |
| --- | ---: |
| Accuracy | 88.8% |
| Precision | 86.5% |
| Recall | 71.9% |
| F1-score | 0.785 |
| ROC-AUC | 0.942 |

Precision shows how often a churn warning was correct. Recall shows how many customers who actually left were found. The model identified 269 of the 374 customers who churned in the test set.

![Model ROC curves](images/roc_curves.png)

## Business question

Which customers are most likely to leave, and where should the company focus its efforts to keep them?

## Data and workflow

- Started with 7,043 customers and 38 columns reflecting account status at the end of Q2 2022.
- Excluded recently joined customers, leaving 6,589 customers with stayed-or-churned outcomes.
- Investigated missing values and filled service-related values based on whether customers had that service.
- Removed customer IDs, location columns, and columns that directly reveal churn outcomes before modeling.
- Converted categories into model inputs and used an 80/20 stratified train-test split with `random_state=2026`.
- Compared KNN, Logistic Regression, Decision Tree, Random Forest, and Gradient Boosting.
- Used five-fold cross-validation for tuning and explored the tradeoff between precision and recall.

## Model comparison

These are the saved test results for the versions selected in the notebook's final comparison.

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
| --- | ---: | ---: | ---: | ---: | ---: |
| KNN | 0.810 | 0.653 | 0.709 | 0.679 | 0.876 |
| Logistic Regression | 0.856 | 0.751 | 0.735 | 0.743 | 0.917 |
| Decision Tree | 0.867 | 0.818 | 0.684 | 0.745 | 0.922 |
| Random Forest | 0.885 | 0.861 | 0.711 | 0.779 | 0.938 |
| Gradient Boosting | 0.888 | 0.865 | 0.719 | 0.785 | 0.942 |

## Key findings

- Newer customers and customers with month-to-month contracts had higher churn rates.
- Customers without Online Security or Premium Tech Support also had higher churn rates.
- Competitor-related reasons accounted for about 45% of reported churn.
- These patterns suggest areas for retention outreach, service improvements, and review of competitor offers.

Lowering the threshold to 0.45 found nine additional churners in the test set, but reduced precision to 82.5%. The notebook kept 0.50 as its final threshold.

## Files

- [Full notebook](telecom_customer_churn_prediction.ipynb): code, explanations, charts, and saved results.
- [Data instructions](DATA.md): required input and source information.
- `requirements.txt`: Python packages needed to run the notebook.
- `images/`: selected charts taken from the notebook's saved outputs.

## How to run

1. Obtain the original `telecom_customer_churn.csv` described in [DATA.md](DATA.md).
2. Place it beside the notebook.
3. Use Python 3.12 as a starting environment.
4. From this project folder, run `python -m pip install -r requirements.txt`.
5. Start Jupyter with `python -m jupyterlab`, open the notebook, and run the cells in order.

You can also read the saved notebook results without downloading the data or training the models.

## Limits and next steps

This is a portfolio analysis of a historical dataset. It does not show that any individual feature causes churn, or that outreach would prevent it. Models and the final threshold were compared using test-set results; a future evaluation should reserve a fresh holdout dataset after those choices are fixed. Prediction inputs should also be checked for availability before the cancellation date.

The repository preserves the supplied notebook and its saved results. Full execution was not repeated while preparing this repository because the original CSV was not supplied. Package versions are starting requirements rather than a fully verified environment lock.
