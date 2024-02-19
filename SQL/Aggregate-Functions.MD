# SUMMARIZING DATA WITH AGGREGATE FUNCTIONS

- Agreggate - <em>grouping</em>
  - summarize functions.
    - EX: `COUNT(), AVG(), SUM(), MIN(), MAX()`
  - comes after SELECT.
    - EX: `SELECT AVG(budget) AS average_budget`

> Notes:
>
> - IT IS IMPORTANT WHEN USING AGGREGATE FUNCTION TO USE - `AS` - ALIAS. THIS IS TO HAVE A READABLE CODE.
>
> - ALWAYS ENCLOSED THE AGGREGATE FUNCTION TO PARENTHESIS () IF YOU ARE DOING AGGREGATE AND ARITHMETIC.

Function that accepts:
| ONLY Numerical Data | Non-numerical/Various Data types |
| ------ | ---- |
| AVG() | COUNT() |
| SUM() | MIN() , MAX() |
| ROUND() | |

- In MIN(), MAX() also accepts strings
- A (lowest) to Z (highest) - dealing with text
- 1715 (lowest) to current year (highest) - dealing with dates

EXAMPLES of non-numerical:

```
SELECT MIN(country) <- returns a field that starts with A.
FROM films
```

## AGGREGATE AND ARITHMETIC

![Summation](images/image.png)

Difference between arithmetic and aggregate

- Aggregate - adds up records vertically

- Arithmetic - `+, -, *, /`
  - adds up records horizontally
  - EX:
  ```
  SELECT (gross-budget) AS profit
  FROM films;
  ```
  - needs to add decimals if you want to return a float EX: ` SELECT (4.0/3.0)` which returns 1.3333...
  - all default integer/becomes absolute unless decimals are stated.

## ALIAS WHEN SUMMARIZING

- always use `AS` inline with SELECT when summarizing values
- seperate aliases for each function

```
SELECT MAX(budget) AS max_budget
       MAX(duration) AS max_duration
FROM films;
```

> note that aliases used in SELECT cannot be used in WHERE clause due to order of execution.

| ORDER OF EXECUTION              |
| ------------------------------- |
| 1. FROM                         |
| 2. WHERE                        |
| 3. SELECT (INLINE ALIASES HERE) |
| 4. LIMIT                        |

Using `WHERE` with aggregate functions

```
SELECT AVG(budget) AS average_budget
FROM films
WHERE release_year >= 2010;
```

USING `ROUND`

- round a number to a speficied decimal
- SYNTAX: `ROUND(target, decimal_places)`

```
SELECT ROUND(AVG(budget), 2)
FROM films;
```

> returns XXXX.XX 2 decimal places. the code above returned 41072235.18

USING `ROUND` with whole number

- default to zero when no input decimal places `ROUND(target)`

USING `ROUND` with negative

- `ROUND(target, -x)` replaces tenths/hundredths/... to 0
- example: `ROUND(AVG(budget), -5)` returns -> rounds to the 5th place (from right to left), 41072235 will be `41100000`.

### MORE EXAMPLES:

```
SELECT title, (duration/60.0) AS duration_hours
FROM films;
```

- Calculate th percentage of people who are no longer alive

```
SELECT COUNT(deathdate) * 100 / COUNT(*) AS percentage_dead
FROM people
```

- - count all if deathdate is not null
  - (deathdate/total_records) \* 100
  - returns 9.239...%

- find numbers of decades of films produced from starting date to end date

```
SELECT (MAX(released_year)-MIN(released_year))/10.0 AS number_of_decades
```

> ALWAYS ENCLOSED THE AGGREGATE FUNCTION TO PARENTHESIS () IF YOU ARE DOING AGGREGATE AND ARITHMETIC.
