#----------------------------------\
This is the readme file for Week 2 Homework.\
#---------------------------------
\
For checking the file size of Yellow Taxi data for the year 2020 and month 12, it was proceeded from the details section of the big query for yellow_tripdata_2020-12.csv file.\
In the GCP big query, yellow and green trip data for 2020 all months are extracted and merged, then the following checking is done for counting the rows for the desired questions.

#-------------------------------------------------------------\
SELECT COUNT(*) AS total_rows
FROM `kestra-data-zc.zoomcamp.yellow_tripdata`
WHERE filename LIKE 'yellow_tripdata_2020%';

SELECT COUNT(*) AS total_rows1
FROM `kestra-data-zc.zoomcamp.green_tripdata`
WHERE filename LIKE 'green_tripdata_2020%';

SELECT COUNT(*) AS total_rows2
FROM `kestra-data-zc.zoomcamp.yellow_tripdata`
WHERE filename LIKE 'yellow_tripdata_2021-03%';

#-------------------------------------------------------------\
For changing the time zone, 
timezone property is added as America/New_York in the Schedule trigger configuration.

...................................................................................
