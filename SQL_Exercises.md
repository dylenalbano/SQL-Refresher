# SQL Exercises — Beginner to Advanced

Setup cell (run first in every session):
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

---

## LEVEL 1 — SELECT, WHERE, ORDER BY

These are the building blocks. Every SQL query starts here.

### Exercise 1.1 — Select all columns
Retrieve the first 10 rows from the `customers` table.
```
Hint: SELECT ... FROM ... LIMIT ...
```

<details><summary>Answer</summary>

```python
sqldf("SELECT * FROM customers LIMIT 10")
```
</details>

---

### Exercise 1.2 — Select specific columns
Show only `customer_id`, `signup_date`, and `plan_type` from customers.

<details><summary>Answer</summary>

```python
sqldf("SELECT customer_id, signup_date, plan_type FROM customers LIMIT 10")
```
</details>

---

### Exercise 1.3 — WHERE with one condition
Find all customers on the `enterprise` plan.

<details><summary>Answer</summary>

```python
sqldf("SELECT * FROM customers WHERE plan_type = 'enterprise'")
```
</details>

---

### Exercise 1.4 — WHERE with multiple conditions (AND)
Find customers who signed up after 2023-01-01 AND are on the `pro` plan.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT * FROM customers 
    WHERE signup_date > '2023-01-01' AND plan_type = 'pro'
""")
```
</details>

---

### Exercise 1.5 — WHERE with OR
Find customers from the US or UK.

<details><summary>Answer</summary>

```python
sqldf("SELECT * FROM customers WHERE country = 'US' OR country = 'UK'")
```
</details>

---

### Exercise 1.6 — IN operator
Same as above but using IN — find customers from US, UK, or CA.

<details><summary>Answer</summary>

```python
sqldf("SELECT * FROM customers WHERE country IN ('US', 'UK', 'CA')")
```
</details>

---

### Exercise 1.7 — BETWEEN
Find transactions with amounts between 100 and 500.

<details><summary>Answer</summary>

```python
sqldf("SELECT * FROM transactions WHERE amount BETWEEN 100 AND 500 LIMIT 20")
```
</details>

---

### Exercise 1.8 — LIKE (pattern matching)
Find all campaigns with "influencer" in the name.

<details><summary>Answer</summary>

```python
sqldf("SELECT * FROM marketing_campaigns WHERE campaign_name LIKE '%influencer%'")
```
</details>

---

### Exercise 1.9 — ORDER BY
Show all customers sorted by `acquisition_cost` from highest to lowest.

<details><summary>Answer</summary>

```python
sqldf("SELECT * FROM customers ORDER BY acquisition_cost DESC LIMIT 15")
```
</details>

---

### Exercise 1.10 — NULL handling
Find customers who have no `churn_date` (still active).

<details><summary>Answer</summary>

```python
sqldf("SELECT * FROM customers WHERE churn_date IS NULL LIMIT 10")
```
</details>

---

## LEVEL 2 — Aggregation (GROUP BY, COUNT, SUM, AVG)

This is where SQL gets powerful — summarizing data.

### Exercise 2.1 — COUNT
How many customers are there in total?

<details><summary>Answer</summary>

```python
sqldf("SELECT COUNT(*) as total_customers FROM customers")
```
</details>

---

### Exercise 2.2 — COUNT with GROUP BY
How many customers per `plan_type`?

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT plan_type, COUNT(*) as total
    FROM customers
    GROUP BY plan_type
    ORDER BY total DESC
""")
```
</details>

---

### Exercise 2.3 — SUM
What is the total revenue from all non-refund transactions?

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT ROUND(SUM(amount), 2) as total_revenue
    FROM transactions
    WHERE is_refund = 0
""")
```
</details>

---

### Exercise 2.4 — AVG
What is the average acquisition cost per channel?

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT acquisition_channel,
           ROUND(AVG(acquisition_cost), 2) as avg_cac,
           COUNT(*) as num_customers
    FROM customers
    GROUP BY acquisition_channel
    ORDER BY avg_cac DESC
""")
```
</details>

---

### Exercise 2.5 — MIN / MAX
Find the earliest and latest signup dates.

<details><summary>Answer</summary>

```python
sqldf("SELECT MIN(signup_date) as first_signup, MAX(signup_date) as last_signup FROM customers")
```
</details>

---

### Exercise 2.6 — GROUP BY with multiple columns
Count customers by `country` and `plan_type`.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT country, plan_type, COUNT(*) as total
    FROM customers
    GROUP BY country, plan_type
    ORDER BY country, total DESC
""")
```
</details>

---

### Exercise 2.7 — HAVING (filter after aggregation)
Which acquisition channels brought in more than 100 customers?

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT acquisition_channel, COUNT(*) as total
    FROM customers
    GROUP BY acquisition_channel
    HAVING total > 100
    ORDER BY total DESC
""")
```
</details>

---

### Exercise 2.8 — DISTINCT
How many unique countries are in the dataset?

<details><summary>Answer</summary>

```python
sqldf("SELECT COUNT(DISTINCT country) as unique_countries FROM customers")
```
</details>

---

### Exercise 2.9 — Revenue by product category
What is the total and average revenue per `product_category` (excluding refunds)?

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT product_category,
           COUNT(*) as num_transactions,
           ROUND(SUM(amount), 2) as total_revenue,
           ROUND(AVG(amount), 2) as avg_transaction
    FROM transactions
    WHERE is_refund = 0
    GROUP BY product_category
    ORDER BY total_revenue DESC
""")
```
</details>

---

### Exercise 2.10 — Monthly signup trend
How many customers signed up each month?

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT cohort_month, COUNT(*) as signups
    FROM customers
    GROUP BY cohort_month
    ORDER BY cohort_month
""")
```
</details>

---

## LEVEL 3 — JOINs

Combining data from multiple tables — this is where real analysis happens.

### Exercise 3.1 — INNER JOIN
Show each transaction with the customer's plan type.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT t.transaction_id, t.customer_id, t.amount, t.product_category, c.plan_type
    FROM transactions t
    JOIN customers c ON t.customer_id = c.customer_id
    LIMIT 15
""")
```
</details>

---

### Exercise 3.2 — JOIN + GROUP BY
Total revenue per plan type.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT c.plan_type,
           COUNT(t.transaction_id) as num_transactions,
           ROUND(SUM(t.amount), 2) as total_revenue
    FROM customers c
    JOIN transactions t ON c.customer_id = t.customer_id
    WHERE t.is_refund = 0
    GROUP BY c.plan_type
    ORDER BY total_revenue DESC
""")
```
</details>

---

### Exercise 3.3 — LEFT JOIN
Show all customers and their transaction count. Include customers with zero transactions.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT c.customer_id, c.plan_type,
           COUNT(t.transaction_id) as txn_count
    FROM customers c
    LEFT JOIN transactions t ON c.customer_id = t.customer_id
    GROUP BY c.customer_id
    ORDER BY txn_count ASC
    LIMIT 20
""")
```
</details>

---

### Exercise 3.4 — JOIN three tables
For each customer, show their plan, total revenue, and number of events.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT c.customer_id, c.plan_type,
           COALESCE(SUM(t.amount), 0) as total_revenue,
           COUNT(DISTINCT e.event_id) as event_count
    FROM customers c
    LEFT JOIN transactions t ON c.customer_id = t.customer_id AND t.is_refund = 0
    LEFT JOIN customer_events e ON c.customer_id = e.customer_id
    GROUP BY c.customer_id
    LIMIT 15
""")
```
</details>

---

### Exercise 3.5 — Revenue per channel
Which acquisition channel generates the most revenue?

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT c.acquisition_channel,
           COUNT(DISTINCT c.customer_id) as customers,
           ROUND(SUM(t.amount), 2) as total_revenue,
           ROUND(SUM(t.amount) / COUNT(DISTINCT c.customer_id), 2) as revenue_per_customer
    FROM customers c
    JOIN transactions t ON c.customer_id = t.customer_id
    WHERE t.is_refund = 0
    GROUP BY c.acquisition_channel
    ORDER BY revenue_per_customer DESC
""")
```
</details>

---

## LEVEL 4 — Subqueries

Queries inside queries — for when one pass isn't enough.

### Exercise 4.1 — Subquery in WHERE
Find customers whose total spend is above the overall average.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT customer_id, total_spend
    FROM (
        SELECT customer_id, SUM(amount) as total_spend
        FROM transactions
        WHERE is_refund = 0
        GROUP BY customer_id
    )
    WHERE total_spend > (
        SELECT AVG(total_spend) FROM (
            SELECT SUM(amount) as total_spend
            FROM transactions
            WHERE is_refund = 0
            GROUP BY customer_id
        )
    )
    ORDER BY total_spend DESC
""")
```
</details>

---

### Exercise 4.2 — Subquery as a table (derived table)
Calculate LTV:CAC ratio per channel using a revenue subquery.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT c.acquisition_channel,
           ROUND(AVG(c.acquisition_cost), 2) as avg_cac,
           ROUND(AVG(rev.total_revenue), 2) as avg_ltv,
           ROUND(AVG(rev.total_revenue) / AVG(c.acquisition_cost), 2) as ltv_cac_ratio
    FROM customers c
    JOIN (
        SELECT customer_id, SUM(amount) as total_revenue
        FROM transactions WHERE is_refund = 0
        GROUP BY customer_id
    ) rev ON c.customer_id = rev.customer_id
    WHERE c.acquisition_cost > 0
    GROUP BY c.acquisition_channel
    ORDER BY ltv_cac_ratio DESC
""")
```
</details>

---

### Exercise 4.3 — Correlated subquery
For each customer, show how their spend compares to the average of their plan type.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT c.customer_id, c.plan_type,
           COALESCE(t.total_spend, 0) as total_spend,
           plan_avg.avg_spend,
           ROUND(COALESCE(t.total_spend, 0) - plan_avg.avg_spend, 2) as vs_plan_avg
    FROM customers c
    LEFT JOIN (
        SELECT customer_id, SUM(amount) as total_spend
        FROM transactions WHERE is_refund = 0
        GROUP BY customer_id
    ) t ON c.customer_id = t.customer_id
    JOIN (
        SELECT c2.plan_type, AVG(t2.total_spend) as avg_spend
        FROM customers c2
        JOIN (
            SELECT customer_id, SUM(amount) as total_spend
            FROM transactions WHERE is_refund = 0
            GROUP BY customer_id
        ) t2 ON c2.customer_id = t2.customer_id
        GROUP BY c2.plan_type
    ) plan_avg ON c.plan_type = plan_avg.plan_type
    ORDER BY vs_plan_avg DESC
    LIMIT 15
""")
```
</details>

---

## LEVEL 5 — CASE statements

Add conditional logic inside your queries.

### Exercise 5.1 — Basic CASE
Categorize customers by acquisition cost: 'Free' (0), 'Low' (1-20), 'Medium' (21-50), 'High' (51+).

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT customer_id, acquisition_cost,
           CASE
               WHEN acquisition_cost = 0 THEN 'Free'
               WHEN acquisition_cost <= 20 THEN 'Low'
               WHEN acquisition_cost <= 50 THEN 'Medium'
               ELSE 'High'
           END as cost_tier
    FROM customers
    LIMIT 20
""")
```
</details>

---

### Exercise 5.2 — CASE with aggregation
Count active vs churned customers per plan type.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT plan_type,
           SUM(CASE WHEN is_active = 1 THEN 1 ELSE 0 END) as active,
           SUM(CASE WHEN is_active = 0 THEN 1 ELSE 0 END) as churned,
           ROUND(SUM(CASE WHEN is_active = 0 THEN 1.0 ELSE 0 END) / COUNT(*) * 100, 1) as churn_rate_pct
    FROM customers
    GROUP BY plan_type
    ORDER BY churn_rate_pct DESC
""")
```
</details>

---

### Exercise 5.3 — CASE for risk segmentation
Segment customers into risk buckets using `risk_score`: Low (<0.3), Medium (0.3-0.6), High (>0.6). Show count and avg predicted LTV per segment.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT
        CASE
            WHEN risk_score < 0.3 THEN 'Low Risk'
            WHEN risk_score <= 0.6 THEN 'Medium Risk'
            ELSE 'High Risk'
        END as risk_segment,
        COUNT(*) as customers,
        ROUND(AVG(predicted_ltv), 2) as avg_predicted_ltv,
        ROUND(AVG(is_active) * 100, 1) as pct_active
    FROM customers
    GROUP BY risk_segment
    ORDER BY pct_active DESC
""")
```
</details>

---

## LEVEL 6 — Window Functions

Perform calculations across rows without collapsing them. This is advanced SQL that separates analysts from beginners.

### Exercise 6.1 — ROW_NUMBER
Rank customers by total spend within each plan type.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT customer_id, plan_type, total_spend,
           ROW_NUMBER() OVER (PARTITION BY plan_type ORDER BY total_spend DESC) as rank_in_plan
    FROM (
        SELECT c.customer_id, c.plan_type, SUM(t.amount) as total_spend
        FROM customers c
        JOIN transactions t ON c.customer_id = t.customer_id
        WHERE t.is_refund = 0
        GROUP BY c.customer_id
    )
    WHERE rank_in_plan <= 5
""")
```
</details>

---

### Exercise 6.2 — Running total
Calculate cumulative daily signups over time.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT date, new_signups,
           SUM(new_signups) OVER (ORDER BY date) as cumulative_signups
    FROM daily_acquisition_stats
    LIMIT 30
""")
```
</details>

---

### Exercise 6.3 — Moving average
Calculate 7-day moving average of daily spend.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT date, total_spend,
           ROUND(AVG(total_spend) OVER (
               ORDER BY date 
               ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
           ), 2) as spend_7day_avg
    FROM daily_acquisition_stats
    LIMIT 30
""")
```
</details>

---

### Exercise 6.4 — LAG / LEAD
Show each month's signups alongside the previous month's signups and the month-over-month change.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT cohort_month,
           signups,
           LAG(signups) OVER (ORDER BY cohort_month) as prev_month,
           signups - LAG(signups) OVER (ORDER BY cohort_month) as mom_change
    FROM (
        SELECT cohort_month, COUNT(*) as signups
        FROM customers
        GROUP BY cohort_month
    )
    ORDER BY cohort_month
""")
```
</details>

---

### Exercise 6.5 — NTILE (percentiles)
Divide customers into LTV quartiles and profile each quartile.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT quartile,
           COUNT(*) as customers,
           ROUND(MIN(total_spend), 2) as min_spend,
           ROUND(MAX(total_spend), 2) as max_spend,
           ROUND(AVG(total_spend), 2) as avg_spend
    FROM (
        SELECT c.customer_id,
               COALESCE(SUM(t.amount), 0) as total_spend,
               NTILE(4) OVER (ORDER BY COALESCE(SUM(t.amount), 0)) as quartile
        FROM customers c
        LEFT JOIN transactions t ON c.customer_id = t.customer_id AND t.is_refund = 0
        GROUP BY c.customer_id
    )
    GROUP BY quartile
    ORDER BY quartile
""")
```
</details>

---

## LEVEL 7 — CTEs (Common Table Expressions)

Clean, readable way to organize complex queries. Used heavily in real analytics work.

### Exercise 7.1 — Basic CTE
Use a CTE to calculate revenue per customer, then find the top 10.

<details><summary>Answer</summary>

```python
sqldf("""
    WITH customer_revenue AS (
        SELECT customer_id, SUM(amount) as total_revenue
        FROM transactions
        WHERE is_refund = 0
        GROUP BY customer_id
    )
    SELECT c.customer_id, c.plan_type, c.acquisition_channel,
           cr.total_revenue
    FROM customers c
    JOIN customer_revenue cr ON c.customer_id = cr.customer_id
    ORDER BY cr.total_revenue DESC
    LIMIT 10
""")
```
</details>

---

### Exercise 7.2 — Multiple CTEs
Calculate both revenue and engagement per customer, then combine.

<details><summary>Answer</summary>

```python
sqldf("""
    WITH revenue AS (
        SELECT customer_id,
               SUM(amount) as total_revenue,
               COUNT(*) as txn_count
        FROM transactions WHERE is_refund = 0
        GROUP BY customer_id
    ),
    engagement AS (
        SELECT customer_id,
               COUNT(*) as event_count,
               COUNT(DISTINCT feature_used) as unique_features,
               AVG(session_duration_sec) as avg_session
        FROM customer_events
        GROUP BY customer_id
    )
    SELECT c.customer_id, c.plan_type, c.is_active,
           COALESCE(r.total_revenue, 0) as revenue,
           COALESCE(r.txn_count, 0) as transactions,
           COALESCE(e.event_count, 0) as events,
           COALESCE(e.unique_features, 0) as features_used,
           ROUND(COALESCE(e.avg_session, 0), 0) as avg_session_sec
    FROM customers c
    LEFT JOIN revenue r ON c.customer_id = r.customer_id
    LEFT JOIN engagement e ON c.customer_id = e.customer_id
    ORDER BY revenue DESC
    LIMIT 15
""")
```
</details>

---

### Exercise 7.3 — CTE for cohort retention (build it yourself)
Build a cohort retention table from scratch using `customers` and `transactions` — don't use the pre-built `monthly_cohort_metrics` table.

<details><summary>Answer</summary>

```python
sqldf("""
    WITH cohort_txns AS (
        SELECT c.cohort_month,
               c.customer_id,
               CAST((CAST(SUBSTR(t.transaction_date, 1, 4) AS INT) - CAST(SUBSTR(c.signup_date, 1, 4) AS INT)) * 12
                   + (CAST(SUBSTR(t.transaction_date, 6, 2) AS INT) - CAST(SUBSTR(c.signup_date, 6, 2) AS INT)) AS INT) as months_since
        FROM customers c
        JOIN transactions t ON c.customer_id = t.customer_id
        WHERE t.is_refund = 0
    ),
    cohort_sizes AS (
        SELECT cohort_month, COUNT(*) as cohort_size
        FROM customers
        GROUP BY cohort_month
    )
    SELECT ct.cohort_month,
           ct.months_since,
           cs.cohort_size,
           COUNT(DISTINCT ct.customer_id) as retained,
           ROUND(COUNT(DISTINCT ct.customer_id) * 100.0 / cs.cohort_size, 1) as retention_pct
    FROM cohort_txns ct
    JOIN cohort_sizes cs ON ct.cohort_month = cs.cohort_month
    WHERE ct.months_since BETWEEN 0 AND 6
    GROUP BY ct.cohort_month, ct.months_since
    ORDER BY ct.cohort_month, ct.months_since
""")
```
</details>

---

## LEVEL 8 — Business Analytics Queries

Real-world questions you'd answer as a data analyst.

### Exercise 8.1 — Campaign ROI
Estimate ROI for each marketing campaign.

<details><summary>Answer</summary>

```python
sqldf("""
    SELECT campaign_name, channel, spend, conversions,
           ROUND(spend / CASE WHEN conversions > 0 THEN conversions ELSE 1 END, 2) as cost_per_conversion,
           ROUND((conversions * 200.0 - spend) / spend * 100, 1) as estimated_roi_pct
    FROM marketing_campaigns
    WHERE spend > 0
    ORDER BY estimated_roi_pct DESC
    LIMIT 15
""")
```
</details>

---

### Exercise 8.2 — Payback period by channel
How many months until cumulative revenue exceeds acquisition cost, by channel?

<details><summary>Answer</summary>

```python
sqldf("""
    WITH monthly_rev AS (
        SELECT c.customer_id, c.acquisition_channel, c.acquisition_cost,
               CAST((CAST(SUBSTR(t.transaction_date, 1, 4) AS INT) - CAST(SUBSTR(c.signup_date, 1, 4) AS INT)) * 12
                   + (CAST(SUBSTR(t.transaction_date, 6, 2) AS INT) - CAST(SUBSTR(c.signup_date, 6, 2) AS INT)) AS INT) as month_num,
               SUM(t.amount) as revenue
        FROM customers c
        JOIN transactions t ON c.customer_id = t.customer_id
        WHERE t.is_refund = 0 AND c.acquisition_cost > 0
        GROUP BY c.customer_id, month_num
    ),
    cum_rev AS (
        SELECT customer_id, acquisition_channel, acquisition_cost, month_num,
               SUM(revenue) OVER (PARTITION BY customer_id ORDER BY month_num) as cumulative_rev
        FROM monthly_rev
    ),
    payback AS (
        SELECT customer_id, acquisition_channel,
               MIN(month_num) as payback_month
        FROM cum_rev
        WHERE cumulative_rev >= acquisition_cost
        GROUP BY customer_id
    )
    SELECT acquisition_channel,
           COUNT(*) as customers_with_payback,
           ROUND(AVG(payback_month), 1) as avg_payback_months
    FROM payback
    GROUP BY acquisition_channel
    ORDER BY avg_payback_months
""")
```
</details>

---

### Exercise 8.3 — Full churn prediction feature table
Build a dataset ready for machine learning. Each row = one customer with features.

<details><summary>Answer</summary>

```python
sqldf("""
    WITH rev AS (
        SELECT customer_id,
               COUNT(*) as txn_count,
               SUM(CASE WHEN is_refund = 0 THEN amount ELSE 0 END) as total_spend,
               SUM(CASE WHEN is_refund = 1 THEN 1 ELSE 0 END) as refund_count,
               COUNT(DISTINCT product_category) as product_categories
        FROM transactions
        GROUP BY customer_id
    ),
    eng AS (
        SELECT customer_id,
               COUNT(*) as event_count,
               COUNT(DISTINCT feature_used) as unique_features,
               ROUND(AVG(session_duration_sec), 0) as avg_session_sec,
               ROUND(AVG(pages_viewed), 1) as avg_pages,
               SUM(CASE WHEN event_type = 'support_ticket' THEN 1 ELSE 0 END) as support_tickets
        FROM customer_events
        GROUP BY customer_id
    )
    SELECT c.customer_id,
           c.plan_type,
           c.acquisition_channel,
           c.acquisition_cost,
           c.country,
           c.age,
           c.gender,
           c.lifetime_days,
           c.risk_score,
           COALESCE(r.txn_count, 0) as txn_count,
           COALESCE(r.total_spend, 0) as total_spend,
           COALESCE(r.refund_count, 0) as refund_count,
           COALESCE(r.product_categories, 0) as product_categories,
           COALESCE(e.event_count, 0) as event_count,
           COALESCE(e.unique_features, 0) as unique_features,
           COALESCE(e.avg_session_sec, 0) as avg_session_sec,
           COALESCE(e.avg_pages, 0) as avg_pages,
           COALESCE(e.support_tickets, 0) as support_tickets,
           c.is_active as target_is_active
    FROM customers c
    LEFT JOIN rev r ON c.customer_id = r.customer_id
    LEFT JOIN eng e ON c.customer_id = e.customer_id
""")
```
</details>

---

## BONUS — Save query results for predictive modeling

Once you've built the churn feature table in Exercise 8.3, save it and build a model:

```python
# Save the feature table
churn_df = sqldf("""...""")  # paste Exercise 8.3 query here

# Quick logistic regression
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import classification_report
import pandas as pd

# Encode categoricals
model_df = pd.get_dummies(churn_df, columns=['plan_type', 'acquisition_channel', 'country', 'gender'], drop_first=True)

X = model_df.drop(columns=['customer_id', 'target_is_active'])
y = model_df['target_is_active']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

model = LogisticRegression(max_iter=1000)
model.fit(X_train, y_train)

print(classification_report(y_test, model.predict(X_test)))
```

---

## Concept Reference

| Concept | Level | What it does |
|---|---|---|
| SELECT, WHERE, ORDER BY | 1 | Filter and sort rows |
| GROUP BY, COUNT, SUM, AVG | 2 | Summarize data |
| JOIN, LEFT JOIN | 3 | Combine tables |
| Subqueries | 4 | Nest queries inside queries |
| CASE | 5 | Conditional logic |
| Window functions (ROW_NUMBER, LAG, NTILE) | 6 | Calculations across rows |
| CTEs (WITH) | 7 | Organize complex queries |
| Business analytics | 8 | Real-world analysis patterns |
