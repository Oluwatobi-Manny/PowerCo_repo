# Use Case: Exploratory Data Analysis (EDA) for PowerCo's Customer Churn Rate
---

**Overview**:
This project focuses on conducting an Exploratory Data Analysis (EDA) for PowerCo, an electric company aiming to analyze and reduce its customer churn rate. The insights gained from this EDA will help PowerCo understand the factors contributing to customer churn and develop strategies to improve customer retention.

**Objective:** 
To analyze QVI Chips sales data using Python to identify key performance indicators, understand customer behavior, and inform marketing and product strategies.

**Dataset:**
The dataset contains anonymized customer data, including demographic information, account details, and service usage metrics. Key features in the dataset include:

    - CustomerID: Unique identifier for each customer
    - Tenure: Number of months the customer has been with PowerCo
    - ContractType: Type of contract (month-to-month, one year, two years)
    - MonthlyCharges: Amount charged to the customer per month
    - TotalCharges: Total amount charged to the customer
    - Churn: Indicates whether the customer has churned (Yes/No)

**Steps:**
The EDA involves the following steps:
- **Data Loading**

        ```
        # Import necessary libraries
        import pandas as pd

        # Load dataset
        client_df = pd.read_csv(client_url, engine='python')
        price_df = pd.read_csv(price_url, engine='python')
        ```
![client_df](<Images/Screenshot (204).png>)
![price_df](<Images/Screenshot (203).png>)


- **Summary statistics:** Calculate summary statistics for numerical variables.
- **Data visualization:** Create visualizations to explore data distributions and relationships.
        - **Plotting the categorical columns of client_df by churn rates**
![Has gas by churn](Images/has_gas_by_churn.jpg)  
        - **Plotting the distribution of numerical columns of client_df**
![net margin on power subscription](<Images/Screenshot (206).png>)
        - **Plotting stacked bars of columns by churn rates**
![Churn rate by has gas](<Images/Screenshot (208).png>)
        - **Plotting box plots of columns by churn rates**
![Gas consumption 12 months](<Images/Screenshot (210).png>)


**Expected Outcomes:**
By the end of this analysis, we expect to:
- Understand the main factors driving customer churn at PowerCo.
- Provide actionable insights for reducing churn rates.
- Offer recommendations for future data collection and analysis.
