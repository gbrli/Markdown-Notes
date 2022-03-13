# String Functions
Strings can be concatenated with **CONCAT**. 

**CONCAT_WS** includes the separator. Note that string index starts at 1, not 0.
```
SELECT CONCAT(title, '-', author_fname, '-', author_lname) FROM books;
SELECT CONCAT_WS(' - ', title, author_fname, author_lname) FROM books;
```
**SUBSTRING** will shorten a string, and it can be nested with CONCAT. 

Both examples will start at the beginning (index 1) and return the first 10 characters of title.
```
SELECT SUBSTRING(title, 1, 10) AS 'short title' FROM books;
SELECT CONCAT(SUBSTRING(title, 1, 10),'...') FROM books;
```
**REPLACE** will replace characters in a string.

The first example will replace all 'e' characters with '3'. 

The second will also shorten it to the first 10 characters.
```
SELECT REPLACE(title, 'e ', '3') FROM books;
SELECT SUBSTRING(REPLACE(title, 'e', '3'), 1, 10) AS 'weird string' FROM books;
```
**REVERSE** reverses a string, the below creates a palindrome by concatenating it with the original string.
```
SELECT CONCAT('woof', REVERSE('woof'));
```
**CHAR_LENGTH** returns an INT.
```
SELECT CONCAT(author_lname, ' is ', CHAR_LENGTH(author_lname), ' characters long' FROM books;
```
**UPPER/LOWER** changes the case.
```
SELECT UPPER(title) FROM books;
```
