# SSB-Iceberg-Demo
 

## Prereqs:

SSB Project requires 3 kafka topics, and 3 impala tables.

```javascript

hue dll create

```

***

## Getting Started

1. Fork this repo and import your repo as a project in Sql Stream Builder
2. Open your Project and have a look around at the left menu and explorer
3. Import Your Keytab
4. Check out Source Control.  If you created vs import on first screen you may have to press import here still.
5. Inspect/Add Data Sources
6. Inspect/Add Virtual Kafka Tables
7. Create an activate an Environment variable userid with your username

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

***

## Execution of Jobs:

Warning: These are not full ssb jobs.  In these are samples you execute each statements one at a time.

***

## Evaluating Results:

```javascript
 
hue dll select

```