# Module 1 – Homework

This document contains answers and SQL queries for the Module 1 homework.

---

## Question 1

**What's the version of pip in the python:3.13 image?**

### Command
```bash
docker run --rm python:3.13 pip --version
```

---

## Question 2

**Given the docker-compose.yaml, what is the hostname and port that pgAdmin should use to connect to the Postgres database?**

### Explanation
Inside Docker Compose, services communicate using the service name as hostname and the container port, not the exposed port.

- Postgres service name: `db`
- Postgres container port: `5432`

---

## Question 3

**For the trips in November 2025, how many trips had a trip_distance of less than or equal to 1 mile?**

### SQL Query
```sql
SELECT COUNT(*) 
FROM green_tripdata
WHERE DATE(lpep_pickup_datetime) BETWEEN '2025-11-01' AND '2025-11-30'
  AND trip_distance <= 1;
```

---

## Question 4

**Which was the pick up day with the longest trip distance?**  
*(Only consider trips with trip_distance < 100 miles)*

### SQL Query
```sql
SELECT DATE(lpep_pickup_datetime) AS pickup_day,
       MAX(trip_distance) AS max_distance
FROM green_tripdata
WHERE trip_distance < 100
GROUP BY pickup_day
ORDER BY max_distance DESC
LIMIT 1;
```

---

## Question 5

**Which was the pickup zone with the largest total_amount on November 18th, 2025?**

### SQL Query
```sql
SELECT z."Zone",
       SUM(t.total_amount) AS total_amount_sum
FROM green_tripdata t
JOIN zones z
  ON t.PULocationID = z.LocationID
WHERE DATE(t.lpep_pickup_datetime) = '2025-11-18'
GROUP BY z."Zone"
ORDER BY total_amount_sum DESC
LIMIT 1;
```

---

## Question 6

**For the passengers picked up in the zone named "East Harlem North" in November 2025, which drop-off zone had the largest total tip?**

### SQL Query
```sql
SELECT dz."Zone" AS dropoff_zone,
       SUM(t.tip_amount) AS total_tip
FROM green_tripdata t
JOIN zones pz
  ON t.PULocationID = pz.LocationID
JOIN zones dz
  ON t.DOLocationID = dz.LocationID
WHERE pz."Zone" = 'East Harlem North'
  AND DATE(t.lpep_pickup_datetime) BETWEEN '2025-11-01' AND '2025-11-30'
GROUP BY dropoff_zone
ORDER BY total_tip DESC
LIMIT 1;
```


---

## Question 7

**Which of the following sequences describes the Terraform workflow for:**
- Downloading plugins and setting up backend
- Generating and executing changes
- Removing all resources

### Correct Workflow
```bash
terraform init
terraform apply -auto-approve
terraform destroy
```
