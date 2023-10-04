# SSB-Iceberg-Demo
 

## Prereqs:

SSB Project requires 3 kafka topics, and 3 impala tables which are not part of this repo.  Please see upstream documenation for details.

***

## Import this github repository as a Project into Sql Stream Builder.   

1. Open Project
2. Import Keytab
3. Inspect/Add Data Sources
4. Inspect/Add Virtual Kafka Tables

***

## Modify Jobs

1. CSA_1_11_Iceberg_Sample - Example in CSA 1.11 docs
2. Countries_Kafka - Select from Kafka Countries, Create IceBerg Table, Insert Results
3. Routes_Kafka - Select from Kafka Routes, Create IceBerg Table, Insert Results
4. Test_Hue_Tables

***

## Execution of Jobs:

Warning: These are not full ssb jobs.  In these are samples you execute each statements one at a time.

***

## Evaluating Results: