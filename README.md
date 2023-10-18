# SQL-Murder-Mystery-by-Knight-Lab
SQL Murder Mystery by Knight Lab: Solve here: https://mystery.knightlab.com/

<kbd>![SQL Murder Mystery](https://github.com/mbellamybb/SQL-Murder-Mystery-by-Knight-Lab/assets/95842597/90c597e6-3d29-4514-8393-dc7528a48d42)<kbd>
## Table of Contents

1. [Scenario](#1-scenario)
2. [ERD - Schema](#2-erd---schema)
3. [Reviewing Crime Scene Report](#3-reviewing-crime-scene-report))
4. [Identifying Witnesses](#4-identifying-witnesses)
5. [Reviewing Witness Interviews](#5-reviewing-witness-interviews)
6. [Finding the killer using details from witness interviews](#6-finding-the-killer-using-details-from-witness-interviews)
7. [Catching the mastermind](#7-catching-the-mastermind)

***
## 1. Scenario

A crime has taken place and the detective needs your help. The detective gave you the crime scene report, but you somehow lost it. You vaguely remember that the crime was a ​murder​ that occurred sometime on ​Jan.15, 2018,​ and that it took place in ​SQL City. Start by retrieving the corresponding crime scene report from the police department’s database.

## 2. ERD - Schema:
<kbd>![Murder Mystery Schema](https://github.com/mbellamybb/SQL-Murder-Mystery-by-Knight-Lab/assets/95842597/21c2695e-c278-48a7-a81a-8abe17ee2236)<kbd>

## 3. Reviewing Crime Scene Report.
	
````sql
	SELECT *
FROM crime_scene_report
WHERE type = ‘murder’ AND date = "20180115" AND city = "SQL City";
````
#### Output:
<kbd>![1 Reviewing Crime Scene Report](https://github.com/mbellamybb/SQL-Murder-Mystery-by-Knight-Lab/assets/95842597/55db185a-a31f-4df9-b8c2-5938182c2808)<kbd>


## 4. Identifying Witnesses

````sql
– 1st witness
SELECT *
FROM person
WHERE address_street_name = 'Northwestern Dr'
ORDER BY address_number DESC
LIMIT 1;
````
#### Output:
<kbd>![2 Identifying Witnesses (1)](https://github.com/mbellamybb/SQL-Murder-Mystery-by-Knight-Lab/assets/95842597/b16557f8-dd88-4a45-9b4a-c2892f84a827)<kbd>

````sql
– 2nd witness 
SELECT *
FROM person
WHERE address_street_name = 'Franklin Ave'
AND name LIKE '%annabel%'
````
#### Output:
<kbd>![2 Identifying Witnesses (2)](https://github.com/mbellamybb/SQL-Murder-Mystery-by-Knight-Lab/assets/95842597/1de53689-28db-4cf5-9cb1-2600f5186825)<kbd>

## 5. Reviewing Witness Interviews

````sql
SELECT *
FROM interview
WHERE person_id IN (14887, 16371);
````
#### Output:
<kbd>![3 Reviewing Witness Interviews](https://github.com/mbellamybb/SQL-Murder-Mystery-by-Knight-Lab/assets/95842597/024067ab-e53a-48db-930f-8f4cbc9bffad)<kbd>

## 6. Finding the killer using details from witness interviews

````sql
SELECT 	person_id,
		person.name
FROM drivers_license as dl
JOIN person
	ON dl.id = person.license_id 
JOIN get_fit_now_member as "member"
	ON person.id = member.person_id
JOIN get_fit_now_check_in as "check_in"
	ON member.id = check_in.membership_id
WHERE check_in_date = "20180109" AND membership_id LIKE "48Z%" AND plate_number LIKE "%H42W%"
````

#### Output:
<kbd>![4 Finding the killer using details from witness interviews](https://github.com/mbellamybb/SQL-Murder-Mystery-by-Knight-Lab/assets/95842597/b3ef65f8-5107-48f3-af2e-d19ac5c29372)<kbd>

## Check Solution:
<kbd>![Solution - Killer](https://github.com/mbellamybb/SQL-Murder-Mystery-by-Knight-Lab/assets/95842597/27ac85af-597e-4703-a2c6-0c04ff4d784f)<kbd>

## 7. Catching the mastermind
### a. Review killer’s interview
````sql
SELECT *
FROM interview
WHERE person_id = "67318";
````
#### Output:
<kbd>![5 a Review killer’s interview ](https://github.com/mbellamybb/SQL-Murder-Mystery-by-Knight-Lab/assets/95842597/63ed3434-4b03-490e-b2c0-753807acf53c)<kbd>

### b. Identify the mastermind

````sql
SELECT 
  person.name, 
  fb.*
FROM 
  drivers_license AS dl
 JOIN person ON dl.id = person.license_id
 JOIN facebook_event_checkin AS fb ON fb.person_id = person.id
WHERE 
  hair_color = 'red'
  AND height >= 65
  AND height <= 67
  AND car_make = 'Tesla'
  AND car_model = 'Model S' 
  AND gender = 'female';
````

#### Output:      

<kbd>![5 b Identify the mastermind](https://github.com/mbellamybb/SQL-Murder-Mystery-by-Knight-Lab/assets/95842597/9274765c-b51a-432e-87c8-8f203da0b762)<kbd>

