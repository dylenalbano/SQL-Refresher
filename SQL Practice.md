# SQL Notebook Sample:


```python
import pandas as pd
import sys
!{sys.executable} -m pip install pandasql -q
from pandasql import sqldf

customers = pd.read_csv('customers.csv')
transactions = pd.read_csv('transactions.csv')
marketing_campaigns = pd.read_csv('marketing_campaigns.csv')
customer_events = pd.read_csv('customer_events.csv')
monthly_cohort_metrics = pd.read_csv('monthly_cohort_metrics.csv')
daily_acquisition_stats = pd.read_csv('daily_acquisition_stats.csv')
```

## Select all columns


```python
sqldf("""
    SELECT *
    FROM customers
    LIMIT 100;
""")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>signup_date</th>
      <th>cohort_month</th>
      <th>acquisition_channel</th>
      <th>acquisition_campaign</th>
      <th>acquisition_cost</th>
      <th>country</th>
      <th>age</th>
      <th>gender</th>
      <th>plan_type</th>
      <th>is_active</th>
      <th>churn_date</th>
      <th>lifetime_days</th>
      <th>predicted_ltv</th>
      <th>risk_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2023-10-17</td>
      <td>2023-10</td>
      <td>paid_search</td>
      <td>spring_promo</td>
      <td>63.20</td>
      <td>UK</td>
      <td>32</td>
      <td>M</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>289</td>
      <td>69.08</td>
      <td>0.59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2022-02-02</td>
      <td>2022-02</td>
      <td>organic_search</td>
      <td>summer_sale</td>
      <td>1.09</td>
      <td>FR</td>
      <td>56</td>
      <td>M</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>911</td>
      <td>69.04</td>
      <td>0.23</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2023-08-27</td>
      <td>2023-08</td>
      <td>email</td>
      <td>spring_promo</td>
      <td>11.86</td>
      <td>US</td>
      <td>62</td>
      <td>M</td>
      <td>free</td>
      <td>0</td>
      <td>2024-08-12</td>
      <td>351</td>
      <td>29.20</td>
      <td>0.38</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2023-01-03</td>
      <td>2023-01</td>
      <td>direct</td>
      <td>product_hunt</td>
      <td>0.79</td>
      <td>US</td>
      <td>64</td>
      <td>M</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>576</td>
      <td>27.09</td>
      <td>0.30</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2023-10-06</td>
      <td>2023-10</td>
      <td>direct</td>
      <td>product_hunt</td>
      <td>0.58</td>
      <td>US</td>
      <td>20</td>
      <td>F</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>300</td>
      <td>1551.66</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>95</th>
      <td>96</td>
      <td>2022-07-25</td>
      <td>2022-07</td>
      <td>social_media</td>
      <td>webinar_series</td>
      <td>53.82</td>
      <td>CA</td>
      <td>51</td>
      <td>F</td>
      <td>free</td>
      <td>0</td>
      <td>2023-12-07</td>
      <td>500</td>
      <td>107.06</td>
      <td>0.30</td>
    </tr>
    <tr>
      <th>96</th>
      <td>97</td>
      <td>2024-06-10</td>
      <td>2024-06</td>
      <td>direct</td>
      <td>summer_sale</td>
      <td>1.40</td>
      <td>US</td>
      <td>27</td>
      <td>F</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>52</td>
      <td>80.70</td>
      <td>0.40</td>
    </tr>
    <tr>
      <th>97</th>
      <td>98</td>
      <td>2024-05-16</td>
      <td>2024-05</td>
      <td>direct</td>
      <td>summer_sale</td>
      <td>2.37</td>
      <td>US</td>
      <td>34</td>
      <td>F</td>
      <td>basic</td>
      <td>1</td>
      <td>None</td>
      <td>77</td>
      <td>483.06</td>
      <td>0.58</td>
    </tr>
    <tr>
      <th>98</th>
      <td>99</td>
      <td>2024-04-22</td>
      <td>2024-04</td>
      <td>direct</td>
      <td>summer_sale</td>
      <td>2.02</td>
      <td>DE</td>
      <td>19</td>
      <td>F</td>
      <td>enterprise</td>
      <td>1</td>
      <td>None</td>
      <td>101</td>
      <td>4494.44</td>
      <td>0.64</td>
    </tr>
    <tr>
      <th>99</th>
      <td>100</td>
      <td>2023-10-13</td>
      <td>2023-10</td>
      <td>content_marketing</td>
      <td>brand_awareness</td>
      <td>21.23</td>
      <td>US</td>
      <td>26</td>
      <td>M</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>293</td>
      <td>30.45</td>
      <td>0.24</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 15 columns</p>
</div>



## Select specific columns


```python
# Retrieve the first 10 rows from the customers table.

sqldf ("""
    SELECT customer_id, signup_date, plan_type
    FROM customers
    LIMIT 10;
""")
    
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>signup_date</th>
      <th>plan_type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2023-10-17</td>
      <td>free</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2022-02-02</td>
      <td>free</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2023-08-27</td>
      <td>free</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2023-01-03</td>
      <td>free</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2023-10-06</td>
      <td>pro</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2023-01-25</td>
      <td>free</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>2024-01-17</td>
      <td>free</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>2022-11-20</td>
      <td>pro</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>2022-09-29</td>
      <td>basic</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>2022-05-22</td>
      <td>pro</td>
    </tr>
  </tbody>
</table>
</div>



## WHERE with one condition


```python
# Find all customers on the enterprise plan.

sqldf ("""
    SELECT customer_id
    FROM customers
    WHERE plan_type = 'enterprise'
    LIMIT 10;
""")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>21</td>
    </tr>
    <tr>
      <th>1</th>
      <td>22</td>
    </tr>
    <tr>
      <th>2</th>
      <td>37</td>
    </tr>
    <tr>
      <th>3</th>
      <td>46</td>
    </tr>
    <tr>
      <th>4</th>
      <td>64</td>
    </tr>
    <tr>
      <th>5</th>
      <td>74</td>
    </tr>
    <tr>
      <th>6</th>
      <td>81</td>
    </tr>
    <tr>
      <th>7</th>
      <td>86</td>
    </tr>
    <tr>
      <th>8</th>
      <td>91</td>
    </tr>
    <tr>
      <th>9</th>
      <td>93</td>
    </tr>
  </tbody>
</table>
</div>



## WHERE with multiple conditions (AND)


```python
# Find customers who signed up after 2023-01-01 AND are on the pro plan.

sqldf ("""
       SELECT customer_id
       FROM customers
       WHERE signup_date > '2023-01-01'
       AND plan_type = 'pro';
""")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>11</td>
    </tr>
    <tr>
      <th>2</th>
      <td>16</td>
    </tr>
    <tr>
      <th>3</th>
      <td>28</td>
    </tr>
    <tr>
      <th>4</th>
      <td>33</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>140</th>
      <td>981</td>
    </tr>
    <tr>
      <th>141</th>
      <td>985</td>
    </tr>
    <tr>
      <th>142</th>
      <td>986</td>
    </tr>
    <tr>
      <th>143</th>
      <td>988</td>
    </tr>
    <tr>
      <th>144</th>
      <td>1000</td>
    </tr>
  </tbody>
</table>
<p>145 rows × 1 columns</p>
</div>



## WHERE with OR


```python
# Find customers from the US or UK.

sqldf ("""
    SELECT *
    FROM customers
    WHERE country = 'US' OR 'UK';
""")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>signup_date</th>
      <th>cohort_month</th>
      <th>acquisition_channel</th>
      <th>acquisition_campaign</th>
      <th>acquisition_cost</th>
      <th>country</th>
      <th>age</th>
      <th>gender</th>
      <th>plan_type</th>
      <th>is_active</th>
      <th>churn_date</th>
      <th>lifetime_days</th>
      <th>predicted_ltv</th>
      <th>risk_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3</td>
      <td>2023-08-27</td>
      <td>2023-08</td>
      <td>email</td>
      <td>spring_promo</td>
      <td>11.86</td>
      <td>US</td>
      <td>62</td>
      <td>M</td>
      <td>free</td>
      <td>0</td>
      <td>2024-08-12</td>
      <td>351</td>
      <td>29.20</td>
      <td>0.38</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>2023-01-03</td>
      <td>2023-01</td>
      <td>direct</td>
      <td>product_hunt</td>
      <td>0.79</td>
      <td>US</td>
      <td>64</td>
      <td>M</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>576</td>
      <td>27.09</td>
      <td>0.30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
      <td>2023-10-06</td>
      <td>2023-10</td>
      <td>direct</td>
      <td>product_hunt</td>
      <td>0.58</td>
      <td>US</td>
      <td>20</td>
      <td>F</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>300</td>
      <td>1551.66</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10</td>
      <td>2022-05-22</td>
      <td>2022-05</td>
      <td>content_marketing</td>
      <td>summer_sale</td>
      <td>23.89</td>
      <td>US</td>
      <td>27</td>
      <td>F</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>802</td>
      <td>411.48</td>
      <td>0.38</td>
    </tr>
    <tr>
      <th>4</th>
      <td>11</td>
      <td>2023-04-25</td>
      <td>2023-04</td>
      <td>email</td>
      <td>webinar_series</td>
      <td>13.19</td>
      <td>US</td>
      <td>61</td>
      <td>F</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>464</td>
      <td>704.23</td>
      <td>0.64</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>235</th>
      <td>978</td>
      <td>2022-01-22</td>
      <td>2022-01</td>
      <td>social_media</td>
      <td>brand_awareness</td>
      <td>54.06</td>
      <td>US</td>
      <td>61</td>
      <td>F</td>
      <td>free</td>
      <td>0</td>
      <td>2023-05-29</td>
      <td>492</td>
      <td>72.48</td>
      <td>0.49</td>
    </tr>
    <tr>
      <th>236</th>
      <td>979</td>
      <td>2022-09-11</td>
      <td>2022-09</td>
      <td>content_marketing</td>
      <td>summer_sale</td>
      <td>6.13</td>
      <td>US</td>
      <td>54</td>
      <td>F</td>
      <td>free</td>
      <td>0</td>
      <td>2024-02-15</td>
      <td>522</td>
      <td>35.06</td>
      <td>0.15</td>
    </tr>
    <tr>
      <th>237</th>
      <td>997</td>
      <td>2022-05-20</td>
      <td>2022-05</td>
      <td>referral</td>
      <td>None</td>
      <td>17.79</td>
      <td>US</td>
      <td>37</td>
      <td>F</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>804</td>
      <td>1480.09</td>
      <td>0.62</td>
    </tr>
    <tr>
      <th>238</th>
      <td>999</td>
      <td>2022-02-26</td>
      <td>2022-02</td>
      <td>paid_search</td>
      <td>brand_awareness</td>
      <td>41.30</td>
      <td>US</td>
      <td>33</td>
      <td>F</td>
      <td>basic</td>
      <td>1</td>
      <td>None</td>
      <td>887</td>
      <td>487.91</td>
      <td>0.85</td>
    </tr>
    <tr>
      <th>239</th>
      <td>1000</td>
      <td>2023-09-24</td>
      <td>2023-09</td>
      <td>paid_search</td>
      <td>influencer_q1</td>
      <td>24.51</td>
      <td>US</td>
      <td>29</td>
      <td>M</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>312</td>
      <td>1056.58</td>
      <td>0.70</td>
    </tr>
  </tbody>
</table>
<p>240 rows × 15 columns</p>
</div>



## IN operator


```python
# Same as above but using IN — find customers from US, UK, or CA.

sqldf ("""
    SELECT *
    FROM customers
    WHERE country IN ('US', 'UK', 'CA');
""")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>signup_date</th>
      <th>cohort_month</th>
      <th>acquisition_channel</th>
      <th>acquisition_campaign</th>
      <th>acquisition_cost</th>
      <th>country</th>
      <th>age</th>
      <th>gender</th>
      <th>plan_type</th>
      <th>is_active</th>
      <th>churn_date</th>
      <th>lifetime_days</th>
      <th>predicted_ltv</th>
      <th>risk_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2023-10-17</td>
      <td>2023-10</td>
      <td>paid_search</td>
      <td>spring_promo</td>
      <td>63.20</td>
      <td>UK</td>
      <td>32</td>
      <td>M</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>289</td>
      <td>69.08</td>
      <td>0.59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>2023-08-27</td>
      <td>2023-08</td>
      <td>email</td>
      <td>spring_promo</td>
      <td>11.86</td>
      <td>US</td>
      <td>62</td>
      <td>M</td>
      <td>free</td>
      <td>0</td>
      <td>2024-08-12</td>
      <td>351</td>
      <td>29.20</td>
      <td>0.38</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4</td>
      <td>2023-01-03</td>
      <td>2023-01</td>
      <td>direct</td>
      <td>product_hunt</td>
      <td>0.79</td>
      <td>US</td>
      <td>64</td>
      <td>M</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>576</td>
      <td>27.09</td>
      <td>0.30</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
      <td>2023-10-06</td>
      <td>2023-10</td>
      <td>direct</td>
      <td>product_hunt</td>
      <td>0.58</td>
      <td>US</td>
      <td>20</td>
      <td>F</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>300</td>
      <td>1551.66</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6</td>
      <td>2023-01-25</td>
      <td>2023-01</td>
      <td>email</td>
      <td>influencer_q2</td>
      <td>10.26</td>
      <td>CA</td>
      <td>28</td>
      <td>M</td>
      <td>free</td>
      <td>0</td>
      <td>2023-04-15</td>
      <td>80</td>
      <td>74.82</td>
      <td>0.18</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>478</th>
      <td>991</td>
      <td>2022-05-19</td>
      <td>2022-05</td>
      <td>affiliate</td>
      <td>webinar_series</td>
      <td>29.98</td>
      <td>UK</td>
      <td>23</td>
      <td>M</td>
      <td>enterprise</td>
      <td>1</td>
      <td>None</td>
      <td>805</td>
      <td>2190.21</td>
      <td>0.78</td>
    </tr>
    <tr>
      <th>479</th>
      <td>995</td>
      <td>2023-06-15</td>
      <td>2023-06</td>
      <td>content_marketing</td>
      <td>spring_promo</td>
      <td>7.12</td>
      <td>UK</td>
      <td>59</td>
      <td>M</td>
      <td>basic</td>
      <td>1</td>
      <td>None</td>
      <td>413</td>
      <td>425.34</td>
      <td>0.69</td>
    </tr>
    <tr>
      <th>480</th>
      <td>997</td>
      <td>2022-05-20</td>
      <td>2022-05</td>
      <td>referral</td>
      <td>None</td>
      <td>17.79</td>
      <td>US</td>
      <td>37</td>
      <td>F</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>804</td>
      <td>1480.09</td>
      <td>0.62</td>
    </tr>
    <tr>
      <th>481</th>
      <td>999</td>
      <td>2022-02-26</td>
      <td>2022-02</td>
      <td>paid_search</td>
      <td>brand_awareness</td>
      <td>41.30</td>
      <td>US</td>
      <td>33</td>
      <td>F</td>
      <td>basic</td>
      <td>1</td>
      <td>None</td>
      <td>887</td>
      <td>487.91</td>
      <td>0.85</td>
    </tr>
    <tr>
      <th>482</th>
      <td>1000</td>
      <td>2023-09-24</td>
      <td>2023-09</td>
      <td>paid_search</td>
      <td>influencer_q1</td>
      <td>24.51</td>
      <td>US</td>
      <td>29</td>
      <td>M</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>312</td>
      <td>1056.58</td>
      <td>0.70</td>
    </tr>
  </tbody>
</table>
<p>483 rows × 15 columns</p>
</div>



## BETWEEN


```python
# Find transactions with amounts between 100 and 500.

sqldf ("""
    SELECT *
    FROM transactions
    WHERE amount BETWEEN 100 AND 500
    LIMIT 20;
""")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>transaction_id</th>
      <th>customer_id</th>
      <th>transaction_date</th>
      <th>amount</th>
      <th>product_category</th>
      <th>payment_method</th>
      <th>is_refund</th>
      <th>discount_pct</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>2024-03-13</td>
      <td>479.36</td>
      <td>one_time_purchase</td>
      <td>wire_transfer</td>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>2</td>
      <td>2023-01-31</td>
      <td>260.56</td>
      <td>training</td>
      <td>credit_card</td>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
      <td>3</td>
      <td>2023-12-12</td>
      <td>214.10</td>
      <td>subscription</td>
      <td>debit_card</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>5</td>
      <td>2024-04-15</td>
      <td>322.63</td>
      <td>training</td>
      <td>ach</td>
      <td>0</td>
      <td>25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8</td>
      <td>5</td>
      <td>2024-02-15</td>
      <td>103.65</td>
      <td>subscription</td>
      <td>ach</td>
      <td>0</td>
      <td>10</td>
    </tr>
    <tr>
      <th>5</th>
      <td>11</td>
      <td>5</td>
      <td>2023-11-28</td>
      <td>430.60</td>
      <td>professional_services</td>
      <td>credit_card</td>
      <td>0</td>
      <td>15</td>
    </tr>
    <tr>
      <th>6</th>
      <td>13</td>
      <td>5</td>
      <td>2024-04-14</td>
      <td>422.53</td>
      <td>one_time_purchase</td>
      <td>credit_card</td>
      <td>0</td>
      <td>10</td>
    </tr>
    <tr>
      <th>7</th>
      <td>14</td>
      <td>5</td>
      <td>2024-05-23</td>
      <td>295.78</td>
      <td>subscription</td>
      <td>debit_card</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>17</td>
      <td>5</td>
      <td>2023-10-23</td>
      <td>179.73</td>
      <td>upgrade</td>
      <td>ach</td>
      <td>0</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>19</td>
      <td>5</td>
      <td>2024-01-11</td>
      <td>118.37</td>
      <td>upgrade</td>
      <td>paypal</td>
      <td>0</td>
      <td>10</td>
    </tr>
    <tr>
      <th>10</th>
      <td>21</td>
      <td>8</td>
      <td>2022-12-13</td>
      <td>281.84</td>
      <td>subscription</td>
      <td>wire_transfer</td>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>11</th>
      <td>22</td>
      <td>8</td>
      <td>2023-11-21</td>
      <td>261.85</td>
      <td>subscription</td>
      <td>ach</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>23</td>
      <td>8</td>
      <td>2024-07-01</td>
      <td>159.63</td>
      <td>subscription</td>
      <td>wire_transfer</td>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>13</th>
      <td>27</td>
      <td>8</td>
      <td>2024-04-08</td>
      <td>283.97</td>
      <td>subscription</td>
      <td>paypal</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>30</td>
      <td>8</td>
      <td>2024-04-22</td>
      <td>111.22</td>
      <td>subscription</td>
      <td>credit_card</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>31</td>
      <td>8</td>
      <td>2023-01-15</td>
      <td>235.94</td>
      <td>subscription</td>
      <td>credit_card</td>
      <td>0</td>
      <td>15</td>
    </tr>
    <tr>
      <th>16</th>
      <td>33</td>
      <td>9</td>
      <td>2023-12-21</td>
      <td>187.92</td>
      <td>subscription</td>
      <td>debit_card</td>
      <td>0</td>
      <td>10</td>
    </tr>
    <tr>
      <th>17</th>
      <td>35</td>
      <td>9</td>
      <td>2023-11-25</td>
      <td>445.40</td>
      <td>one_time_purchase</td>
      <td>credit_card</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>37</td>
      <td>9</td>
      <td>2022-11-12</td>
      <td>184.09</td>
      <td>subscription</td>
      <td>debit_card</td>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>19</th>
      <td>38</td>
      <td>9</td>
      <td>2024-06-10</td>
      <td>200.04</td>
      <td>subscription</td>
      <td>paypal</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



## LIKE (pattern matching)


```python
# Find all campaigns with "04" in the name.

sqldf ("""
    SELECT *
    FROM marketing_campaigns
    WHERE campaign_name LIKE '%04%';
""")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>campaign_id</th>
      <th>campaign_name</th>
      <th>channel</th>
      <th>start_date</th>
      <th>end_date</th>
      <th>budget</th>
      <th>spend</th>
      <th>impressions</th>
      <th>clicks</th>
      <th>conversions</th>
      <th>target_audience</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4</td>
      <td>campaign_004</td>
      <td>organic_search</td>
      <td>2023-11-13</td>
      <td>2024-01-25</td>
      <td>6561.07</td>
      <td>4187.47</td>
      <td>427357</td>
      <td>28548</td>
      <td>2589</td>
      <td>returning</td>
    </tr>
    <tr>
      <th>1</th>
      <td>40</td>
      <td>campaign_040</td>
      <td>email</td>
      <td>2023-04-28</td>
      <td>2023-07-24</td>
      <td>5488.91</td>
      <td>4949.17</td>
      <td>73972</td>
      <td>4103</td>
      <td>587</td>
      <td>enterprise_prospects</td>
    </tr>
    <tr>
      <th>2</th>
      <td>41</td>
      <td>campaign_041</td>
      <td>referral</td>
      <td>2024-02-11</td>
      <td>2024-04-29</td>
      <td>30316.39</td>
      <td>28150.50</td>
      <td>291359</td>
      <td>8299</td>
      <td>1134</td>
      <td>enterprise_prospects</td>
    </tr>
    <tr>
      <th>3</th>
      <td>42</td>
      <td>campaign_042</td>
      <td>paid_search</td>
      <td>2023-05-28</td>
      <td>2023-07-11</td>
      <td>28953.55</td>
      <td>25545.48</td>
      <td>321116</td>
      <td>18042</td>
      <td>2338</td>
      <td>smb</td>
    </tr>
    <tr>
      <th>4</th>
      <td>43</td>
      <td>campaign_043</td>
      <td>direct</td>
      <td>2023-08-28</td>
      <td>2023-10-18</td>
      <td>11919.20</td>
      <td>9019.02</td>
      <td>404405</td>
      <td>21589</td>
      <td>2115</td>
      <td>returning</td>
    </tr>
    <tr>
      <th>5</th>
      <td>44</td>
      <td>campaign_044</td>
      <td>organic_search</td>
      <td>2022-05-17</td>
      <td>2022-08-02</td>
      <td>36059.22</td>
      <td>32219.79</td>
      <td>173659</td>
      <td>1899</td>
      <td>282</td>
      <td>new_users</td>
    </tr>
    <tr>
      <th>6</th>
      <td>45</td>
      <td>campaign_045</td>
      <td>paid_search</td>
      <td>2023-07-16</td>
      <td>2023-08-03</td>
      <td>25330.44</td>
      <td>18639.85</td>
      <td>306552</td>
      <td>12051</td>
      <td>1441</td>
      <td>new_users</td>
    </tr>
    <tr>
      <th>7</th>
      <td>46</td>
      <td>campaign_046</td>
      <td>paid_search</td>
      <td>2022-10-22</td>
      <td>2023-01-14</td>
      <td>21740.34</td>
      <td>15098.18</td>
      <td>450964</td>
      <td>3115</td>
      <td>282</td>
      <td>new_users</td>
    </tr>
    <tr>
      <th>8</th>
      <td>47</td>
      <td>campaign_047</td>
      <td>paid_search</td>
      <td>2022-11-19</td>
      <td>2022-11-26</td>
      <td>14809.86</td>
      <td>15518.99</td>
      <td>173939</td>
      <td>8764</td>
      <td>619</td>
      <td>developers</td>
    </tr>
    <tr>
      <th>9</th>
      <td>48</td>
      <td>campaign_048</td>
      <td>content_marketing</td>
      <td>2023-11-02</td>
      <td>2024-01-05</td>
      <td>45093.64</td>
      <td>46580.19</td>
      <td>37294</td>
      <td>264</td>
      <td>29</td>
      <td>enterprise_prospects</td>
    </tr>
    <tr>
      <th>10</th>
      <td>49</td>
      <td>campaign_049</td>
      <td>social_media</td>
      <td>2024-03-06</td>
      <td>2024-05-18</td>
      <td>11188.91</td>
      <td>11300.64</td>
      <td>157492</td>
      <td>5011</td>
      <td>579</td>
      <td>new_users</td>
    </tr>
  </tbody>
</table>
</div>



## ORDER BY


```python
# Show all customers sorted by acquisition_cost from highest to lowest.

sqldf ("""
    SELECT *
    FROM customers
    ORDER BY acquisition_cost DESC;
""")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>signup_date</th>
      <th>cohort_month</th>
      <th>acquisition_channel</th>
      <th>acquisition_campaign</th>
      <th>acquisition_cost</th>
      <th>country</th>
      <th>age</th>
      <th>gender</th>
      <th>plan_type</th>
      <th>is_active</th>
      <th>churn_date</th>
      <th>lifetime_days</th>
      <th>predicted_ltv</th>
      <th>risk_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>871</td>
      <td>2022-10-15</td>
      <td>2022-10</td>
      <td>paid_search</td>
      <td>brand_awareness</td>
      <td>79.63</td>
      <td>UK</td>
      <td>60</td>
      <td>F</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>656</td>
      <td>92.90</td>
      <td>0.70</td>
    </tr>
    <tr>
      <th>1</th>
      <td>161</td>
      <td>2023-08-12</td>
      <td>2023-08</td>
      <td>paid_search</td>
      <td>fall_launch</td>
      <td>78.20</td>
      <td>IN</td>
      <td>22</td>
      <td>M</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>355</td>
      <td>1584.26</td>
      <td>0.77</td>
    </tr>
    <tr>
      <th>2</th>
      <td>74</td>
      <td>2022-01-27</td>
      <td>2022-01</td>
      <td>paid_search</td>
      <td>winter_deal</td>
      <td>77.52</td>
      <td>BR</td>
      <td>55</td>
      <td>F</td>
      <td>enterprise</td>
      <td>1</td>
      <td>None</td>
      <td>917</td>
      <td>2655.36</td>
      <td>0.05</td>
    </tr>
    <tr>
      <th>3</th>
      <td>790</td>
      <td>2022-07-16</td>
      <td>2022-07</td>
      <td>paid_search</td>
      <td>winter_deal</td>
      <td>77.32</td>
      <td>US</td>
      <td>60</td>
      <td>M</td>
      <td>free</td>
      <td>0</td>
      <td>2022-11-10</td>
      <td>117</td>
      <td>93.41</td>
      <td>0.33</td>
    </tr>
    <tr>
      <th>4</th>
      <td>678</td>
      <td>2024-02-01</td>
      <td>2024-02</td>
      <td>paid_search</td>
      <td>webinar_series</td>
      <td>76.87</td>
      <td>AU</td>
      <td>23</td>
      <td>M</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>182</td>
      <td>97.90</td>
      <td>0.10</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>995</th>
      <td>926</td>
      <td>2022-08-07</td>
      <td>2022-08</td>
      <td>direct</td>
      <td>product_hunt</td>
      <td>0.09</td>
      <td>BR</td>
      <td>42</td>
      <td>M</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>725</td>
      <td>1729.13</td>
      <td>0.22</td>
    </tr>
    <tr>
      <th>996</th>
      <td>959</td>
      <td>2022-08-31</td>
      <td>2022-08</td>
      <td>organic_search</td>
      <td>brand_awareness</td>
      <td>0.09</td>
      <td>BR</td>
      <td>18</td>
      <td>F</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>701</td>
      <td>56.25</td>
      <td>0.89</td>
    </tr>
    <tr>
      <th>997</th>
      <td>14</td>
      <td>2023-09-06</td>
      <td>2023-09</td>
      <td>direct</td>
      <td>influencer_q2</td>
      <td>0.06</td>
      <td>CA</td>
      <td>37</td>
      <td>M</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>330</td>
      <td>27.09</td>
      <td>0.73</td>
    </tr>
    <tr>
      <th>998</th>
      <td>484</td>
      <td>2023-11-10</td>
      <td>2023-11</td>
      <td>direct</td>
      <td>summer_sale</td>
      <td>0.06</td>
      <td>IN</td>
      <td>42</td>
      <td>M</td>
      <td>basic</td>
      <td>1</td>
      <td>None</td>
      <td>265</td>
      <td>173.79</td>
      <td>0.32</td>
    </tr>
    <tr>
      <th>999</th>
      <td>553</td>
      <td>2022-11-17</td>
      <td>2022-11</td>
      <td>organic_search</td>
      <td>None</td>
      <td>0.04</td>
      <td>US</td>
      <td>18</td>
      <td>M</td>
      <td>basic</td>
      <td>1</td>
      <td>None</td>
      <td>623</td>
      <td>309.82</td>
      <td>0.72</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 15 columns</p>
</div>



## NULL handling


```python
# Find customers who have no churn_date (still active).

sqldf("""
    SELECT *
    FROM customers
    WHERE churn_date IS NULL
    LIMIT 20;
""")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>signup_date</th>
      <th>cohort_month</th>
      <th>acquisition_channel</th>
      <th>acquisition_campaign</th>
      <th>acquisition_cost</th>
      <th>country</th>
      <th>age</th>
      <th>gender</th>
      <th>plan_type</th>
      <th>is_active</th>
      <th>churn_date</th>
      <th>lifetime_days</th>
      <th>predicted_ltv</th>
      <th>risk_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2023-10-17</td>
      <td>2023-10</td>
      <td>paid_search</td>
      <td>spring_promo</td>
      <td>63.20</td>
      <td>UK</td>
      <td>32</td>
      <td>M</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>289</td>
      <td>69.08</td>
      <td>0.59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2022-02-02</td>
      <td>2022-02</td>
      <td>organic_search</td>
      <td>summer_sale</td>
      <td>1.09</td>
      <td>FR</td>
      <td>56</td>
      <td>M</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>911</td>
      <td>69.04</td>
      <td>0.23</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4</td>
      <td>2023-01-03</td>
      <td>2023-01</td>
      <td>direct</td>
      <td>product_hunt</td>
      <td>0.79</td>
      <td>US</td>
      <td>64</td>
      <td>M</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>576</td>
      <td>27.09</td>
      <td>0.30</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
      <td>2023-10-06</td>
      <td>2023-10</td>
      <td>direct</td>
      <td>product_hunt</td>
      <td>0.58</td>
      <td>US</td>
      <td>20</td>
      <td>F</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>300</td>
      <td>1551.66</td>
      <td>0.86</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8</td>
      <td>2022-11-20</td>
      <td>2022-11</td>
      <td>affiliate</td>
      <td>brand_awareness</td>
      <td>23.31</td>
      <td>BR</td>
      <td>63</td>
      <td>M</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>620</td>
      <td>1636.95</td>
      <td>0.46</td>
    </tr>
    <tr>
      <th>5</th>
      <td>9</td>
      <td>2022-09-29</td>
      <td>2022-09</td>
      <td>social_media</td>
      <td>winter_deal</td>
      <td>47.25</td>
      <td>FR</td>
      <td>34</td>
      <td>F</td>
      <td>basic</td>
      <td>1</td>
      <td>None</td>
      <td>672</td>
      <td>315.48</td>
      <td>0.99</td>
    </tr>
    <tr>
      <th>6</th>
      <td>10</td>
      <td>2022-05-22</td>
      <td>2022-05</td>
      <td>content_marketing</td>
      <td>summer_sale</td>
      <td>23.89</td>
      <td>US</td>
      <td>27</td>
      <td>F</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>802</td>
      <td>411.48</td>
      <td>0.38</td>
    </tr>
    <tr>
      <th>7</th>
      <td>11</td>
      <td>2023-04-25</td>
      <td>2023-04</td>
      <td>email</td>
      <td>webinar_series</td>
      <td>13.19</td>
      <td>US</td>
      <td>61</td>
      <td>F</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>464</td>
      <td>704.23</td>
      <td>0.64</td>
    </tr>
    <tr>
      <th>8</th>
      <td>13</td>
      <td>2023-10-03</td>
      <td>2023-10</td>
      <td>email</td>
      <td>None</td>
      <td>8.60</td>
      <td>UK</td>
      <td>27</td>
      <td>M</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>303</td>
      <td>103.02</td>
      <td>0.91</td>
    </tr>
    <tr>
      <th>9</th>
      <td>14</td>
      <td>2023-09-06</td>
      <td>2023-09</td>
      <td>direct</td>
      <td>influencer_q2</td>
      <td>0.06</td>
      <td>CA</td>
      <td>37</td>
      <td>M</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>330</td>
      <td>27.09</td>
      <td>0.73</td>
    </tr>
    <tr>
      <th>10</th>
      <td>16</td>
      <td>2024-02-13</td>
      <td>2024-02</td>
      <td>referral</td>
      <td>brand_awareness</td>
      <td>12.98</td>
      <td>IN</td>
      <td>59</td>
      <td>M</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>170</td>
      <td>676.98</td>
      <td>0.07</td>
    </tr>
    <tr>
      <th>11</th>
      <td>17</td>
      <td>2022-01-22</td>
      <td>2022-01</td>
      <td>referral</td>
      <td>product_hunt</td>
      <td>9.40</td>
      <td>US</td>
      <td>63</td>
      <td>F</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>922</td>
      <td>97.37</td>
      <td>0.08</td>
    </tr>
    <tr>
      <th>12</th>
      <td>18</td>
      <td>2022-09-01</td>
      <td>2022-09</td>
      <td>email</td>
      <td>None</td>
      <td>8.31</td>
      <td>FR</td>
      <td>26</td>
      <td>F</td>
      <td>pro</td>
      <td>1</td>
      <td>None</td>
      <td>700</td>
      <td>669.92</td>
      <td>0.47</td>
    </tr>
    <tr>
      <th>13</th>
      <td>19</td>
      <td>2023-02-21</td>
      <td>2023-02</td>
      <td>referral</td>
      <td>summer_sale</td>
      <td>6.94</td>
      <td>AU</td>
      <td>40</td>
      <td>M</td>
      <td>basic</td>
      <td>1</td>
      <td>None</td>
      <td>527</td>
      <td>483.62</td>
      <td>0.97</td>
    </tr>
    <tr>
      <th>14</th>
      <td>21</td>
      <td>2022-03-19</td>
      <td>2022-03</td>
      <td>content_marketing</td>
      <td>webinar_series</td>
      <td>7.45</td>
      <td>IN</td>
      <td>52</td>
      <td>F</td>
      <td>enterprise</td>
      <td>1</td>
      <td>None</td>
      <td>866</td>
      <td>5782.96</td>
      <td>0.17</td>
    </tr>
    <tr>
      <th>15</th>
      <td>22</td>
      <td>2023-05-13</td>
      <td>2023-05</td>
      <td>content_marketing</td>
      <td>winter_deal</td>
      <td>26.62</td>
      <td>US</td>
      <td>28</td>
      <td>M</td>
      <td>enterprise</td>
      <td>1</td>
      <td>None</td>
      <td>446</td>
      <td>5433.98</td>
      <td>0.46</td>
    </tr>
    <tr>
      <th>16</th>
      <td>23</td>
      <td>2023-03-10</td>
      <td>2023-03</td>
      <td>content_marketing</td>
      <td>fall_launch</td>
      <td>9.75</td>
      <td>UK</td>
      <td>21</td>
      <td>F</td>
      <td>basic</td>
      <td>1</td>
      <td>None</td>
      <td>510</td>
      <td>150.87</td>
      <td>0.58</td>
    </tr>
    <tr>
      <th>17</th>
      <td>24</td>
      <td>2023-05-30</td>
      <td>2023-05</td>
      <td>social_media</td>
      <td>spring_promo</td>
      <td>58.04</td>
      <td>US</td>
      <td>29</td>
      <td>M</td>
      <td>free</td>
      <td>1</td>
      <td>None</td>
      <td>429</td>
      <td>56.34</td>
      <td>0.93</td>
    </tr>
    <tr>
      <th>18</th>
      <td>25</td>
      <td>2023-08-07</td>
      <td>2023-08</td>
      <td>referral</td>
      <td>product_hunt</td>
      <td>16.89</td>
      <td>BR</td>
      <td>23</td>
      <td>M</td>
      <td>basic</td>
      <td>1</td>
      <td>None</td>
      <td>360</td>
      <td>624.74</td>
      <td>0.21</td>
    </tr>
    <tr>
      <th>19</th>
      <td>26</td>
      <td>2024-01-04</td>
      <td>2024-01</td>
      <td>direct</td>
      <td>winter_deal</td>
      <td>0.80</td>
      <td>US</td>
      <td>60</td>
      <td>F</td>
      <td>basic</td>
      <td>1</td>
      <td>None</td>
      <td>210</td>
      <td>625.30</td>
      <td>0.02</td>
    </tr>
  </tbody>
</table>
</div>



## COUNT


```python
# How many customers are there in total?

sqldf ("""
    SELECT COUNT(*) AS total_customers
    FROM customers
""")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>total_customers</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000</td>
    </tr>
  </tbody>
</table>
</div>



## COUNT with GROUP BY


```python
# How many customers per plan_type?

sqldf ("""
    SELECT plan_type, COUNT(*) AS total
    FROM customers
    GROUP BY plan_type
    ORDER BY total DESC;
""")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>plan_type</th>
      <th>total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>free</td>
      <td>336</td>
    </tr>
    <tr>
      <th>1</th>
      <td>basic</td>
      <td>311</td>
    </tr>
    <tr>
      <th>2</th>
      <td>pro</td>
      <td>254</td>
    </tr>
    <tr>
      <th>3</th>
      <td>enterprise</td>
      <td>99</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
