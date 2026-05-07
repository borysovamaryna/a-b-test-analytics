
#  A/B Test Analytics

##  Description

This project consists of 3 main parts:

1. A SQL query for analyzing user behavior within A/B testing experiments. The analysis is based on user sessions and includes product interactions, conversions, and events across countries, continents, devices, and traffic channels.  
2. Further analysis of the experiment in Python.  
3. Visualization of the results in a Tableau dashboard.


#  Part 1 — SQL Data Preparation

##  What was implemented

The SQL query includes:

- joining session, event, and order data  
- inclusion of A/B test identifiers (`test`, `test_group`)  
- calculation of key metrics:
  - number of sessions  
  - number of sessions with orders  
  - number of events  
  - number of new accounts  


##  Query structure

### `general_info`

Basic session-level information:

- date  
- country  
- device  
- traffic channel  
- A/B test  


### `session_with_orders`

Number of sessions that resulted in an order


### `events`

Aggregation of user events (`event_name`)


### `sessions`

Total number of sessions


### `new_account`

Number of newly registered users


##  Final dataset

The final query produces a unified table with the following metrics:

- session  
- session with orders  
- events  
- new account  

Data format:

- date  
- country  
- device  
- channel  
- A/B test  
- metric name (`event_name`)  
- value  


##  Technologies

- SQL (BigQuery / standard SQL)


#  Part 2 — Metric Calculation in Python

##  Metric aggregation

Data was aggregated using pivot tables. For each test and group (A/B), the following were calculated:

- number of sessions (`session`)  
- event counts:
  - add_payment_info  
  - add_shipping_info  
  - begin_checkout  
  - new_accounts  


##  Conversion rates

Conversion rates were calculated for each metric:

- add_payment_info / session  
- add_shipping_info / session  
- begin_checkout / session  
- new_accounts / session  


##  A/B group comparison

For each test and metric:

- conversion rate for group A  
- conversion rate for group B  
- uplift (%) — relative change between groups  


##  Statistical testing

A Z-test for proportions was used to evaluate statistical significance between groups.

The following were calculated:

- Z-score — deviation between groups  
- p-value — probability of observing the difference by chance  
- significant_95 — boolean indicator (p-value < 0.05)  


##  Technologies

- Python (Jupyter Notebook / Google Colaboratory)  


# Part 3 — Data Visualization

##  Dashboards

Two separate dashboards were created:
- one based on SQL output  
- one based on Python analysis  


### SQL-based dashboard allows:

- analysis of results across tests  
- evaluation of differences between groups  
- identification of outliers across countries, continents, devices, and channels  
- extraction of metric values for hypothesis validation  


### Python-based dashboard allows:

- comparison of A and B groups  
- uplift analysis per metric  
- identification of statistically significant changes  
- breakdown of results by test  


##  Interactive dashboard

```text
https://public.tableau.com/app/profile/maryna.borysova/viz/ABtest_17756611762510/ABtest
```

## Final Result

An end-to-end A/B testing analytics pipeline was built:

1. SQL — data extraction and aggregation
2. Python — metric calculation and statistical testing
3. Tableau — visualization and interpretation of results
