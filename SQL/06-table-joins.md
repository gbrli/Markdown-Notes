# Table Joins

Real world data is messy and interrelated.

**Foreign keys** are used when declaring a table that references an ID on a different table. 

The insert below would fail if there is no customer id no. 98:
```
FOREIGN KEY(customer_id) REFERENCES customers(id) ON DELETE CASCADE;

INSERT INTO orders (order_date, amount, customer_id)
VALUES ('2016/06/06', 33.67, 98);
```

A **CROSS JOIN** will attach two tables together but the data is multiplied into every possible combination, so it has limited use:

```
SELECT * FROM customers, orders;
```

An **IMPLICIT INNER JOIN** will match a parameter and prove more useful:

```
SELECT * FROM customers, orders WHERE customers.id = orders.customer_id;

SELECT first_name, last_name, order_date, amount FROM customers, orders 
WHERE customers.id = orders.customer_id;
```

AN **EXPLICIT INNER JOIN** is the same thing but it uses the JOIN syntax. This is the preferred method:

```
SELECT * FROM orders JOIN customers ON customers.id = orders.customer_id;
```

**LEFT JOIN** selects everything on the left table and whatever matches from the right table.
**RIGHT JOIN** does the opposite. 

```
SELECT first_name
IFNULL(AVG(grade), 0) AS average
FROM students
LEFT JOIN papers
ON students.id = papers.student_id
GROUP BY students.i 
ORDER BY average DESC;
```

**Multiple FOREIGN KEY** references on many-to-many relationships:

```
CREATE TABLE reviews (
id INT AUTO_INCREMENT PRIMARY KEY,
rating DECIMAL(2,1),
series_id INT,
reviewer_id INT,
FOREIGN KEY(series_id) REFERENCES series(id),
FOREIGN KEY(reviewer_id) REFERENCES reviewers(id));
````

**INNER JOINS** can be put in any order. **RIGHT AND LEFT JOINS** will instead invert the data order.

**ROUND** function will round a long decimal number to the digits specified in the second parameter.

```
SELECT genre, 
ROUND(AVG(rating), 2) AS avg_rating 
FROM series
INNER JOIN reviews 
ON series.id = reviews.series_id 
GROUP  BY genre; 
```