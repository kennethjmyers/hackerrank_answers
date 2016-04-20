# Simply SQL The Sequel

Contest.

## Employee Names

MS SQL Server
```
SELECT name
FROM Employee
ORDER BY name;
```

## Employee Salaries

MS SQL Server
```
SELECT name
FROM Employee
WHERE months < 10 AND salary > 2000
ORDER BY employee_id;
```

## Top Earners

MySQL
```
SELECT a.maxearnings, COUNT(a.maxearnings)
FROM
(
    SELECT employee_id, (months*salary) AS maxearnings
    FROM Employee
) AS a
GROUP BY a.maxearnings
ORDER BY a.maxearnings DESC
LIMIT 1;
```

## New Companies

MySQL
```
SELECT Company.company_code, founder, a,b,c,d
FROM Company
  JOIN (Select company_code,COUNT(DISTINCT lead_manager_code) as a
        From Lead_Manager
        Group By company_code) as l
    ON l.company_code = Company.company_code
  JOIN (Select company_code,COUNT(DISTINCT senior_manager_code) as b
        From Senior_Manager
        Group By company_code) as s
    ON s.company_code = Company.company_code
  JOIN (Select company_code,COUNT(DISTINCT manager_code) as c
        From Manager
        Group By company_code) as m
    ON m.company_code = Company.company_code
  JOIN (Select company_code,COUNT(DISTINCT employee_code) as d
        From Employee
        Group By company_code) as e
    ON e.company_code = Company.company_code
ORDER BY Company.company_code;
```

## Top Competitors

MySQL
```
SELECT Submissions.hacker_id, name
FROM Submissions
  JOIN (SELECT challenge_id, difficulty_level FROM Challenges) AS ch
    ON ch.challenge_id = Submissions.challenge_id
  JOIN (SELECT difficulty_level, score AS max_score FROM Difficulty) AS diff
    ON diff.difficulty_level = ch.difficulty_level
  JOIN (SELECT hacker_id, name FROM Hackers) as n
    ON n.hacker_id = Submissions.hacker_id
WHERE max_score = score
GROUP BY Submissions.hacker_id
HAVING COUNT(Submissions.hacker_id) > 1
ORDER BY COUNT(Submissions.hacker_id) DESC, Submissions.hacker_id ASC
;
```

## Ollivander's Inventory

Oracle
```
SELECT id, age, coins_needed, power
FROM (
    SELECT id, age, coins_needed, power, row_number() OVER(PARTITION BY age,power ORDER BY coins_needed) AS rn
    FROM Wands
      JOIN Wands_Property
      ON Wands.code = Wands_Property.code
    WHERE is_evil = 0
    ORDER BY power DESC, age DESC
    )
WHERE rn = 1
;
```

## Challenges

MySQL
```
SELECT h,name,cnt
FROM
(
    SELECT Hackers.hacker_id as h, name, COUNT(challenge_id) as cnt
    FROM Hackers
    JOIN Challenges
    ON Hackers.hacker_id = Challenges.hacker_id
    GROUP BY h,name
    ORDER BY cnt DESC, h ASC
) as t1
WHERE cnt = (SELECT COUNT(hacker_id) as c2
            FROM Challenges
            GROUP BY hacker_id
            ORDER BY c2 DESC
            LIMIT 1
            )
UNION
SELECT h, name, cnt
FROM
(
    SELECT h,name,cnt,COUNT(cnt) as cntofcnt
    FROM
    (
        SELECT Hackers.hacker_id as h, name, COUNT(challenge_id) as cnt
        FROM Hackers
        JOIN Challenges
        ON Hackers.hacker_id = Challenges.hacker_id
        GROUP BY h,name
        ORDER BY cnt DESC
    ) as t1
    GROUP BY cnt
) as t2
WHERE cnt != (SELECT COUNT(hacker_id) as c2
            FROM Challenges
            GROUP BY hacker_id
            ORDER BY c2 DESC
            LIMIT 1
            )
  AND cntofcnt = 1
ORDER BY cnt DESC,h ASC
;
```

## Contest Leaderboard

MySQL
```
SELECT new_submissions.hacker_id, name, SUM(mscore) AS sscore
FROM Hackers
JOIN
(
    SELECT hacker_id, challenge_id, MAX(score) AS mscore
    FROM Submissions
    GROUP BY hacker_id, challenge_id
) as new_submissions
ON Hackers.hacker_id = new_submissions.hacker_id
GROUP BY hacker_id, name
HAVING sscore > 0
ORDER BY sscore DESC, hacker_id ASC
;
```

## Interviews

MS SQL Server
```
SELECT t3.cid, t3.hacker_id, t3.name, s11,s22,s33,s44
FROM
    (SELECT Contests.contest_id as cid, hacker_id, name, SUM(s1) as s11,SUM(s2) as s22
     FROM Contests
     JOIN
     Colleges
     ON Colleges.contest_id = Contests.contest_id
     JOIN
     Challenges
     ON Colleges.college_id = Challenges.college_id
     JOIN
     (
         SELECT challenge_id, SUM(total_submissions) AS s1,SUM(total_accepted_submissions) AS s2
         FROM Submission_Stats
         GROUP BY challenge_id
     ) AS t1
     ON Challenges.challenge_id = t1.challenge_id
     GROUP BY Contests.contest_id, hacker_id, name) AS t3
JOIN
    (SELECT Contests.contest_id as cid, hacker_id, name, SUM(s3) as s33,SUM(s4) as s44
     FROM Contests
     JOIN
     Colleges
     ON Colleges.contest_id = Contests.contest_id
     JOIN
     Challenges
     ON Colleges.college_id = Challenges.college_id
     JOIN
     (
         SELECT challenge_id, SUM(total_views) AS s3, SUM(total_unique_views) AS s4
         FROM View_Stats
         GROUP BY challenge_id
     ) as t2
     ON Challenges.challenge_id = t2.challenge_id
     GROUP BY Contests.contest_id, hacker_id, name) AS t4
ON t3.cid = t4.cid
WHERE s11 > 0 or s22 > 0 or s33 > 0 or s44 > 0
ORDER BY t3.cid ASC
;
```

## 15 Days of Learning SQL

Oracle
```
SELECT tbl2.sd, cons_counts.fullcc, tbl2.hid, tbl2.n
FROM
(
    SELECT tbl1.submission_date as sd, tbl1.hacker_id as hid, Hackers.name as n
    FROM
    (
        SELECT submission_date,hacker_id,cnt_sub,row_number() OVER(PARTITION BY submission_date order by submission_date, cnt_sub DESC, hacker_id) as rn
        FROM
        (
            SELECT submission_date,hacker_id,cnt_sub
            FROM
            (
                SELECT submission_date, hacker_id, Count(*) as cnt_sub
                FROM Submissions
                GROUP BY submission_date, hacker_id
            )
            ORDER BY submission_date,cnt_sub DESC, hacker_id
        )
    ) tbl1
    JOIN
        Hackers
    ON Hackers.hacker_id = tbl1.hacker_id
    WHERE rn = 1
) tbl2
JOIN
(
    SELECT submission_date, count(*) as fullcc
    FROM
    (
        SELECT submission_date, day, hacker_id, row_number() OVER(PARTITION BY hacker_id ORDER BY submission_date) AS cc
        FROM
        (
            SELECT DISTINCT submission_date, CAST(SUBSTR(submission_date,9,2) AS INT) as day, hacker_id
            FROM Submissions
            ORDER BY submission_date, hacker_id
        )
        ORDER BY Submission_date
    )
    WHERE day = cc
    GROUP BY submission_date
) cons_counts
ON tbl2.sd = cons_counts.submission_date
;
```
