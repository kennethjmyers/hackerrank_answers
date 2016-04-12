# Basic Select

## Revising the Select Query 1

```
SELECT *
FROM CITY
WHERE
    (COUNTRYCODE = "USA")
AND
    (POPULATION > 100000);
```

## Revising the Select Query 2

```
SELECT NAME
FROM CITY
WHERE
    (COUNTRYCODE = "USA")
AND
    (POPULATION > 120000);
```

## Select All

```
SELECT *
FROM CITY;
```

## Select by ID

```
SELECT *
FROM CITY
WHERE ID = 1661;
```

## Japanese Cities' Detail

```
SELECT *
FROM CITY
WHERE COUNTRYCODE = "JPN";
```

## Japanese Cities' Name

```
SELECT NAME
FROM CITY
WHERE COUNTRYCODE = 'JPN';
```

## Weather Observation Station 1

```
SELECT CITY, STATE
FROM STATION;
```

## Weather Observation Station 3

```
SELECT DISTINCT CITY
FROM STATION
WHERE ID%2 = 0;
```

## Weather Observation Station 4

```
SELECT
COUNT(CITY)-COUNT(DISTINCT CITY)
FROM STATION;
```

## Weather Observation Station 5

```
SELECT CITY, CHAR_LENGTH(CITY) AS L
FROM STATION
ORDER BY L,CITY
LIMIT 1
;
SELECT CITY, CHAR_LENGTH(CITY) AS L
FROM STATION
ORDER BY L DESC,CITY
LIMIT 1
;
```

## Weather Observation Station 6

```
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[aeiouAEIOU]'
;
```

## Weather Observation Station 7

```
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '[aeiouAEIOU]$'
;
```

## Weather Observation Station 8

```
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[aeiouAEIOU][a-zA-Z ]*[aeiouAEIOU]$'
;
```

## Weather Observation Station 9

```
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[^aeiouAEIOU]'
;
```

## Weather Observation Station 10

```
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '[^aeiouAEIOU]$'
;
```

## Weather Observation Station 11

```
SELECT DISTINCT CITY
FROM STATION
WHERE
    CITY REGEXP '^[^aeiouAEIOU]'
  OR
    CITY REGEXP '[^aeiouAEIOU]$'
;
```

## Weather Observation Station 12

```
SELECT DISTINCT CITY
FROM STATION
WHERE CITY REGEXP '^[^aeiouAEIOU][a-zA-Z ]*[^aeiouAEIOU]$'
;
```

## Higher than 75 marks

```
SELECT Name
FROM STUDENTS
WHERE Marks > 75
ORDER BY SUBSTRING(Name, CHAR_LENGTH(Name)-2,3) ASC, ID ASC
;
```
