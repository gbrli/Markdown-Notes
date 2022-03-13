# Logical Operators

**WHERE** can be used with logical operators to refine search.

```
SELECT title FROM books WHERE released_year != 2017;
SELECT title FROM books WHERE title LIKE 'W%'; 
SELECT title FROM books WHERE title NOT LIKE 'W%';
```

Characters are in order. Z is greater than A, but a is equal to A.

```
SELECT title, released_year FROM books WHERE released_year >= 2000 ORDER BY released_year;

SELECT 'h' < 'p'; SELECT 'Q' <= 'q'; BOTH TRUE

SELECT title, author_lname, released_year FROM books WHERE author_lname='Eggers' AND released_year > 2010;
```

**BETWEEN** and **NOT BETWEEN**

```
SELECT title, released_year FROM books WHERE released_year BETWEEN 2004 AND 2015;

SELECT title, released_year FROM books WHERE released_year NOT BETWEEN 2004 AND 2015;
```

Use **CAST** when working with dates to ensure it is converted to the right data type.

```
SELECT name, birthdt
FROM people WHERE birthdt BETWEEN 
CAST('1980-01-01' AS DATETIME) AND 
CAST('2000-01-01' AS DATETIME);
```

**IN** and **NOT IN** should be used instead of having multiple AND/OR clauses. The second example should be corrected with the third, using the modulo operator instead of NOT IN.

```SELECT title, released_year FROM books WHERE released_year IN (2017, 1985);
SELECT title, author_lname FROM books WHERE author_lname IN ('Chabon', 'Eggers');

SELECT title, released_year FROM books WHERE released_year NOT IN (2000,2002,2004,2006,2008,2010,2012,2014,2016);

SELECT title, released_year FROM books WHERE released_year >= 2000 AND released_year % 2 != 0 ORDER BY released_year;
```

**IF** statements work with one condition to be met.

```
IF (count(rating) >= 1,
'Active',
'Inactive')
```

**CASE** statements work with multiple conditions to be met.

```
SELECT title, stock_quantity,
    CASE
        WHEN stock_quantity BETWEEN 0 AND 50 THEN '*'
        WHEN stock_quantity BETWEEN 51 AND 100 THEN '**'
        WHEN stock_quantity BETWEEN 101 AND 150 THEN '***'
        ELSE '****'
    END AS STOCK
FROM books;

SELECT title, author_lname,
    CASE
        WHEN COUNT(*)=1 THEN '1 book'
        ELSE concat(count(*),' books')
    END AS COUNT
FROM books GROUP BY author_lname, author_fname;
