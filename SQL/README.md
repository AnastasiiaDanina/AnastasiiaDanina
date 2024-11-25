## SQL Script for Email_Metrics

This SQL script aggregates multiple metrics related to revenue, email campaigns, and account registrations across different data sources. The script calculates key metrics per day, combining data from various tables, such as orders, email sends, email opens, email visits, and account registrations.

### Script Breakdown:

1. **Revenue Calculation (`revenue_usd`)**:
   - Calculates total revenue per day by joining the `order` and `product` tables.
   - Revenue is summed up based on the prices of the products sold.

2. **Email Metrics (`email_metrics`)**:
   - Tracks email campaign performance, including the number of sent, opened, and clicked emails.
   - Joins multiple tables (`email_sent`, `account_session`, `session`, `email_open`, `email_visit`) to calculate these metrics by date.

3. **Registrations (`registrations`)**:
   - Counts the number of account registrations per day by joining the `account_session` and `session` tables.

4. **Combining Data (`final`)**:
   - Aggregates all the metrics (revenue, cost, email metrics, and registrations) into one unified table for each date.
   - Uses `UNION ALL` to merge results from different metric sources.

5. **Final Output**:
   - The final `SELECT` statement aggregates the data by date and provides the summed values of revenue, cost, email metrics (sent, opened, clicked), and account registrations.

### Usage:
- This script is useful for tracking and analyzing daily performance across multiple channels (revenue, email marketing, registrations).
- It can be customized to add additional metrics or adjust the date ranges.

### Tables Used:
- `DA.order`
- `DA.product`
- `DA.session`
- `DA.email_sent`
- `DA.account_session`
- `DA.email_open`
- `DA.email_visit`
- `DA.paid_search_cost`
# SQL Script for ecommerce_data_analysis

## Description
This SQL query extracts and organizes key metrics from an e-commerce database to analyze user activity and interactions with email campaigns. The query creates a unified dataset with metrics grouped by date and country, providing insights into account creation, email campaign engagement, and user interactions.

### Output Dataset Columns:
- **date**: The date of the activity (account creation or email sent).
- **country**: The country of the user.
- **send_interval**: The interval for email sending.
- **is_verified**: Indicates whether an account is verified.
- **is_unsubscribed**: Indicates whether a user unsubscribed.
- **account_cnt**: Total number of accounts created.
- **sent_msg**: Number of emails sent.
- **open_msg**: Number of emails opened.
- **visit_msg**: Number of email clicks (visits from email).
- **total_country_account_cnt**: Total number of accounts created by country.
- **total_country_sent_cnt**: Total number of emails sent by country.
- **rank_total_country_account_cnt**: Rank of countries by total accounts created.
- **rank_total_country_sent_cnt**: Rank of countries by total emails sent.

## Query Structure and Logic

### CTEs for Data Segmentation:
- The query begins by organizing account creation data in the `account_data` CTE and email metrics in the `email_metrics` CTE.
- Each CTE gathers data with a focus on either account activities or email interactions, ensuring independence between these two data segments. They are then combined using `UNION ALL`.

### Window Functions and Aggregation:
- The query uses window functions to calculate the total account creation count by country (`total_country_account_cnt`) and the total emails sent by country (`total_country_sent_cnt`).
- It ranks each country based on these totals (`rank_total_country_account_cnt` and `rank_total_country_sent_cnt`), enabling easy comparison between countries.

### Filtering and Final Output:
- The final selection only includes records where either the account creation rank or email sent rank is within the top 10. This highlights the most active countries in terms of account creation and email engagement.

## Visualization
The query results can be visualized in Looker Studio to display key metrics such as:
- **Total accounts created** (`account_cnt`)
- **Total emails sent by country** (`total_country_sent_cnt`)
- **Country ranking by account creation** (`rank_total_country_account_cnt`)
- **Country ranking by emails sent** (`rank_total_country_sent_cnt`)
- **Daily trend of sent messages** (`sent_msg`)

For a closer look, check the visualization in [Looker Studio](https://lookerstudio.google.com/reporting/bd6f8eb0-9e85-4da6-8353-c41b5e73016b). 
