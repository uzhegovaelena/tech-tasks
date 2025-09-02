## Task N1
Given a table of candidates and their skills, you're tasked with finding the candidates best suited for an open Data Science job. You want to find candidates who are proficient in Python, Tableau, and PostgreSQL.

Write a query to list the candidates who possess all of the required skills for the job. Sort the output by candidate ID in ascending order.

Assumption:

There are no duplicates in the candidates table.
candidates Table:
Column Name	Type
candidate_id	integer
skill	varchar
candidates Example Input:
candidate_id	skill
- Python
- Tableau
-	PostgreSQL
-	R
-	PowerBI
-	SQL Server
-	Python
-	Tableau

**Example Output:** 

candidate_id

123

**Explanation**

Candidate 123 is displayed because they have Python, Tableau, and PostgreSQL skills. 345 isn't included in the output because they're missing one of the required skills: PostgreSQL.

The dataset you are querying against may have different input & output - this is just an example!

p.s. give the hints below a try if you're stuck and don't know where to start!

**Answers**
1. SELECT candidate_id FROM candidates
WHERE skill IN ('Python', 'Tableau', 'PostgreSQL')
GROUP BY 1
HAVING COUNT(skill) = 3
ORDER BY 1 ASC
2. WITH ds_skills as (
Select UNNEST(ARRAY['Python', 'Tableau', 'PostgreSQL']) as skill
) 

Select c.candidate_id
FROM candidates c
JOIN ds_skills ON c.skill = ds_skills.skill
GROUP BY 1
HAVING COUNT(*) = (SELECT COUNT(*) FROM ds_skills)

Comment: ARRAY['Python','Tableau','PostgreSQL'] = creates an array literal in Postgres.

UNNEST(...) = turns the array into rows:
