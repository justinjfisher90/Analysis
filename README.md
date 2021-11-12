# Analysis
Shootings in United States

Exploring Police shootings from January 2015 to June 2020. The following dataset inbludes 4,895 rows with important fields such as race, body cameras, signs of mental illness, and others. the following sql queries were used to find accurate data using bigquery to answer the following questions:

What weapons did the suspect have?
Which states had the most shootings?
Finding police shootings by race.
If signs of mental illnesses were present.
If bodycams were present on police officers.

-- Getting top 10 armed weapons from database
select armed, COUNT(armed) AS num_of_armed
from `shootings-329516.shootings.shootingslist`
group by armed order by num_of_armed desc
limit 10;

--selecting top 10 states shootings occur
SELECT state, COUNT(state) as states
FROM `shootings-329516.shootings.shootingslist`
group by state order by states desc LIMIT 10

--which race has been shot more by police
select race, COUNT(race) AS num_race_shot
from `shootings-329516.shootings.shootingslist`
group by race;

--Retreiving signs_of_mental_illness count by race
select race,COUNT(id) AS mental_illness_signs_total, COUNT(case when signs_of_mental_illness = true then 1 END) AS mental_illness_true, COUNT(case when signs_of_mental_illness = false then 1 END) AS mental_illness_false
from `shootings-329516.shootings.shootingslist`
group by race;

--checking if bodycam was present
select race, COUNT(id) AS total_shootings, COUNT(case when body_camera = true then 1 end) AS bodycam_present, COUNT(case when body_camera = false then 1 end) AS bodycam_not_present
from `shootings-329516.shootings.shootingslist`
group by race;
