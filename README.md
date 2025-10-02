1. What is a subquery?
A subquery is a query inside another query. It is used to fetch results that will be used by the main query.
Example:

SELECT name FROM employees WHERE dept_id = (SELECT id FROM departments WHERE name = 'HR');


2. Difference between subquery and join?

Subquery: Inner query executes first, result is passed to outer query. Often easier to read but can be slower.

Join: Combines rows from multiple tables based on a relationship. Usually more efficient for large datasets.

3. What is a correlated subquery?
A correlated subquery depends on the outer query for its values. It runs once for each row of the outer query.
Example:

SELECT name
FROM employees e
WHERE salary > (SELECT AVG(salary) FROM employees WHERE dept_id = e.dept_id);


4. Can subqueries return multiple rows?
Yes .

If multiple rows are returned, you must use operators like IN, ANY, or ALL.
Example:

SELECT name FROM employees WHERE dept_id IN (SELECT id FROM departments WHERE location = 'New York');


5. How does EXISTS work?

EXISTS checks if a subquery returns at least one row.

If yes → returns TRUE, otherwise FALSE.
Example:

SELECT name FROM employees e
WHERE EXISTS (SELECT 1 FROM departments d WHERE d.id = e.dept_id);


6. How is performance affected by subqueries?

Simple subqueries: Fine for small datasets.

Correlated subqueries: Can be slow, because they execute once per row of outer query.

Joins are often more efficient for large data.

7. What is scalar subquery?
A scalar subquery returns exactly one value (one row, one column).
Example:

SELECT name, (SELECT COUNT(*) FROM employees) AS total_employees
FROM employees;


8. Where can we use subqueries?

In WHERE clause (filtering)

In FROM clause (as a derived table)

In SELECT clause (returning values)

In HAVING clause (filter groups)

9. Can a subquery be in FROM clause?
Yes . That’s called a derived table.
Example:

SELECT dept_id, avg_salary
FROM (SELECT dept_id, AVG(salary) AS avg_salary FROM employees GROUP BY dept_id) AS dept_avg;


10. What is a derived table?
A derived table is a subquery in the FROM clause, treated as a temporary table by the outer query.
