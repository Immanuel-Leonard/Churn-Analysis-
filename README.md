# Telco Customer Churn Analysis

An exploratory analysis of telecommunications customer churn using Python, pandas, and data visualization. This project examines customer demographics, tenure, geography, reported reasons for leaving, and revenue to identify patterns that could inform retention strategies.

**Business question:** Which customer segments show higher observed churn, and what areas should a retention team investigate first?

## Project overview

The analysis explores:

- Observed churn rates across age groups.
- Average churn scores across customer tenure and selected cities.
- The most frequently reported reasons for leaving.
- Customer distribution by age, ZIP code, and city.
- Total revenue by age group and city.

This is a descriptive analysis, not a predictive machine-learning model. The notebook uses the dataset's existing `Churn Score`; it does not generate its own risk predictions.

## Dataset

The notebook loads the Hugging Face dataset `aai510-group1/telco-customer-churn` using the `datasets` library.

The current analysis uses the dataset's **test split**, containing **1,409 customer records and 52 columns**, as shown in the notebook's saved outputs.

Fields used include:

- `Churn`: the binary outcome used to calculate observed churn rates.
- `Churn Score`: an existing score supplied with the dataset.
- `Churn Reason`: the reported reason for leaving.
- `Age` and `Tenure in Months`: customer characteristics.
- `City` and `Zip Code`: geographic attributes.
- `Total Revenue`: the dataset's recorded revenue measure.

**Important distinction:** average churn score is not the same as observed churn rate. A score of 59.05 should not be interpreted as 59.05% of customers leaving or as a calibrated probability.

## Tools

- **Python** for the analysis workflow.
- **pandas** for filtering, grouping, and aggregation.
- **Matplotlib and seaborn** for visualizations.
- **Hugging Face datasets** for data access.
- **Google Colab** for notebook execution.

## Analysis workflow

1. Load the dataset and inspect its structure.
2. Summarize customer demographics and geographic distribution.
3. Group customers into age bands and calculate observed churn rates.
4. Examine average churn scores by tenure and city.
5. Count reported churn reasons.
6. Compare revenue across age groups and cities.
7. Visualize the results and identify questions for further investigation.

## Findings from the saved notebook outputs

### Observed churn varies across age groups

Customers aged **70-79** had an observed churn rate of **43.38%**, compared with **22.71%** among customers aged **18-29** in the analyzed split.

The 70-79 group contained 136 customers, while the 18-29 group contained 295. These are descriptive differences, not evidence that age causes churn.

The **80+** group contained only **14 customers**, so its estimated churn rate should be treated cautiously.

### Competitor offers and support experiences deserve investigation

Two reported reasons were tied at **55 customers each**:

- Competitor had better devices.
- Competitor made better offer.

“Attitude of support person” appeared **43 times**.

These responses suggest investigating competitive offers and customer-support experiences. They do not establish which intervention would successfully retain customers.

### Geographic churn scores vary

Among cities with more than 10 customers in the analyzed split:

- **San Diego** had an average churn score of **68.68**.
- **Los Angeles** had an average churn score of **54.90**.

These are averages of the supplied score, not actual city-level churn rates. Customer counts and observed churn rates should be considered before prioritizing locations.

## Business implications

The results suggest several retention hypotheses worth testing:

- **Competitive positioning:** investigate whether device options and competing offers influence customers' decisions to leave.
- **Support quality:** review customer-support feedback and identify recurring service issues.
- **Segment-specific outreach:** investigate higher-churn groups while accounting for tenure, contract type, pricing, and sample size.

These are proposed areas for investigation, not proven recommendations with measured financial impact.

## Repository contents

- `Churn_Analysis.ipynb`: analysis code, visualizations, and saved outputs.
- `README.md`: project overview, findings, and limitations.

## Running the notebook

Open `Churn_Analysis.ipynb` in Google Colab or a Jupyter environment.

Install the required packages before running the analysis:

```python
%pip install datasets numpy pandas matplotlib seaborn
```

Run the notebook from top to bottom. An internet connection is required to download the dataset.

The notebook loads the data with:

```python
from datasets import load_dataset

dataset = load_dataset("aai510-group1/telco-customer-churn")
customers = dataset["test"].to_pandas()
```

Do not hardcode authentication tokens in the notebook. If authentication is needed, supply the token through a secure runtime configuration such as Colab Secrets.

## Limitations

- **Subset analysis:** findings describe the test split, not the full dataset or a live customer population.
- **Test-set reuse:** because this split has already been explored, a later predictive project should use an appropriate untouched holdout for final evaluation.
- **Association, not causation:** differences between groups do not establish why customers leave.
- **Small groups:** some age and geographic segments contain too few customers for stable comparisons.
- **Score interpretation:** the supplied churn score has not been independently validated or calibrated in this project.
- **Revenue interpretation:** recorded total revenue is not automatically revenue at risk, profit, or recoverable revenue.
- **Missing-value handling:** the churn-reason analysis filters the literal string `"None"`; a stronger cleaning step should explicitly handle actual nulls and other missing-value representations.
- **No predictive model:** model performance, feature importance, and deployment are outside the current scope.

## Planned improvements

- Calculate overall observed churn and compare it across contract types, tenure bands, payment methods, and service options.
- Include segment sizes and confidence intervals alongside churn-rate comparisons.
- Replace average churn scores with observed churn rates where the question concerns actual customer departures.
- Add data-quality checks for missing values, duplicate records, and unexpected category values.
- Export selected charts so the main findings are visible directly in the README.
- Add SQL queries for reusable customer-segmentation and churn summaries.
- Develop a baseline predictive model with leakage checks and an untouched evaluation set.

## Skills demonstrated

Python, pandas, exploratory data analysis, customer segmentation, aggregation, data visualization, and business interpretation.
