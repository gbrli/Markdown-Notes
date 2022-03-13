# Aggregate Functions

**COUNT** can be used with DISTINCT and LIKE to filter out duplicates. The below will count all books that contain "the".

```
SELECT COUNT(DISTINCT author_lname, author_fname) FROM books;
SELECT title FROM books WHERE title LIKE '%the%';
```

**GROUP BY** groups everything in one row, but it will hide the rows and only display one. COUNT allows to see the total rows hidden in the group.

GROUP BY aggregates data, after than HAVING can be used to sort the data. WHERE only works with data that was not aggregated prior. See second example.

```
SELECT title, author_lname FROM books GROUP BY author_lname;
SELECT author_lname, COUNT(*) FROM books GROUP BY author_lname;

SELECT CONCAT('In ', released_year, ' ', COUNT(*), ' book(s) were released') AS year FROM books GROUP BY released_year;
```

```
SELECT username, 
COUNT(*) AS num_likes 
FROM users 
    INNER JOIN likes 
    ON users.id = likes.user_id 
GROUP  BY likes.user_id 
HAVING num_likes = (SELECT COUNT(*) 
FROM   photos); 
```

**MIN/MAX** return the highest value or the lowest value. Nesting will allow to select more rows.

The third example will return the title and the page number of the book with the highest number of pages.

```
SELECT MIN(released_year) FROM books;
SELECT MAX(pages) FROM books;

SELECT title, pages FROM books WHERE pages = (SELECT Max(pages) FROM books); 

SELECT title, pages FROM books ORDER BY pages ASC LIMIT 1;
SELECT * FROM books ORDER BY pages DESC LIMIT 1;
SELECT * FROM books WHERE pages = (SELECT Min(pages) FROM books); 
```

**GROUP BY** with MIN/MAX can be used to find the longest book written by an author.

```
SELECT
  CONCAT(author_fname, ' ', author_lname) AS author,
  MAX(pages) AS 'longest book'
FROM books
GROUP BY author_lname,
         author_fname;
```

**SUM** of pages written by each author.

```
SELECT author_fname, author_lname, 
SUM(pages) FROM books GROUP BY author_lname, author_fname;
```

**AVERAGE** of stock for each year, and of pages from each author.

```
SELECT released_year, AVG(stock_quantity) FROM books GROUP BY released_year;

SELECT author_fname, author_lname, AVG(pages) FROM books GROUP BY author_lname, author_fname;
```

Find full name of author with the longest book (nested select **SUBQUERY** to use MIN/MAX), or use ORDER BY below:

```
SELECT CONCAT(author_fname, ' ', author_lname) FROM books WHERE pages = (SELECT Max(pages) FROM books);

SELECT CONCAT(author_fname, ' ', author_lname) FROM books ORDER BY pages DESC LIMIT 1;
```
