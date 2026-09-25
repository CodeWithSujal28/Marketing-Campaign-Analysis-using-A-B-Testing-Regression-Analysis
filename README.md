# Marketing Campaign Analysis using A/B Testing & Regression Analysis

## 📌 Project Overview

This project analyzes and compares the performance of two digital advertising campaigns:

* **Facebook Ads**
* **AdWords Ads**

The analysis is performed using daily campaign data from **January 1, 2019 to December 31, 2019**.

The main purpose of the project is to help a marketing agency understand which advertising platform generates better campaign results, particularly in terms of **clicks and conversions**, and to identify useful patterns in campaign performance over time.

The project combines **Exploratory Data Analysis (EDA), campaign comparison, correlation analysis, A/B-style hypothesis testing, Linear Regression, weekly and monthly analysis, cost-per-conversion analysis, and a cointegration test**.

---

## 🎯 Business Problem

A marketing agency is running advertising campaigns on both Facebook and AdWords.

The agency wants to understand:

* Which platform generates more conversions?
* How do clicks relate to conversions?
* Are the differences between Facebook and AdWords statistically significant?
* How many conversions can be expected from a certain number of Facebook clicks?
* How does Facebook campaign performance change across weekdays and months?
* How does the cost required to generate conversions change over time?
* Is there a long-term relationship between Facebook advertising cost and conversions?

The analysis is intended to convert these questions into measurable insights that can be understood by both technical and non-technical stakeholders.

---

## ❓ Research Question

> **Which advertising platform is more effective in terms of conversions, clicks, and overall campaign performance?**

The project mainly compares **Facebook Ads and AdWords Ads** using the available campaign metrics.

---

## 📊 Dataset

The dataset contains daily advertising campaign information for the complete year **2019**.

### Dataset size

* **Rows:** 365
* **Columns:** 17
* **Time period:** January 1, 2019 – December 31, 2019
* **Frequency:** Daily

Each row represents one day's performance for both Facebook and AdWords campaigns.

### Main information available

For Facebook:

* Facebook Ad Views
* Facebook Ad Clicks
* Facebook Ad Conversions
* Cost per Facebook Ad
* Facebook Click-Through Rate
* Facebook Conversion Rate
* Facebook Cost per Click

For AdWords:

* AdWords Ad Views
* AdWords Ad Clicks
* AdWords Ad Conversions
* Cost per AdWords Ad
* AdWords Click-Through Rate
* AdWords Conversion Rate
* AdWords Cost per Click

The dataset also contains the campaign date.

---

## 🛠️ Technologies & Libraries

### Programming Language

* Python

### Libraries

* **Pandas** — data loading, manipulation and analysis
* **NumPy** — numerical operations
* **Matplotlib** — data visualization
* **Seaborn** — statistical visualizations
* **SciPy** — statistical testing
* **Scikit-learn** — Linear Regression and model evaluation
* **Statsmodels** — cointegration/time-series analysis

---

# 🔎 Project Workflow

The project follows this general workflow:

**Business Problem**

↓

**Research Question**

↓

**Data Understanding**

↓

**Data Preparation**

↓

**Exploratory Data Analysis**

↓

**Campaign Performance Comparison**

↓

**Correlation Analysis**

↓

**A/B Testing using Hypothesis Testing**

↓

**Regression Analysis**

↓

**Weekly & Monthly Analysis**

↓

**Cost Per Conversion Analysis**

↓

**Cointegration Analysis**

↓

**Business Findings**

---

# 1. Data Loading & Initial Understanding

The dataset is loaded using Pandas.

```python
df = pd.read_csv('marketing_campaign.csv')
```

The first few records are inspected to understand the structure of the dataset.

The following checks are performed:

* First few rows
* Number of rows and columns
* Column data types
* Descriptive statistics

The `Date` column is converted into a proper datetime format so that time-based analysis can be performed later.

```python
df['Date'] = pd.to_datetime(df['Date'], format='mixed')
```

---

# 2. Exploratory Data Analysis (EDA)

EDA is performed before the statistical analysis to understand the behavior of the campaign data.

The analysis looks at the distributions of:

* Facebook clicks
* Facebook conversions
* AdWords clicks
* AdWords conversions

Histograms are used to understand how frequently different levels of clicks and conversions occur.

Boxplots are also used to inspect the spread of numerical variables and identify unusually high or low observations.

The purpose of this stage is to understand the data before drawing conclusions from statistical tests or regression models.

---

# 3. Conversion Category Analysis

To make the daily conversion patterns easier to compare, conversions are divided into categories:

* Less than 6
* 6–10
* 10–15
* More than 15

These categories are created separately for Facebook and AdWords.

The number of days falling into each conversion category is then compared between the two platforms.

This helps answer:

> **How frequently do we observe days with high numbers of conversions compared with days having lower numbers of conversions?**

The analysis shows that Facebook has more days with higher conversion counts, while AdWords is concentrated more heavily in the lower conversion ranges.

---

# 4. Clicks vs Conversions

The next question is:

> **Do more clicks on an advertisement lead to more conversions?**

Scatter plots are created for both platforms:

* Facebook Clicks vs Facebook Conversions
* AdWords Clicks vs AdWords Conversions

Correlation coefficients are then calculated.

### Facebook

The analysis produces a strong positive relationship between clicks and conversions, with a correlation of approximately **0.87**.

### AdWords

The analysis produces a moderate positive relationship, with a correlation of approximately **0.45**.

This indicates that higher click counts tend to be associated with higher conversion counts in both campaigns, although the relationship is stronger for Facebook in this dataset.

Correlation should not be interpreted as proof that clicks alone cause conversions.

---

# 5. A/B Testing using Hypothesis Testing

The project compares the two advertising platforms using a statistical hypothesis test.

Here:

* **A = Facebook Ads**
* **B = AdWords Ads**

The business question is:

> **Is Facebook generating significantly more conversions than AdWords?**

### Null Hypothesis (H₀)

There is no difference in conversion performance between Facebook and AdWords, or Facebook does not have higher conversions.

The hypothesis is represented as:

**H₀: μFacebook ≤ μAdWords**

### Alternative Hypothesis (H₁)

Facebook generates more conversions than AdWords.

**H₁: μFacebook > μAdWords**

The analysis compares the mean conversions of the two platforms and performs an independent-samples statistical test.

### Results

The notebook reports:

* **Average Facebook conversions:** 11.74
* **Average AdWords conversions:** 5.98
* **T-statistic:** approximately 32.88
* **P-value:** approximately 9.35 × 10⁻¹³⁴

Using a significance level of **0.05**, the p-value is far below the significance level.

Therefore, the notebook rejects the null hypothesis and finds strong statistical evidence that Facebook's average conversion count is higher than AdWords' average conversion count in this dataset.

### Important interpretation

This result applies to the campaign data analyzed in this project. It does not by itself prove that Facebook will always outperform AdWords in every marketing situation.

---

# 6. Regression Analysis

Regression analysis is used to investigate the relationship between **Facebook Ad Clicks** and **Facebook Ad Conversions**.

### Business Question

> **If we know the number of Facebook ad clicks, how many conversions can we expect?**

### Independent Variable

**Facebook Ad Clicks**

### Dependent Variable

**Facebook Ad Conversions**

A Linear Regression model is created using Scikit-learn.

The original analysis evaluates the model using:

* R² Score
* Mean Squared Error

The original notebook reports an R² score of approximately **76.35%** when the model is fitted and evaluated on the same dataset.

### Prediction Examples

The model is also used to estimate expected conversions for specific numbers of clicks, including:

* 50 clicks
* 80 clicks

These predictions demonstrate how regression can be used to translate advertising activity into an estimated number of conversions.

### Model interpretation

An R² score of approximately 76.35% in the original notebook indicates that the fitted linear relationship explains a substantial portion of the variation in Facebook conversions within this dataset.

However, because the original notebook fits and evaluates the model on the same observations, this R² value should **not be treated as an unbiased test-set performance measure**.

For a stronger portfolio version, the regression should be trained on a training set and evaluated on an unseen test set.

---

# 7. Facebook Campaign Analysis Over Time

The project then focuses specifically on the Facebook campaign.

The relevant Facebook metrics are converted into numerical values where necessary, including:

* Click-through rate
* Conversion rate
* Cost per click
* Advertising cost

The analysis then extracts:

* Month
* Day of week

from the date.

This allows the campaign to be studied across different periods of the year.

---

# 8. Weekly Conversion Analysis

The project calculates total Facebook conversions by day of the week.

This helps answer:

> **On which days of the week do we observe higher conversion activity?**

The analysis suggests that conversions remain relatively consistent across weekdays, with Monday and Tuesday showing relatively higher conversion totals in the notebook's interpretation.

This can help a marketing team identify periods that may deserve additional attention when planning campaign activity.

---

# 9. Monthly Conversion Analysis

Monthly Facebook conversions are calculated and visualized across the 12 months of 2019.

This helps identify:

* Increasing or decreasing trends
* High-conversion months
* Lower-conversion months
* Possible seasonal patterns

The notebook observes an overall upward movement over the year but also identifies several months with lower conversion totals compared with surrounding months.

These changes may be associated with factors such as:

* Seasonal behavior
* Changes in consumer activity
* Campaign strategy changes
* Other external factors

The dataset alone cannot establish the exact reason for these changes.

---

# 10. Cost Per Conversion Analysis

The project also examines how advertising cost changes relative to the number of conversions.

Monthly cost per conversion is calculated as:

**Total Facebook Advertising Cost / Total Facebook Conversions**

This metric helps answer:

> **How much advertising cost is associated with generating one conversion?**

The analysis finds variation in monthly cost per conversion.

The notebook identifies **May and November** as relatively lower-cost months and **February** as a relatively higher-cost month.

Lower cost per conversion can indicate more efficient campaign performance during those periods, although cost alone should not be used as the only measure of campaign success.

---

# 11. Cointegration Analysis

The final statistical analysis investigates whether Facebook advertising cost and Facebook conversions have a long-term equilibrium relationship.

The question is:

> **Is there a long-term relationship between advertising spend and conversions over time?**

A **cointegration test** is performed using:

* Facebook advertising cost
* Facebook conversions

The notebook compares the resulting p-value with the **0.05 significance level**.

The notebook reports a statistically significant result and rejects the null hypothesis, indicating evidence of a long-term relationship between the two time series in this dataset.

This analysis provides an additional time-series perspective beyond simple correlation.

However, cointegration does not by itself establish that increasing advertising cost causes conversions to increase.

---

# 📈 Main Findings

Based on the analysis performed in the notebook:

### Campaign comparison

Facebook produces a higher average number of conversions than AdWords in the analyzed dataset.

* Facebook average conversions: **11.74**
* AdWords average conversions: **5.98**

### Clicks and conversions

Facebook shows a strong positive correlation between clicks and conversions:

**Correlation ≈ 0.87**

AdWords shows a moderate positive correlation:

**Correlation ≈ 0.45**

### Hypothesis testing

The statistical test produces an extremely small p-value:

**p-value ≈ 9.35 × 10⁻¹³⁴**

At a 5% significance level, the null hypothesis is rejected.

### Regression

The original Facebook regression model reports:

**R² ≈ 76.35%**

This indicates a strong fitted relationship between Facebook clicks and conversions in the sample, but the original notebook evaluates the model on the same data used for training.

### Time analysis

Facebook conversions vary across weekdays and months, with some periods showing higher or lower conversion totals.

### Cost per conversion

Monthly cost per conversion fluctuates throughout the year, with May and November identified in the notebook as relatively lower-cost periods and February as a relatively higher-cost period.

### Long-term relationship

The cointegration analysis reports evidence of a long-term relationship between Facebook advertising cost and conversions.

---

# 💼 Business Interpretation

The analysis provides evidence that Facebook performed strongly in terms of conversion volume within the 2019 campaign data.

The statistical test also provides strong evidence that the difference in average conversions between the two platforms is not simply a small random difference within this sample.

The strong relationship between Facebook clicks and conversions also indicates that click activity is useful for understanding Facebook conversion performance.

However, campaign decisions should not be based on conversions alone. A marketing team should also consider:

* Advertising cost
* Cost per conversion
* Click-through rate
* Conversion rate
* Campaign objectives
* Target audience
* Seasonal behavior
* Long-term performance

Therefore, the results can be used as evidence for campaign planning rather than as a universal rule that one platform will always outperform another.

---

# 📂 Project Structure

```text
Marketing-Campaign-Analysis-AB-Testing-Regression-Analysis/
│
├── marketing_campaign.csv
│
├── AB_Testing_Marketing_Campaigns.ipynb
│
└── README.md
```

---

# 🧰 Skills Demonstrated

This project demonstrates practical skills in:

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Data cleaning
* Data type conversion
* Exploratory Data Analysis
* Descriptive statistics
* Data visualization
* Marketing KPI analysis
* Campaign comparison
* Correlation analysis
* A/B testing concepts
* Hypothesis testing
* Statistical significance
* P-values
* Linear Regression
* R²
* Mean Squared Error
* Prediction
* Time-based analysis
* Weekly analysis
* Monthly analysis
* Cost per conversion analysis
* Cointegration testing
* Business interpretation

---

# 🚀 Conclusion

This project analyzes a full year of Facebook and AdWords campaign data to understand advertising performance from both a **business and statistical perspective**.

The workflow starts with basic data understanding and EDA, then moves into campaign comparison, correlation analysis, hypothesis testing, regression analysis, weekly and monthly trends, cost-per-conversion analysis, and cointegration testing.

The analysis provides evidence that Facebook generated higher average conversions than AdWords in the available 2019 campaign data, while also showing a stronger relationship between clicks and conversions.

Rather than relying only on descriptive numbers, the project uses statistical methods to determine whether the observed differences are meaningful and uses regression to estimate expected conversions from Facebook click activity.

Overall, the project demonstrates how **Python and statistical analysis can be used to convert advertising campaign data into practical business insights.**

---

## 👤 Author

**Sujal Mondal**

Data Analyst | Python | SQL | Power BI | Excel

GitHub: [CodeWithSujal28](https://github.com/CodeWithSujal28)

LinkedIn: [Sujal Mondal](https://www.linkedin.com/in/sujal-mondal/)
