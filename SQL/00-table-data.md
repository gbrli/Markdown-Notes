# Shirts
```
INSERT INTO shirts(article, color, shirt_size, last_worn) VALUES
('t-shirt', 'white', 'S', 10),
('t-shirt', 'green', 'S', 200),
('polo shirt', 'black', 'M', 10),
('tank top', 'blue', 'S', 50),
('t-shirt', 'pink', 'S', 0),
('polo shirt', 'red', 'M', 5),
('tank top', 'white', 'S', 200),
('tank top', 'blue', 'M', 15);
```
# Cats
```
	1. CREATE TABLE cats 
	2.   ( 
	3.      cat_id INT NOT NULL AUTO_INCREMENT, 
	4.      name   VARCHAR(100), 
	5.      breed  VARCHAR(100), 
	6.      age    INT, 
	7.      PRIMARY KEY (cat_id) 
	8.   ); 

	1. INSERT INTO cats(name, breed, age) 
	2. VALUES ('Ringo', 'Tabby', 4),
	3.        ('Cindy', 'Maine Coon', 10),
	4.        ('Dumbledore', 'Maine Coon', 11),
	5.        ('Egg', 'Persian', 4),
	6.        ('Misty', 'Tabby', 13),
	7.        ('George Michael', 'Ragdoll', 9),
       ('Jackson', 'Sphynx', 7);
```
# Books
```
CREATE TABLE books 
	(
		book_id INT NOT NULL AUTO_INCREMENT,
		title VARCHAR(100),
		author_fname VARCHAR(100),
		author_lname VARCHAR(100),
		released_year INT,
		stock_quantity INT,
		pages INT,
		PRIMARY KEY(book_id)
	);

INSERT INTO books (title, author_fname, author_lname, released_year, stock_quantity, pages)
VALUES
('The Namesake', 'Jhumpa', 'Lahiri', 2003, 32, 291),
('Norse Mythology', 'Neil', 'Gaiman',2016, 43, 304),
('American Gods', 'Neil', 'Gaiman', 2001, 12, 465),
('Interpreter of Maladies', 'Jhumpa', 'Lahiri', 1996, 97, 198),
('A Hologram for the King: A Novel', 'Dave', 'Eggers', 2012, 154, 352),
('The Circle', 'Dave', 'Eggers', 2013, 26, 504),
('The Amazing Adventures of Kavalier & Clay', 'Michael', 'Chabon', 2000, 68, 634),
('Just Kids', 'Patti', 'Smith', 2010, 55, 304),
('A Heartbreaking Work of Staggering Genius', 'Dave', 'Eggers', 2001, 104, 437),
('Coraline', 'Neil', 'Gaiman', 2003, 100, 208),
('What We Talk About When We Talk About Love: Stories', 'Raymond', 'Carver', 1981, 23, 176),
("Where I'm Calling From: Selected Stories", 'Raymond', 'Carver', 1989, 12, 526),
('White Noise', 'Don', 'DeLillo', 1985, 49, 320),
('Cannery Row', 'John', 'Steinbeck', 1945, 95, 181),
('Oblivion: Stories', 'David', 'Foster Wallace', 2004, 172, 329),
('Consider the Lobster', 'David', 'Foster Wallace', 2005, 92, 343);
```
# Customers and Orders
```
	1. CREATE TABLE customers(
	2.     id INT AUTO_INCREMENT PRIMARY KEY,
	3.     first_name VARCHAR(100),
	4.     last_name VARCHAR(100),
	5.     email VARCHAR(100)
	6. );
	7. CREATE TABLE orders(
	8.     id INT AUTO_INCREMENT PRIMARY KEY,
	9.     order_date DATE,
	10.     amount DECIMAL(8,2),
	11.     customer_id INT,
	12.     FOREIGN KEY(customer_id) REFERENCES customers(id)
	13. );

	1. INSERT INTO customers (first_name, last_name, email) 
	2. VALUES ('Boy', 'George', 'george@gmail.com'),
	3.        ('George', 'Michael', 'gm@gmail.com'),
	4.        ('David', 'Bowie', 'david@gmail.com'),
	5.        ('Blue', 'Steele', 'blue@gmail.com'),
	6.        ('Bette', 'Davis', 'bette@aol.com');
	7.        
	8. INSERT INTO orders (order_date, amount, customer_id)
	9. VALUES ('2016/02/10', 99.99, 1),
	10.        ('2017/11/11', 35.50, 1),
	11.        ('2014/12/12', 800.67, 2),
	12.        ('2015/01/03', 12.50, 2),
	13.        ('1999/04/11', 450.25, 5);
```