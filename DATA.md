# Data instructions

## Source

- **Dataset:** Telecom Customer Churn.
- **Downloaded from:** [Maven Analytics Data Playground](https://mavenanalytics.io/data-playground/telecom-customer-churn).
- **Original source credited by Maven Analytics:** IBM Cognos Analytics.
- **Context:** A fictional telecom company serving customers in California during Q2 2022.

## Input used in this project

The notebook loads `telecom_customer_churn.csv` from its working folder. In Google Colab, upload it to the runtime Files panel, normally under `/content`. The CSV is not included in this package.

The original input used in the notebook has 7,043 customer records and 38 columns. It includes customer details, contracts, service use, charges, customer status, and reported churn reasons.

## How to obtain and use the data

1. Open the Maven Analytics dataset link above and download the Telecom Customer Churn dataset. Maven may require you to sign in.
2. Unzip the download and locate `telecom_customer_churn.csv`.
3. Open `telecom_customer_churn_prediction.ipynb` in Google Colab and upload the CSV through the Files panel to the working folder, normally `/content`, before running the notebook.

Use the customer-churn CSV used for this project, rather than another telecom churn dataset with a similar name. The additional ZIP-code population table provided with the Maven dataset is not loaded by this notebook.
