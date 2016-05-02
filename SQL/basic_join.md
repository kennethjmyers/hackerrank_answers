# Basic Joins

## [Asian Population](https://www.hackerrank.com/challenges/asian-population)

Oracle
```
SELECT sum(CITY.Population)
FROM CITY
  JOIN COUNTRY
    ON CITY.CountryCode = COUNTRY.Code
WHERE COUNTRY.Continent = 'Asia';
```

## [African Cities](https://www.hackerrank.com/challenges/african-cities)

Oracle
```
SELECT CITY.name
FROM CITY
    JOIN COUNTRY
  ON CITY.countrycode = COUNTRY.code
WHERE COUNTRY.continent = 'Africa';
```
