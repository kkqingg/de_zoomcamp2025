# de_zoomcamp2025

docker run -it -entrypoint bash python python:3.12.8
pip --version
#---------------------------------------------------------
## For Question 3
Select 
CAST(lpep_pickup_datetime AS DATE) as "Pu_date",
CAST(lpep_dropoff_datetime AS DATE) as "Do_date",
trip_distance

from green_trip_data 
where
CAST(lpep_pickup_datetime AS DATE)>='2019-10-01'and 
CAST(lpep_dropoff_datetime AS DATE)<'2019-11-01' and 
trip_distance <=1;
#---------------------------------------------------------
Select 
CAST(lpep_pickup_datetime AS DATE) as "Pu_date",
CAST(lpep_dropoff_datetime AS DATE) as "Do_date",
trip_distance

from green_trip_data 
where
CAST(lpep_pickup_datetime AS DATE)>='2019-10-01'and 
CAST(lpep_dropoff_datetime AS DATE)<'2019-11-01' and 
trip_distance >7 and 
trip_distance <=10;
#---------------------------------------------------------
## For Question 4
Select 
CAST(lpep_pickup_datetime AS DATE) as "Pu_date",
COUNT(1) as trip_count,
MAX(trip_distance) as max_trip_dis

from green_trip_data 
GROUP BY CAST(lpep_pickup_datetime AS DATE)
ORDER BY "max_trip_dis";

#---------------------------------------------------------
## For Question 6
SELECT
    CAST(lpep_dropoff_datetime AS DATE) AS "day",
    "DOLocationID",
	MAX(tip_amount) AS "tip_amount",
    COUNT(1) AS "count",
	CONCAT(zpu."Zone") AS "pickup_loc",
	CONCAT(zdo."Borough", ' | ', zdo."Zone") AS "dropff_loc",
    MAX(total_amount) AS "total_amount"
    	
FROM 
    green_trip_data t
JOIN
	taxi_zones zpu ON t."PULocationID" = zpu."LocationID"
JOIN
	taxi_zones zdo ON t."DOLocationID" = zdo."LocationID"
WHERE
	CAST(lpep_dropoff_datetime AS DATE) >= '2019-10-01' AND
	CAST(lpep_dropoff_datetime AS DATE) < '2019-10-31' AND
	zpu."Zone" = 'East Harlem North'
	
GROUP BY
    CAST(lpep_dropoff_datetime AS DATE),
	"DOLocationID",
	zpu."Borough",
    zpu."Zone",
	zdo."Borough",
    zdo."Zone"
ORDER BY
	"tip_amount" DESC,
    "day" ASC
