# SELECTING DATA

## How to Execute a Query, count and view specific records

## USING COUNT()

1. Count() - return number of records with value.

   ```SQL
   SELECT COUNT(target) AS alias_variable
   FROM tablename;
   ```

   Note: Using `AS` for aliases.

2. Counting multiple fields
   ```SQL
   SELECT COUNT(name) AS count_name, COUNT(birthday) AS count_birthday
   FROM people;
   ```
3. Counting all field
   ```SQL
   SELECT COUNT(*) AS total_records
   FROM people;
   ```

## Using DISTINCT

Select unique values and return fields that exclude the duplicate

```SQL
    SELECT DISTINCT target AS alias_variable
    FROM tablename;
```

Using DISTINCT WITH COUNT

```SQL
    SELECT COUNT(DISTINCT birthday) AS count_birthdates
    FROM PEOPLE;
```

- From the code above: It count all the unique birthdates but doesnt all the duplicates.
- COUNT - includes counting the duplicate
- DISTINCT - exclude counting the duplicates / return all the unique values

## Query Execution / Order of Execution

> SQL is not processed in order it is written.

- `SELECT name` this line will execute NEXT, it tells which field is to look up
- `FROM people` this line will execute FIRST, to fetch the data from the table
- `LIMIT 10;` this line will execute LAST, to refine the step.

Notes:

- `LIMIT` - limit how many record to return. This is also a best practice for faster query.
- it is good to know how the query execute for debugging purposes.
- `AS` are declared in line of `SELECT` statement. EX: `SELECT COUNT(name) AS total_name`

### DEBUGGING SQL - Most common mistake

- KEYWORDS and FIELDS ERRORS - mispelling, incorrect capitalization
- COMMA ERRORS - missing comma.

### SQL FORMATTING BEST PRACTICES

> format is not required but formatting encourages:
>
> - easy collaboration
> - Clean and readable code
> - easier to debug
>
> BEST PRACTICES: Holyhell's guide -> link: [sqlstyle.guide](sqlstyle.guide)
>
> - Capitalize KEYWORDS
> - underscore in field_names
> - END QUERIES WITH SEMICOLON ; <em>this is important to know where the query ends.</em>

#### DEALING WITH NON-STANDARD FIELD NAMES

- field names should have underscore as alternative to space but: if dealing with non-standard field names, put it into double quotes.

```SQL
 SELECT title, "release year", country
 FROM films;
```
