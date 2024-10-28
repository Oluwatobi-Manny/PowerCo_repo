# Use Case: Exploratory Data Analysis (EDA) for PowerCo's Customer Churn Rate
---

**Overview**:
This project focuses on conducting an Exploratory Data Analysis (EDA) for PowerCo, an electric company aiming to analyze and reduce its customer churn rate. The insights gained from this EDA will help PowerCo understand the factors contributing to customer churn and develop strategies to improve customer retention.

**Objective:** 
To analyze QVI Chips sales data using Python to identify key performance indicators, understand customer behavior, and inform marketing and product strategies.

**Dataset:**
The datasets contains anonymized customer data, including demographic information, account details, and service usage metrics. The features in the datasets include:

**client_df**

id = client company identifier

activity_new = category of the company’s activity 

channel_sales = code of the sales

channelcons_12m = electricity consumption of the past 12 months

cons_gas_12m = gas consumption of the past 12 months

cons_last_month = electricity consumption of the last month

date_activ = date of activation of the contract

date_end = registered date of the end of the contract

date_modif_prod = date of the last modification of the product

date_renewal = date of the next contract renewal

forecast_cons_12m = forecasted electricity consumption for next 12 months

forecast_cons_year = forecasted electricity consumption for the next calendar year

forecast_discount_energy = forecasted value of current discount

forecast_meter_rent_12m = forecasted bill of meter rental for the next 2 months

forecast_price_energy_off_peak = forecasted energy price for 1st period (off peak)

forecast_price_energy_peak = forecasted energy price for 2nd period (peak)

forecast_price_pow_off_peak = forecasted power price for 1st period (off peak)

has_gas = indicated if client is also a gas client imp_cons = current paid consumption

margin_gross_pow_ele = gross margin on power subscription

margin_net_pow_ele = net margin on power subscription

nb_prod_act = number of active products and services

net_margin = total net marginnum_years_antig = antiquity of the client (in number of years)

origin_up = code of the electricity campaign the customer first subscribed.

pow_max = subscribed power *churn = has the client churned over the next 3 months


**price_df**

id = client company identifier

price_date = reference date

price_off_peak_var = price of energy for the 1st period (off peak)

price_peak_var = price of energy for the 2nd period (peak)

price_mid_peak_var = price of energy for the 3rd period (mid peak)

price_off_peak_fix = price of power for the 1st period (off peak)

price_peak_fix = price of power for the 2nd period (peak)

price_mid_peak_fix = price of power for the 3rd period (mid peak)

**Steps:**
The EDA involves the following steps:
- **Data Loading**

        ```
        # Import libraries
        import pandas as pd

        # Load dataset
        client_df = pd.read_csv(client_url, engine='python')
        price_df = pd.read_csv(price_url, engine='python')
        ```

![client_df](<PowerCo EDA/Images/Screenshot (204).png>)

![price_df](<PowerCo EDA/Images/Screenshot (203).png>)


- **Summary statistics:** Calculate summary statistics for numerical variables.
- **Data visualization:** Create visualizations to explore data distributions and relationships.
- **Plotting the categorical columns of client_df by churn rates**

![Has gas by churn](<PowerCo EDA/Images/has_gas_by_churn.jpg>)  

- **Plotting the distribution of numerical columns of client_df**

![net margin on power subscription](<PowerCo EDA/Images/Screenshot (206).png>)

- **Plotting stacked bars of columns by churn rates**

![Churn rate by has gas](<PowerCo EDA/Images/Screenshot (208).png>)

- **Plotting box plots of columns by churn rates**

![Gas consumption 12 months](<PowerCo EDA/Images/Screenshot (210).png>)


**Expected Outcomes:**
By the end of this analysis, we expect to:
- Understand the main factors driving customer churn at PowerCo.
- Provide actionable insights for reducing churn rates.
- Offer recommendations for future data collection and analysis.
---
---

# Use Case: Feature Engineering for PowerCo's Customer Churn Analysis
---

## Overview
---
This project focuses on conducting feature engineering for PowerCo, an electric company aiming to improve its analysis of customer churn rates. The insights gained from this process will help PowerCo create more accurate predictive models, ultimately aiding in customer retention strategies.

## Objective
---
The primary objective of this feature engineering is to create new variables that better capture the underlying patterns in the data related to customer churn. These engineered features will enhance the performance of predictive models.

**Method:**
Creating New Features such as difference between off-peak prices in December and preceding January, average price changes across periods and so on
```
  # Group off-peak prices by companies and month
  monthly_price_by_id = price_df.groupby(['id', 'price_date']).agg({'price_off_peak_var': 'mean', 'price_off_peak_fix': 'mean'}).reset_index()

  # Get january and december prices
  jan_prices = monthly_price_by_id.groupby('id').first().reset_index()
  dec_prices = monthly_price_by_id.groupby('id').last().reset_index()

  # Calculate the difference
  diff = pd.merge(dec_prices.rename(columns={'price_off_peak_var': 'dec_1', 'price_off_peak_fix': 'dec_2'}), jan_prices.drop(columns='price_date'), on='id')
  diff['offpeak_diff_dec_january_energy'] = diff['dec_1'] - diff['price_off_peak_var']
  diff['offpeak_diff_dec_january_power'] = diff['dec_2'] - diff['price_off_peak_fix']
  diff = diff[['id', 'offpeak_diff_dec_january_energy','offpeak_diff_dec_january_power']]
  diff.head()
```

![Feature engineering](<PowerCo FE/Images/Screenshot (212).png>)

---
---

# Use Case: Model Building for PowerCo's Customer Churn Prediction
---
**Overview:**
This project focuses on building predictive models for PowerCo, an electric company aiming to forecast customer churn rates. The insights gained from these models will help PowerCo implement targeted retention strategies to reduce churn.

**Objective:**
The primary objective of this model building process is to develop and evaluate machine learning models that accurately predict customer churn. These models will help PowerCo identify at-risk customers and take proactive measures to retain them.

**Model Building:**

A function is ran to pick the most model suitable in terms of the following metrics: F1 Score, Precision, Recall, Accuracy.Random Forest Model was picked for the prediction model.

![Model choosing](<PowerCo PM/Image/Screenshot (214).png>)

For Train-test split, size of test is 20% percent of data with shuffled ones. VIF and Recursive Elimination methods were used to remove columns with high linearity to avoid multicollinearity.

The top 5 most important features were also selected.

![Important features](<PowerCo PM/Image/Screenshot (216).png>)