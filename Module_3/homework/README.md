## Dataset

**Source:** [NYC TLC Trip Record Data](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)


### 1. Create External Table
```sql
CREATE OR REPLACE EXTERNAL TABLE `case-study-53427.zoomcamp.yellow_taxi_external_table`
OPTIONS (
  format = 'PARQUET',
  uris = ['gs://your-bucket-name/*.parquet']
);
```

### 2. Create Materialized Table
```sql
CREATE OR REPLACE TABLE `case-study-53427.zoomcamp.yellow_taxi_materialized_table`
AS
SELECT *
FROM `case-study-53427.zoomcamp.yellow_taxi_external_table`;
```

## Questions & Solutions

### Question 1: 
**What is the count of records for the 2024 Yellow Taxi Data?**

**Query:**
```sql
SELECT COUNT(*) AS total_records
FROM `case-study-53427.zoomcamp.yellow_taxi_materialized_table`;
```

---

### Question 2: 
**What is the estimated amount of data that will be read when this query is executed on the External Table and the Table?**

**Query for External Table:**
```sql
SELECT COUNT(DISTINCT PULocationID)
FROM `case-study-53427.zoomcamp.yellow_taxi_external_table`;
```

**Query for Materialized Table:**
```sql
SELECT COUNT(DISTINCT PULocationID)
FROM `case-study-53427.zoomcamp.yellow_taxi_materialized_table`;
```

---

### Question 3: 
**Why are the estimated number of Bytes different?**

**Query 1 (Single Column):**
```sql
SELECT PULocationID
FROM `case-study-53427.zoomcamp.yellow_taxi_materialized_table`;
```

**Query 2 (Two Columns):**
```sql
SELECT PULocationID, DOLocationID
FROM `case-study-53427.zoomcamp.yellow_taxi_materialized_table`;
```

---

### Question 4: 
**How many records have a fare_amount of 0?**

**Query:**
```sql
SELECT COUNT(*) AS zero_fare_count
FROM `case-study-53427.zoomcamp.yellow_taxi_materialized_table`
WHERE fare_amount = 0;
```

---

### Question 5: 
**What is the best strategy to make an optimized table in Big Query if your query will always filter based on tpep_dropoff_datetime and order the results by VendorID?**

**Query:**
```sql
CREATE OR REPLACE TABLE `case-study-53427.zoomcamp.yellow_taxi_partitioned`
PARTITION BY DATE(tpep_dropoff_datetime)
CLUSTER BY VendorID
AS
SELECT *
FROM `case-study-53427.zoomcamp.yellow_taxi_materialized_table`;
```

---

### Question 6: 
**Write a query to retrieve the distinct VendorIDs between tpep_dropoff_datetime 2024-03-01 and 2024-03-15 (inclusive).**

**Query on Non-Partitioned Table:**
```sql
SELECT DISTINCT VendorID
FROM `case-study-53427.zoomcamp.yellow_taxi_materialized_table`
WHERE tpep_dropoff_datetime BETWEEN '2024-03-01' AND '2024-03-15';
```

**Query on Partitioned Table:**
```sql
SELECT DISTINCT VendorID
FROM `case-study-53427.zoomcamp.yellow_taxi_partitioned`
WHERE tpep_dropoff_datetime BETWEEN '2024-03-01' AND '2024-03-15';
```








