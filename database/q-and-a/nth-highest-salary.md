# Nth highest salary

```sql
CREATE FUNCTION getNthHighestSalary(@N INT) RETURNS INT AS
BEGIN
    RETURN (
        select isnull(
        (select Salary
            from (
            select distinct Salary, 
                dense_rank()over(order by Salary desc) as DENSERANK
            from Employee
        ) result
        where result.DENSERANK = @N), null) as SecondHighestSalary        
    );
END
```
