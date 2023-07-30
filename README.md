# Introduction

### `DENSE_RANK()` function

&#x20;The `DENSE_RANK()` is a window function that assigns ranks to rows in partitions with no gaps in the ranking values. If two or more rows in each partition have the same values, they receive the same rank. The next row has the rank increased by one.

```sql
DENSE_RANK() OVER (
    PARTITION BY expr1[{,expr2...}]
    ORDER BY expr1 [ASC|DESC], [{,expr2...}]
)
```

* First, the `PARTITION BY` clause divides the result set produced by the `FROM` clause into partitions.
* Then, The `ORDER BY` specifies the order of rows in each partition.
* Finally, the `DENSE_RANK(`) function is applied to the rows in the specified order of each partition. It resets the rank when the partition boundary is crossed.

```sql
SELECT
    col,
    DENSE_RANK() OVER (
        ORDER BY col
    ) my_dense_rank,
    RANK() OVER (
        ORDER BY col
    ) my_rank
FROM
    t;
```

![](broken-reference)

The following statement ranks employees in each department by their salaries:

```sql
SELECT 
    first_name, 
    last_name, 
    department_name,
    salary, 
    DENSE_RANK() OVER (
        PARTITION BY department_name
        ORDER BY salary DESC) salary_rank
FROM 
    employees e
    INNER JOIN departments d 
        ON d.department_id = e.department_id;
```

In this example:

* First, the `PARTITION BY` clause divided the employees by department names into partitions.
* Then, the `ORDER BY` clause sorted the employees in each department (partition) by their salaries.
* Finally, the `DENSE_RANK()` function was applied to each partition to assign the rank to rows based on the salary order.

The following picture shows the partial output of the query:

![SQL DENSE\_RANK Function Over Partition example](https://www.sqltutorial.org/wp-content/uploads/2018/09/SQL-DENSE\_RANK-Function-Over-Partition-example.png)

If you want to find only employees who have the highest salary in their departments, you just to use a [subquery](https://www.sqltutorial.org/sql-subquery/) in the `FROM` clause as follows:

```sql
SELECT 
    * 
FROM (
    SELECT 
        first_name, 
        last_name, 
        department_name,
        salary, 
        DENSE_RANK() OVER (
            PARTITION BY department_name
            ORDER BY salary DESC) salary_rank
    FROM 
        employees e
        INNER JOIN departments d 
            ON d.department_id = e.department_id
    ) t
WHERE 
    salary_rank = 1;
```

The following output shows the employees who have the highest salary in their department:

![SQL DENSE\_RANK Function find nth highest value](https://www.sqltutorial.org/wp-content/uploads/2018/09/SQL-DENSE\_RANK-Function-find-nth-highest-value.png)

## `ROW_NUMBER()` Function

The `ROW_NUMBER()` is a [window function](https://www.sqltutorial.org/sql-window-functions/) that assigns a sequential integer number to each row in the query’s result set.

```sql
SELECT 
    ROW_NUMBER() OVER (
            ORDER BY salary
    ) row_num, 
    first_name, 
    last_name, 
    salary
FROM
    employees;
```

The following picture shows the partial result set:

![SQL ROW\_NUMBER Function Example](https://www.sqltutorial.org/wp-content/uploads/2018/09/SQL-ROW\_NUMBER-Function-Example.png)

## &#x20;`PERCENT_RANK()` function

The `PERCENT_RANK()` function returns a percentile ranking number which ranges from zero to one.

For a specific row, `PERCENT_RANK()` uses the following formula to calculate the percentile rank:

(rank - 1) / (total\_rows - 1)

In this formula, `rank` is the rank of the row. `total_rows` is the number of rows that are being evaluated.

```sql
SELECT
    first_name,
    last_name,
    salary,
    ROUND(
        PERCENT_RANK() OVER (
            ORDER BY salary
        ) 
    ,2) percentile_rank
FROM
    employees;
```

The following picture shows the output:
