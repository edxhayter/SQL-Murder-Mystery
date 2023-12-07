# SQL Murder Mystery Solver

Solve the SQL Murder Mystery challenge with this interactive script. Sharpen your SQL skills by analyzing clues and writing queries to unravel the mystery.

## Challenge Overview

The SQL Murder Mystery is an online challenge designed to teach SQL concepts in a fun and engaging way. Check out the challenge [here](https://mystery.knightlab.com/) before diving into this script.

First the goal was to look at the crime report:

<pre>
  SELECT *
  FROM crime_scene_report
  WHERE type = 'murder'
  AND city = 'SQL City'
  AND date = '20180115'
</pre>
  
This revealed two witnesses:
*  Witness 1 lives in the last house on Northwestern Dr.
*  Witness 2's first name is Annabel and they live on Franklin Ave.

Witness 1
<pre>
  SELECT *
  FROM person
  WHERE address_street_name = 'Northwestern Dr'
  ORDER BY address_number desc
  LIMIT 1;
</pre>

Witness 2
<pre>
  SELECT *
  FROM person
  WHERE name like '%Annabel%'
  AND address_street_name = 'Franklin Ave';
</pre>

Witness Details:
| ID | Name | license_id | address_number | address_street_name | ssn |
|----|----- |------------|----------------|---------------------|-----|
| 14887 | Morty Schapiro | 118009 | 4919 | Northwestern Dr | 111564949 |
| 16371	| Annabel Miller | 490173 | 103 | Franklin Ave | 318771143 |

Now we have to find the interview transcripts:

<pre>
  SELECT *
  FROM interview
  WHERE person_id = 14887 
  OR person_id = 16371;
</pre>

Transcripts:
| id | report |
|----|--------|
| 14887 | I heard a gunshot and then saw a man run out. He had a "Get Fit Now Gym" bag. The membership number on the bag started with "48Z". Only gold members have those bags. The man got into a car with a plate that included "H42W". |
| 16371 | I saw the murder happen, and I recognized the killer from my gym when I was working out last week on January the 9th. |

Now I trued to identify the killer:
<pre>
  SELECT *
  FROM get_fit_now_member
  WHERE id like '48Z%'
  AND membership_status = 'gold';
</pre>

Gym Members:
| id | person_id | name | membership_start_date | membership_status |
|----|-----------|------|-----------------------|-------------------|
| 48Z7A	| 28819 | Joe Germuska | 20160305 | gold |
| 48Z55	67318 | Jeremy Bowers | 20160101 | gold |

Demographic Info:
| id | name	| license_id | address_number | address_street_name | ssn |
|----|------|------------|----------------|---------------------|-----|
| 28819 | Joe Germuska | 173289 | 111 | Fisk Rd | 138909730 |
| 67318	| Jeremy Bowers |	423327 | 530 | Washington Pl, Apt 3A | 871539279 |

<pre>
  SELECT *
  FROM drivers_license
  WHERE plate_number like '%H42W%'
  AND id = 173289 OR id = 423327;
</pre>

License Plate Match:
| id | age | height	| eye_color |	hair_color | gender | plate_number | car_make | car_model |
|----|-----|--------|-----------|------------|--------|--------------|----------|-----------|
| 183779 | 21	| 65	| blue | blonde	| female | H42W0X | Toyota | Prius |
| 423327 | 30	| 70	| brown | brown | male | 0H42W2 | Chevrolet | Spark LS |
| 664760 | 21 | 71	| black	| black | male | 4H42WR	| Nissan | Altima |

Jeremy Bowers matches the reports as the killer.

Finding the Mastermind:
<pre>
  SELECT *
  FROM interview
  WHERE person_id = 67318;
</pre>

Report:
-- I was hired by a woman with a lot of money. I don't know her name but I know she's around 5'5" (65") or 5'7" (67"). She has red hair and she drives a Tesla Model S. I know that she attended the SQL Symphony Concert 3 times in December 2017. 



