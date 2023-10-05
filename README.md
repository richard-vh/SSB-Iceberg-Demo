# SSB-Iceberg-Demo
 

## Prereqs:

SSB Project requires 3 kafka topics ingested via [this](https://github.com/cldr-steven-matison/NiFi-Templates/blob/main/SSBDemo.json) nifi flow, and 3 impala tables of the following schema.

```javascript

-- CREATE DATABASES
-- EACH USER RUNS TO CREATE DATABASES
CREATE DATABASE ${user_id}_airlines;

--
-- TABLES NEEDED FOR THE NIFI LAB
DROP TABLE IF EXISTS ${user_id}_airlines.`routes_nifi_iceberg`;
CREATE TABLE ${user_id}_airlines.`routes_nifi_iceberg` (
  `airline_iata` VARCHAR,
  `airline_icao` VARCHAR,
  `departure_airport_iata` VARCHAR,
  `departure_airport_icao` VARCHAR,
  `arrival_airport_iata` VARCHAR,
  `arrival_airport_icao` VARCHAR,
  `codeshare` BOOLEAN,
  `transfers` BIGINT,
  `planes` ARRAY<VARCHAR>
) STORED AS ICEBERG;

DROP TABLE IF EXISTS ${user_id}_airlines.`airports_nifi_iceberg`;
CREATE TABLE ${user_id}_airlines.`airports_nifi_iceberg` (
  `city_code` VARCHAR,
  `country_code` VARCHAR,
  `name_translations` STRUCT<`en`:string>,
  `time_zone` VARCHAR,
  `flightable` BOOLEAN,
  `coordinates` struct<`lat`:DOUBLE, `lon`:DOUBLE>,
  `name` VARCHAR,
  `code` VARCHAR,
  `iata_type` VARCHAR
) STORED AS ICEBERG;

DROP TABLE IF EXISTS ${user_id}_airlines.`countries_nifi_iceberg`;
CREATE TABLE ${user_id}_airlines.`countries_nifi_iceberg` (
  `name_translations` STRUCT<`en`:VARCHAR>,
  `cases` STRUCT<`su`:VARCHAR>,
  `code` VARCHAR,
  `name` VARCHAR,
  `currency` VARCHAR
) STORED AS ICEBERG;


```

***

## Getting Started

1. Fork this repo and import your repo as a project in Sql Stream Builder
2. Open your Project and have a look around at the left menu. Notice all hover tags. Explore the vast detail in Explorer menus.
3. Import Your Keytab
4. Check out Source Control.  If you created vs import on first screen you may have to press import here still.  You can setup Authentication here.
5. Create and activate an Environment with a key value pair for your userid -> username
6. Inspect/Add Data Sources
7. Inspect/Add Virtual Kafka Tables

***

## Modifications to Jobs

1. CSA_1_11_Iceberg_Sample - Example in CSA 1.11 docs
	* No modifications should be required to this job
2. Countries_Kafka - Select from Kafka Countries, Create IceBerg Table, Insert Results
	* Confirm Kafka topic, ssb_default table names, and namespaces
3. Routes_Kafka - Select from Kafka Routes, Create IceBerg Table, Insert Results
	* Confirm Kafka topic, ssb_default table names, and namespaces
4. Test_Hue_Tables
	* Confirm source iceberg table exists, check table names, and namespaces.

Top Tip:  If you are using different topics w/ different schema, use SSB to get the DDL for topic.  Copy paste into the ssb job's create statement.  Just be careful with complicated schema such as array, struct, etc.

***

## Execution of Jobs:

Warning: These are not full ssb jobs.  In these are samples you execute each statements one at a time.

***

## Evaluating Results:

```javascript
 
SELECT * FROM ${user_id}_airlines.`airports_nifi_iceberg`;
SELECT * FROM ${user_id}_airlines.`countries_nifi_iceberg`;
SELECT * FROM ${user_id}_airlines.`routes_nifi_iceberg`;

SELECT * FROM ${user_id}_airlines.`airports_kafka_iceberg`;
SELECT * FROM ${user_id}_airlines.`countries_kafka_iceberg`;
SELECT * FROM ${user_id}_airlines.`routes_kafka_iceberg`;

```