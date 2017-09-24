sudo systemctl start cassandra
sudo systemctl stop cassandra

sudo service cassandra start
sudo service cassandra stop

nodetool status

cqlsh


CREATE KEYSPACE tutorial WITH replication = {'class':'SimpleStrategy', 'replication_factor' : 2};

USE tutorial;

CREATE TABLE temperature_by_day (weatherstation_id text, event_date date, event_time timestamp, temperature text, ref_id text, PRIMARY KEY ((weatherstation_id,event_date),event_time));

CREATE INDEX refidIndex ON temperature_by_day(ref_id);

INSERT INTO temperature_by_day(weatherstation_id,event_date,event_time,temperature, ref_id) VALUES ('1234ABCD','2013-04-03','2013-04-03 07:01:00','72F', 'A12345678');
INSERT INTO temperature_by_day(weatherstation_id,event_date,event_time,temperature, ref_id) VALUES ('1234ABCD','2013-04-03','2013-04-03 07:02:00','73F', 'B12345678');
INSERT INTO temperature_by_day(weatherstation_id,event_date,event_time,temperature, ref_id) VALUES ('1234ABCD','2013-04-04','2013-04-04 07:01:00','73F', 'C12345678');
INSERT INTO temperature_by_day(weatherstation_id,event_date,event_time,temperature, ref_id) VALUES ('1234ABCD','2013-04-04','2013-04-04 07:02:00','74F', 'D12345678');
INSERT INTO temperature_by_day(weatherstation_id,event_date,event_time,temperature, ref_id) VALUES ('1234ABCD','2013-04-04','2013-04-04 07:02:00','79F', 'D12345678');

INSERT INTO temperature_by_day JSON '{"weatherstation_id":"1234ABCD","event_date":"2013-04-04","event_time":"2013-04-04 07:02:00","temperature":"79F", "ref_id":"E12345678" }';

SELECT * FROM temperature_by_day WHERE weatherstation_id='1234ABCD' AND event_date='2013-04-03';
SELECT * FROM temperature_by_day WHERE weatherstation_id='1234ABCD' AND event_date>='2013-04-03';

DROP TABLE temperature_by_day;



