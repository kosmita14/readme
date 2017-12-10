
#run influxdb CLI:
docker exec -it influxdb influx

influx -format=column
influx -format=csv
influx -format=json
influx -format=json -pretty


#show all databases
show databases

#use given database
USE telegraf

#show all measurements in the database
SHOW measurements

#create database
create database ekd_metrics;

#select data from measurement
select * from mem limit 3;


