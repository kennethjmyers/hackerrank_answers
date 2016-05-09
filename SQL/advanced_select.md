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

## [Binary Search Trees](https://www.hackerrank.com/challenges/binary-search-tree-1)

```
SELECT b.N, CASE
            WHEN b.P IS NULL
                THEN 'Root'
            ELSE CASE
                    WHEN (SELECT COUNT(*) FROM BST WHERE P=b.N)>0
                        THEN 'Inner'
                    ELSE 'Leaf'
                    END
            END
FROM BST AS b
ORDER BY b.N;
```

## [Type of Triangle](https://www.hackerrank.com/challenges/what-type-of-triangle)

```
SELECT CASE
       WHEN A+B <= C OR A+C <= B OR C+B <= A THEN 'Not A Triangle'
       WHEN A = B AND B = C THEN 'Equilateral'
       WHEN A = B OR A = C OR B = C THEN 'Isosceles'
       ELSE 'Scalene'
       END AS t
FROM Triangles;
```
