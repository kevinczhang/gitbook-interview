# SQL Server

## CAST()

The CAST() function converts a value (of any type) into a specified datatype.

CAST(expression AS datatype(length))

#### Parameter Values

| Value      | Description                                                                                                                                                                                                                                                              |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| expression | Required. The value to convert                                                                                                                                                                                                                                           |
| datatype   | Required. The datatype to convert _expression_ to. Can be one of the following: bigint, int, smallint, tinyint, bit, decimal, numeric, money, smallmoney, float, real, datetime, smalldatetime, char, varchar, text, nchar, nvarchar, ntext, binary, varbinary, or image |
| _(length)_ | Optional. The length of the resulting data type (for char, varchar, nchar, nvarchar, binary and varbinary)                                                                                                                                                               |

```sql
SELECT CAST(25.65 AS varchar);
```

## COALESCE()

The COALESCE() function returns the first non-null value in a list.

```sql
SELECT COALESCE(NULL, 1, 2, 'W3Schools.com');
```

## IIF()

The IIF() function returns a value if a condition is TRUE, or another value if a condition is FALSE.

&#x20;IIF(_condition_, _value\_if\_true_, _value\_if\_false_)

```sql
SELECT IIF(500<1000, 5, 10);
```

## ISNULL()

The ISNULL() function returns a specified value if the expression is NULL.

If the expression is NOT NULL, this function returns the expression.

```sql
SELECT ISNULL(NULL, 'W3Schools.com');
```

## ISNUMERIC()

The ISNUMERIC() function tests whether an expression is numeric.

This function returns 1 if the expression is numeric, otherwise it returns 0.

```sql
SELECT ISNUMERIC('4567');
```

## NULLIF() Function

The NULLIF() function returns NULL if two expressions are equal, otherwise it returns the first expression.

```sql
SELECT NULLIF('Hello', 'Hello');
```

## `DECODE`()

&#x20;The SQL `DECODE()` function allows you to add procedure if-then-else logic to [queries](https://www.sqltutorial.org/sql-select/). Let’s see the following example:

```sql
SELECT DECODE(3,1, 'Equal 1,', 2, 'Equal 2', 'Not Equal 1 or 2');
```

This example works like the following IF-THEN-ELSEIF-ELSE statement:

```sql
IF 3 = 1 THEN 
    RETURN 'Equal 1';
ELSE IF 3 =2 THEN
    RETURN 'Equal 2';
ELSE
    RETURN 'Not Equal 1 or 2';
END IF;
```

## CASE

```sql
CASE expression
WHEN when_expression_1 THEN
    result_1
WHEN when_expression_2 THEN
    result_2
WHEN when_expression_3 THEN
    result_3
...
ELSE
    else_result
END
```

```sql
SELECT 
    first_name,
    last_name,
    hire_date,
    CASE (2000 - YEAR(hire_date))
        WHEN 1 THEN '1 year'
        WHEN 3 THEN '3 years'
        WHEN 5 THEN '5 years'
        WHEN 10 THEN '10 years'
        WHEN 15 THEN '15 years'
        WHEN 20 THEN '20 years'
        WHEN 25 THEN '25 years'
        WHEN 30 THEN '30 years'
    END aniversary
FROM
    employees
ORDER BY first_name;
```
