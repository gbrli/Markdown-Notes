# Read
**SELECT** will return data selected from a table, meaning it will read data. 

**WHERE** gives SELECT a parameter to filter by.

**AS** will provide an alias for the table.

None of the above will modify the original table as they are only reading.
```
SELECT * FROM cats;
SELECT age, breed, name, cat_id FROM cats; 
SELECT cat_id, name, age, breed FROM cats; 

SELECT * FROM cats WHERE age=4; 
SELECT age, name FROM cats WHERE breed='Tabby'; 
SELECT * FROM cats WHERE age=4; 

SELECT cat_id AS id, name FROM cats;
SELECT name AS 'cat name', breed AS 'kitty breed' FROM cats;
```
**DISTINCT** filters out duplicates.
```
SELECT DISTINCT author_lname FROM books;
SELECT DISTINCT CONCAT(author_fname,' ', author_lname) FROM books;
SELECT DISTINCT author_fname, author_lname FROM books;
```
**ORDER BY** sorts data ASC or DESC, can take multiple parameters, or a number to specify the column to sort by, but it's harder to keep track of.
```
SELECT released_year FROM books ORDER BY released_year ASC;
SELECT title, author_fname, author_lname FROM books ORDER BY 1 DESC;
```
**LIMIT** is used with ORDER BY often. It limits what is returned:
3 gives 3 rows. 3,5 gives 5 rows starting from row 3. Large number is all rows (from SQL docs).
```
SELECT * FROM books LIMIT 3;
SELECT title FROM books LIMIT 3,5;
SELECT * FROM tbl LIMIT 95,18446744073709551615;
```
**LIKE** is used with WHERE and uses wildcards '%' for chars and underscores '____'  for char length:
So (235)234-0987 would use LIKE '(___)___-____'. Regex should be implemented here.
Most search functions on websites implement LIKE.
```
SELECT title, author_fname FROM books WHERE author_fname LIKE 'da%';
SELECT title FROM books WHERE title LIKE '%the%';
SELECT title FROM books WHERE title LIKE '___';
```
# Update
**UPDATE** should be used exclusively with SELECT first to make sure the data is selected correctly. It will modify the original table. The example below will turn all tabby kitties to 12-year old shorthairs.
```
SELECT * FROM cats WHERE breed='Tabby';
UPDATE cats SET breed='Shorthair', age=12 WHERE breed='Tabby'; 
SELECT * FROM cats WHERE breed='Shorthair';
```
# Delete
**DELETE** will remove data permanently from a table, until all entries are removed and the table remains empty.
```
DELETE FROM cats WHERE age=4;
DELETE FROM cats;
```