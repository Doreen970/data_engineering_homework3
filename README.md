These are the steps I carried out to complete my project

I first started docker then opened mage-ai. After this I created a pipeline that would have may data. I created the data loader then extracted my data. I then exported the data to Google Cloud using the exporter on Mage

The following are the SQL queries I used:
-- Creating external table referring to gcs path CREATE OR REPLACE EXTERNAL TABLE terraform-demo-409714.ny_taxi.external_green2022_tripdata OPTIONS ( format = 'PARQUET', uris = ['gs://mage-zoomcamp-qaladid-24/greent_data_2022.parquet'] );

-- Creating native bigquery table CREATE TABLE terraform-demo-409714.ny_taxi.native_green2022_tripdata AS SELECT * FROM terraform-demo-409714.ny_taxi.external_green2022_tripdata;

-- Question 1: What is count of records for the 2022 Green Taxi Data?? SELECT COUNT(*) AS record_count FROM terraform-demo-409714.ny_taxi.native_green2022_tripdata;

-- External Table SELECT COUNT(DISTINCT PULocationID) AS distinct_pu_location_ids_external FROM terraform-demo-409714.ny_taxi.external_green2022_tripdata;

-- Native Table SELECT COUNT(DISTINCT PULocationID) AS distinct_pu_location_ids_native FROM terraform-demo-409714.ny_taxi.native_green2022_tripdata;

SELECT COUNT(*) AS zero_fare_records_native  FROM terraform-demo-409714.ny_taxi.external_green2022_tripdata WHERE fare_amount = 0;

SELECT COUNT(*) AS zero_fare_records_native  FROM terraform-demo-409714.ny_taxi.native_green2022_tripdata WHERE fare_amount = 0;

-- Non-partitioned Table SELECT DISTINCT PULocationID FROM terraform-demo-409714.ny_taxi.native_green2022_tripdata WHERE TIMESTAMP_SECONDS(lpep_pickup_datetime) BETWEEN TIMESTAMP('2022-06-01') AND TIMESTAMP('2022-06-30');