# FILTERING DATA

`WHERE` - use for filtering with comparison operators such as ` >, <, <=, >=, <>`

Note: the `<>` operator is equivalent to `is not equal to`

```
    SELECT table
    FROM films
    WHERE release_year <= 1990
```

For filtering strings use single quotes:
`WHERE country = 'Japan'`

| WRITTEN ORDER       | ORDER OF EXECUTION: |
| ------------------- | ------------------- |
| SELECT item         | FROM coats          |
| FROM coats          | WHERE color = green |
| WHERE color = green | SELECT item         |
| LIMIT 5;            | LIMIT 5             |

- After fetching the table, the filtering execute next.

## COUNTING WITH FILTER

Counting films that has over 100,000 votes and in Spanish language.

```
SELECT COUNT(num_votes) AS films_over_1ook_votes
FROM films
WHERE language = 'Spanish'
    AND num_votes > 100,000;
```

> ALWAYS REMEMBER THAT INDENTATION IS IMPORTANT IN FILTERING.

## FILTERING MULTIPLE CRITERIA

USING `OR, AND, BETWEEN`

```
SELECT *
from coats
WHERE color='yellow' OR length='short';
```

```
WHERE buttons BETWEEN 1 AND 5
```

- Note that in using `BETWEEN` use AND to declare the values

`OR` - use to satisfy atleast one common

- Example: `WHERE release_year = 1990 OR release_year = 1997`

Combining `AND, OR` - add paranthesis

```
SELECT title
FROM films
WHERE (release_year=1990 OR release_year = 1997)
    AND (certificatio='PG' OR certification='R');
```

USING `BETWEEN, AND` - instead of using <,> use BETWEEN. Example below is using between and, and other filtering AND.

```
SELECT title
FROM films
WHERE release_year
    BETWEEN 1994 AND 2000
    AND country = 'UK'
    AND (language='German' OR language='Spanish');
```

## FILTERING TEXT

- WHERE can also filter text
- filtering text using wildcards is finding a pattern than specific text
- using LIKE, NOT LIKE

### WILDCARDS

- % (percent) - matches zero, one, or many characters
- \_ (underscore) - match SINGLE characters. only one.

> REMEMBER: placing matters in wildcards!

- '%r' - finds string that ends with r
- '\_ \_%' - find a string that has a third character is t, but the first two characters can be anything.
- %s% - find strings that starts with s and ends with s

using LIKE with wildcards:

```
SELECT name
FROM people
WHERE name LIKE 'Ade%;' <- return any string that starts with Ade
```

```
SELECT name
FROM people
WHERE name LIKE 'Ev_;' <- return any string that starts with EV, with only 3 characters.
```

Using NOT LIKE

```
WHERE name NOT LIKE 'Ade%;' <- return any string that DOES NOT starts with Ade.
```

## FILTERING WITH `IN` as alternative to OR

- easier to set numerous OR condition
- allows multiple values IN(var1,var2,...)

```
SELECT title
FROM films
WHERE release_year IN(1970,1930,1940)
    AND duration > 120 -> return film duration more than 2hours.
    AND language IN('Spanish','German'); ->return films released in year 1970,1930,1940 and langauge in spanish, german.
```

## FILTERING WITH DISTINCT

```
SELECT COUNT(DISTINCT title) AS nineties_english_films_for_teens
FROM films
WHERE release_year BETWEEN 1990 AND 1999
    AND language = 'English'
    AND certification IN('G','PG','PG-13');
```

## FILTERING WITH NULL VALUES

`NULL` - is read as missing values and also very common.

- use `NULL` and `NOT NULL` to:
  - identify missing values
  - select missing values
  - exclude missing values

> COUNT(field_name) already exclude in counting the missing values but in COUNT(\*), it counts everything including the null values.

Example:

```
SELECT COUNT(*) AS no_birthdate
FROM people
WHERE birthdate IS NULL; -> counts fields that has no birthday
```

```
SELECT COUNT(name) AS count_birthdate
FROM people
WHERE birthdate IS NOT NULL; -> return a number where birthdate field has a value.
```
