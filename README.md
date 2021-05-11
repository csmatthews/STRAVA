# STRAVA
Process STRAVA data for GIS
***CREATE TABLE***

create table XXXX
(edge_uid INTEGER,
activity_type VARCHAR(20),
date DATE,
forward_trip_count DOUBLE PRECISION,
reverse_trip_count DOUBLE PRECISION,
forward_people_count DOUBLE PRECISION,
reverse_people_count DOUBLE PRECISION,
forward_hour_0_trip_count DOUBLE PRECISION,
reverse_hour_0_trip_count DOUBLE PRECISION,
forward_hour_1_trip_count DOUBLE PRECISION,
reverse_hour_1_trip_count DOUBLE PRECISION,
forward_hour_2_trip_count DOUBLE PRECISION,
reverse_hour_2_trip_count DOUBLE PRECISION,
forward_hour_3_trip_count DOUBLE PRECISION,
reverse_hour_3_trip_count DOUBLE PRECISION,
forward_hour_4_trip_count DOUBLE PRECISION,
reverse_hour_4_trip_count DOUBLE PRECISION,
forward_hour_5_trip_count DOUBLE PRECISION,
reverse_hour_5_trip_count DOUBLE PRECISION,
forward_hour_6_trip_count DOUBLE PRECISION,
reverse_hour_6_trip_count DOUBLE PRECISION,
forward_hour_7_trip_count DOUBLE PRECISION,
reverse_hour_7_trip_count DOUBLE PRECISION,
forward_hour_8_trip_count DOUBLE PRECISION,
reverse_hour_8_trip_count DOUBLE PRECISION,
forward_hour_9_trip_count DOUBLE PRECISION,
reverse_hour_9_trip_count DOUBLE PRECISION,
forward_hour_10_trip_count DOUBLE PRECISION,
reverse_hour_10_trip_count DOUBLE PRECISION,
forward_hour_11_trip_count DOUBLE PRECISION,
reverse_hour_11_trip_count DOUBLE PRECISION,
forward_hour_12_trip_count DOUBLE PRECISION,
reverse_hour_12_trip_count DOUBLE PRECISION,
forward_hour_13_trip_count DOUBLE PRECISION,
reverse_hour_13_trip_count DOUBLE PRECISION,
forward_hour_14_trip_count DOUBLE PRECISION,
reverse_hour_14_trip_count DOUBLE PRECISION,
forward_hour_15_trip_count DOUBLE PRECISION,
reverse_hour_15_trip_count DOUBLE PRECISION,
forward_hour_16_trip_count DOUBLE PRECISION,
reverse_hour_16_trip_count DOUBLE PRECISION,
forward_hour_17_trip_count DOUBLE PRECISION,
reverse_hour_17_trip_count DOUBLE PRECISION,
forward_hour_18_trip_count DOUBLE PRECISION,
reverse_hour_18_trip_count DOUBLE PRECISION,
forward_hour_19_trip_count DOUBLE PRECISION,
reverse_hour_19_trip_count DOUBLE PRECISION,
forward_hour_20_trip_count DOUBLE PRECISION,
reverse_hour_20_trip_count DOUBLE PRECISION,
forward_hour_21_trip_count DOUBLE PRECISION,
reverse_hour_21_trip_count DOUBLE PRECISION,
forward_hour_22_trip_count DOUBLE PRECISION,
reverse_hour_22_trip_count DOUBLE PRECISION,
forward_hour_23_trip_count DOUBLE PRECISION,
reverse_hour_23_trip_count DOUBLE PRECISION,
forward_commute_trip_count DOUBLE PRECISION,
reverse_commute_trip_count DOUBLE PRECISION,
forward_leisure_trip_count DOUBLE PRECISION,
reverse_leisure_trip_count DOUBLE PRECISION,
forward_morning_trip_count DOUBLE PRECISION,
reverse_morning_trip_count DOUBLE PRECISION,
forward_evening_trip_count DOUBLE PRECISION,
reverse_evening_trip_count DOUBLE PRECISION,
forward_male_people_count DOUBLE PRECISION,
reverse_male_people_count DOUBLE PRECISION,
forward_female_people_count DOUBLE PRECISION,
reverse_female_people_count DOUBLE PRECISION,
forward_unspecified_people_count DOUBLE PRECISION,
reverse_unspecified_people_count DOUBLE PRECISION,
forward_13_19_people_count DOUBLE PRECISION,
reverse_13_19_people_count DOUBLE PRECISION,
forward_20_34_people_count DOUBLE PRECISION,
reverse_20_34_people_count DOUBLE PRECISION,
forward_35_54_people_count DOUBLE PRECISION,
reverse_35_54_people_count DOUBLE PRECISION,
forward_55_64_people_count DOUBLE PRECISION,
reverse_55_64_people_count DOUBLE PRECISION,
forward_65_plus_people_count DOUBLE PRECISION,
reverse_65_plus_people_count DOUBLE PRECISION,
forward_average_speed DOUBLE PRECISION,
reverse_average_speed DOUBLE PRECISION)


***IMPORT CSV INTO DATABASE***

\copy janmar2020bike FROM 'O:\d-multiyear\d-bikeped\d-STRAVA\d-data\d-2020\all_edges_2020-01-01-2020-03-31_ride\all_edges_2020-01-01-2020-03-31_ride.csv' DELIMITER ',' CSV HEADER;

\copy aprjun2020bike FROM 'O:\d-multiyear\d-bikeped\d-STRAVA\d-data\d-2020\all_edges_2020-04-01-2020-06-30_ride\all_edges_2020-04-01-2020-06-30_ride.csv' DELIMITER ',' CSV HEADER;

\copy julsep2020bike FROM 'O:\d-multiyear\d-bikeped\d-STRAVA\d-data\d-2020\all_edges_2020-07-01-2020-09-30_ride\all_edges_2020-07-01-2020-09-30_ride.csv' DELIMITER ',' CSV HEADER;

\copy octdec2020bike FROM 'O:\d-multiyear\d-bikeped\d-STRAVA\d-data\d-2020\all_edges_2020-10-01-2020-12-31_ride\all_edges_2020-10-01-2020-12-31_ride.csv' DELIMITER ',' CSV HEADER;

\copy janmar2020ped FROM 'O:\d-multiyear\d-bikeped\d-STRAVA\d-data\d-2020\all_edges_2020-01-01-2020-03-31_ped\all_edges_2020-01-01-2020-03-31_ped.csv' DELIMITER ',' CSV HEADER;

\copy aprjun2020ped FROM 'O:\d-multiyear\d-bikeped\d-STRAVA\d-data\d-2020\all_edges_2020-04-01-2020-06-30_ped\all_edges_2020-04-01-2020-06-30_ped.csv' DELIMITER ',' CSV HEADER;

\copy julsep2020ped FROM 'O:\d-multiyear\d-bikeped\d-STRAVA\d-data\d-2020\all_edges_2020-07-01-2020-09-30_ped\all_edges_2020-07-01-2020-09-30_ped.csv' DELIMITER ',' CSV HEADER;

\copy octdec2020ped FROM 'O:\d-multiyear\d-bikeped\d-STRAVA\d-data\d-2020\all_edges_2020-10-01-2020-12-31_ped\all_edges_2020-10-01-2020-12-31_ped.csv' DELIMITER ',' CSV HEADER;


***CREATE MONTHLY TABLE AND GET SUMS***

CREATE TABLE summary2020ped AS 
TABLE summary2020bike 
WITH NO DATA;

INSERT INTO summary2020ped (edge_uid)
SELECT edge_uid
FROM janmar2020ped
GROUP BY edge_uid

create TABLE summary2020ped as
SELECT DISTINCT edge_uid, jansum, febsum, marsum, aprsum, maysum, junsum, julsum, augsum, sepsum, octsum, novsum, decsum
FROM summary2020ped2
ORDER BY edge_uid asc;

create table jansumbike
as (select 
	edge_uid,
	sum (forward_trip_count+reverse_trip_count) as jansumbike
from janmar2020bike
WHERE EXTRACT(MONTH FROM date) = 1
group by edge_uid)

create table aprsumbike
as (select 
	edge_uid,
	sum (forward_trip_count+reverse_trip_count) as bikeaprsum
from aprjun2020bike
WHERE EXTRACT(MONTH FROM date) = 4
group by edge_uid)

create table aprsumbike
as (select 
	edge_uid,
	sum (forward_trip_count+reverse_trip_count) as bikeaprsum
from aprjun2020bike
WHERE EXTRACT(MONTH FROM date) = 4
group by edge_uid)




UPDATE summary2020bike a
SET
    aprsum = c.aprsum
FROM 
    aprsum c
where a.edge_uid = c.edge_uid;




***CONFIRM DATA IN MONTHLY TABLE IS GOOD***

select * from aprrsum
limit 1000




update summary2020bike
set decsum = 0
where decsum is null




select * from summary2020bike
where aprsum is not null
order by apr_sum desc
limit 1000



update summary2020bike
set total = (jansum+febsum+marsum+aprsum+maysum+junsum+julsum+augsum+sepsum+octsum+novsum+decsum)


