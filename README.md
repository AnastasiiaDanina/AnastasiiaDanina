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
