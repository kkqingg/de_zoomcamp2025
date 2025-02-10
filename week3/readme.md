1 #Count of records for the 2024 Yellow Taxi Data\
-- SELECTING COUNTS FROM TOTAL RECORDS--\
SELECT COUNT (*) AS total_records FROM `kestra-data-zc.2025_taxi_homework.2025_taxi_hw` LIMIT 1000\
\
--2. Creating external table\
CREATE EXTERNAL TABLE `kestra-data-zc.2025_taxi_homework.yellow_taxi_external`\
OPTIONS (\
  format = 'PARQUET',\
  uris = ['gs://2024_taxi_assignment_1/yellow_tripdata_2024-*.parquet']\
);\
\
--3.Distinct Counts FROM PULocation ID--\
SELECT COUNT(DISTINCT PULocationID) as distinct_counts \
FROM `kestra-data-zc.2025_taxi_homework.2025_taxi_hw` \
-- FROM 'kestra-data-zc.2025_taxi_homework.2025_taxi_hw'\
\
SELECT COUNT(DISTINCT PULocationID) as distinct_counts \
FROM `kestra-data-zc.2025_taxi_homework.yellow_taxi_external` \
-- FROM 'kestra-data-zc.2025_taxi_homework.yellow_taxi_external'\
\
--4. PULocationID and DOLocationID--\
SELECT PULocationID as PULocationID \
FROM `kestra-data-zc.2025_taxi_homework.2025_taxi_hw` \
\
SELECT PULocationID as PULocationID, DOLocationID as DOLocationID \
FROM `kestra-data-zc.2025_taxi_homework.2025_taxi_hw` \
\
-- 5. Fare Amount zero--\
SELECT COUNT (*) as fare_zero\
FROM `kestra-data-zc.2025_taxi_homework.2025_taxi_hw`\
WHERE fare_amount = 0; \
\
-- 6. Create a partioned Clustered table--\
CREATE OR REPLACE TABLE `kestra-data-zc.2025_taxi_homework.partationed_clustered_table`\
PARTITION BY DATE(tpep_dropoff_datetime)\
CLUSTER BY VendorID AS\
SELECT * FROM `kestra-data-zc.2025_taxi_homework.2025_taxi_hw`\
\
-- 7. File Size on original table VS partioned Clustered table  --\
SELECT DISTINCT (VendorID) as distinct_vendorID\
FROM `kestra-data-zc.2025_taxi_homework.2025_taxi_hw` \
WHERE DATE (tpep_dropoff_datetime) BETWEEN "2024-03-01" and "2024-03-15";\
\
SELECT DISTINCT (VendorID) as distinct_vendorID\
FROM `kestra-data-zc.2025_taxi_homework.partationed_clustered_table` \
WHERE DATE (tpep_dropoff_datetime) BETWEEN "2024-03-01" and "2024-03-15";\
