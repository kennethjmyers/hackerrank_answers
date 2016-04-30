# Advanced Select

Everything done in MySQL unless stated otherwise

## The PADS

```
SELECT CONCAT(Name,'(',SUBSTRING(Occupation,1,1),')') AS n
FROM OCCUPATIONS
ORDER BY n
;
SELECT CONCAT('There are total ', COUNT(Occupation), ' ', LOWER(Occupation), 's.') AS c
FROM OCCUPATIONS
GROUP BY Occupation
ORDER BY c, Occupation
;
```

## Occupations

MS SQL Server
```
SELECT Doctor,Professor,Singer,Actor
FROM
(
    SELECT Name,Occupation,ROW_NUMBER() OVER(PARTITION BY Occupation ORDER BY Name) rn
    FROM OCCUPATIONS
) AS source
PIVOT
(
    MAX(Name)
    FOR Occupation IN (Doctor,Professor,Singer,Actor)
) as PVT
;
```
