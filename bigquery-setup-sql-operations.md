# BigQuery Setup and SQL Operations

## 1. Open BigQuery

1. Sign in to the **Google Cloud Console**.
2. Select your **GCP Project**.
3. From the navigation menu, go to **BigQuery**.
4. Click **SQL workspace**.

## 2. Create a Dataset

1. In **Explorer**, select your project.
2. Click **⋮** next to the project name.
3. Select **Create dataset**.
4. Enter a Dataset ID, for example:
   ```text
   sales_dataset
   ```
5. Select the **Data location**.
6. Click **Create dataset**.

## 3. Create a Table

You can create a table from:

- Uploading a file
- Google Cloud Storage
- SQL query
- Empty table

### Create an Empty Table

1. Select your dataset.
2. Click **Create table**.
3. Choose **Create table from → Empty table**.
4. Enter the table name, for example:
   ```text
   customer
   ```
5. Add schema fields:

| Field | Data Type |
|---|---|
| customer_id | INTEGER |
| customer_name | STRING |
| city | STRING |
| purchase_amount | FLOAT |

6. Click **Create table**.

## 4. Insert Data Using SQL

Run the following query in the **SQL workspace**:

```sql
INSERT INTO `project_id.sales_dataset.customer`
(customer_id, customer_name, city, purchase_amount)
VALUES
  (1, 'Ravi', 'Chennai', 2500),
  (2, 'Priya', 'Bangalore', 3500),
  (3, 'Arun', 'Chennai', 1800);
```

> Replace `project_id` with your actual GCP project ID.

## 5. Query the Data

### Display All Data

```sql
SELECT *
FROM `project_id.sales_dataset.customer`;
```

### Analytical Query

```sql
SELECT
  city,
  COUNT(*) AS total_customers,
  SUM(purchase_amount) AS total_sales
FROM `project_id.sales_dataset.customer`
GROUP BY city
ORDER BY total_sales DESC;
```

This query:

- Groups customers by city.
- Counts the number of customers in each city.
- Calculates total sales for each city.
- Sorts cities by total sales in descending order.

## 6. Create a Partitioned Table

When creating a table, you can choose **Partitioning**.

For example, if you have a `transaction_date` column:

```sql
CREATE TABLE `project_id.sales_dataset.transactions`
(
  transaction_id INT64,
  customer_id INT64,
  transaction_date DATE,
  amount NUMERIC
)
PARTITION BY transaction_date;
```

### Why Use Partitioning?

Partitioning divides a large table into smaller sections based on a column such as date.

For example:

```text
transactions
│
├── 2026-08-16
├── 2026-08-17
├── 2026-08-18
└── ...
```

When a query filters by date, BigQuery can scan only the required partitions instead of the entire table.

**Benefits:**

- Reduces data scanned.
- Reduces query processing cost.
- Improves query performance.

## 7. Create a Clustered Table

You can also cluster a table based on columns that are frequently used for filtering or grouping.

```sql
CREATE TABLE `project_id.sales_dataset.transactions`
(
  transaction_id INT64,
  customer_id INT64,
  transaction_date DATE,
  city STRING,
  amount NUMERIC
)
PARTITION BY transaction_date
CLUSTER BY customer_id, city;
```

Here:

- **Partitioning:** `transaction_date`
- **Clustering:** `customer_id`, `city`

Partitioning organizes data into partitions, while clustering organizes data within those partitions based on the specified columns.

## 8. View Query Results

After running a query in BigQuery, you can view:

### Results

Displays the rows returned by your query.

### Execution Details

Shows information about how BigQuery executed the query, including data processed and execution stages.

### Query History

Shows previously executed queries so you can review or run them again.

## Quick Summary

| Operation | Purpose |
|---|---|
| Dataset | Organizes tables |
| Table | Stores structured data |
| INSERT | Adds data to a table |
| SELECT | Retrieves data |
| Partitioning | Reduces data scanned using partitions |
| Clustering | Organizes data for efficient filtering |
| Results | Displays query output |
| Execution Details | Shows query execution information |
| Query History | Shows previous queries |
