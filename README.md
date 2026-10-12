# Telecom Customer Churn Prediction

Predicting which customers may cancel their service to help a telecom company plan retention efforts.

**Project type:** Classification | **Tools:** Python, Pandas, NumPy, scikit-learn, Matplotlib, Seaborn, Google Colab

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

## Data Source

This project uses the [Telecom Customer Churn dataset from Maven Analytics](https://mavenanalytics.io/data-playground/telecom-customer-churn). It describes a fictional telecom company serving 7,043 customers in California during Q2 2022. Maven Analytics credits IBM Cognos Analytics as the original source.

The input used in this notebook is `telecom_customer_churn.csv`, with 7,043 rows and 38 columns.

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
- `requirements.txt`: Python package requirements for reference or installation if needed.
- `images/`: selected charts taken from the notebook's saved outputs.

## How to run in Google Colab

1. Open [Google Colab](https://colab.research.google.com/) and upload `telecom_customer_churn_prediction.ipynb` using **File > Upload notebook**.
2. Obtain the original `telecom_customer_churn.csv` described in [DATA.md](DATA.md).
3. Upload the CSV through Colab's **Files** panel. Keep its filename unchanged and place it in the runtime's working folder, normally `/content`, because the notebook reads it using a relative filename.
4. Run the notebook cells in order.

Colab provides the notebook environment, so you do not need to install or start Jupyter on your computer. If a required package is missing or incompatible, upload `requirements.txt` to the runtime's working folder and run `%pip install -r requirements.txt` in a new code cell before the analysis. Restart the runtime if prompted after package changes, then rerun the notebook from the start. The requirements are not a fully verified environment lock.

Uploaded CSVs belong to the temporary runtime. You may need to upload them again when starting a new session.

You can also read the saved notebook results on GitHub without downloading the data or running the models.

## Limits and next steps

This is a portfolio analysis of a historical dataset. It does not show that any individual feature causes churn, or that outreach would prevent it. Models and the final threshold were compared using test-set results; a future evaluation should reserve a fresh holdout dataset after those choices are fixed. Prediction inputs should also be checked for availability before the cancellation date.

The repository preserves the supplied analysis and saved results. A data-source section was added to the notebook during portfolio preparation. Full execution was not repeated while preparing this repository because the original CSV was not supplied. Package versions are starting requirements rather than a fully verified environment lock.
