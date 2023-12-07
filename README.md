# SQL Murder Mystery Solver

Solve the SQL Murder Mystery challenge with this interactive script. Sharpen your SQL skills by analyzing clues and writing queries to unravel the mystery.

## Challenge Overview

The SQL Murder Mystery is an online challenge designed to teach SQL concepts in a fun and engaging way. Check out the challenge [here](https://mystery.knightlab.com/) before diving into this script.

First the goal was to look at the crime report:

<pre>
\```sql
SELECT *
FROM crime_scene_report
WHERE type = 'murder'
AND city = 'SQL City'
AND date = '20180115'
\```
</pre>
  
This revealed two witnesses:
Witness 1 lives in the last house on Northwestern Dr.
Witness 2's first name is Annabel and they live on Franklin Ave.
