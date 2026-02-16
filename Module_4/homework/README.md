# Homework

### Question 3:

**Q:** Count of records in fct_monthly_zone_revenue?

```sql
SELECT COUNT(*)
FROM {{ ref('fct_monthly_zone_revenue') }};
```

---

### Question 4:

**Q:** Zone with highest revenue for Green taxis in 2020?

```sql
SELECT
    pickup_zone,
    SUM(revenue_monthly_total_amount) AS total_revenue
FROM {{ ref('fct_monthly_zone_revenue') }}
WHERE service_type = 'Green'
  AND year = 2020
GROUP BY pickup_zone
ORDER BY total_revenue DESC
LIMIT 1;
```

---

### Question 5: 

**Q:** Total trips for Green taxis in October 2019?

```sql
SELECT
    SUM(total_monthly_trips)
FROM {{ ref('fct_monthly_zone_revenue') }}
WHERE service_type = 'Green'
  AND year = 2019
  AND month = 10;
```

---

### Question 6:

**Q:** Count of records in stg_fhv_tripdata?

```sql
SELECT COUNT(*) AS total_records
FROM {{ ref('stg_fhv_tripdata') }};
```


```

---
