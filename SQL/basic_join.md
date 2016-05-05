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

## [Average Population of Each Continent](https://www.hackerrank.com/challenges/average-population-of-each-continent)

```
SELECT Country.continent, FLOOR(AVG(City.population))
FROM Country
  JOIN City
    ON Country.code = city.countrycode
GROUP BY Country.continent;
```

## [The Report](https://www.hackerrank.com/challenges/the-report)

MySQL (allowed me to see the result whereas Oracle didn't)
```
SELECT * FROM
(
    SELECT students.name, grades.grade, students.marks
    FROM students
    JOIN grades
    ON students.marks >= grades.min_mark and students.marks <= grades.max_mark
    WHERE grades.grade >= 8
    ORDER BY grades.grade desc, students.name asc)a
UNION
SELECT * FROM
(
    SELECT null, grades.grade, students.marks
    FROM students
    JOIN grades
    ON students.marks >= grades.min_mark and students.marks <= grades.max_mark
    WHERE grades.grade < 8
    ORDER BY grades.grade desc, students.marks asc
)b
```
