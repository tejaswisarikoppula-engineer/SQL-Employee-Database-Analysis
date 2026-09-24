Employees above average salary
SELECT *
FROM employee
WHERE salary >
(
    SELECT AVG(salary)
    FROM employee
);

Second highest salar
SELECT *
FROM employee
WHERE salary =
(
    SELECT MAX(salary)
    FROM employee
    WHERE salary <
    (
        SELECT MAX(salary)
        FROM employee
    )
);

Highest salary by department
SELECT *
FROM
(
    SELECT
        e.*,
        ROW_NUMBER() OVER
        (
            PARTITION BY dept_name
            ORDER BY salary DESC
        ) AS rn
    FROM employee e
) x
WHERE rn = 1;
