# Department highest salary

```sql
-- Solution 1
Select d.Name as Department, e3.Name as Employee, e3.Salary from Department d
INNER JOIN (
    Select e1.DepartmentId, e1.Name, e1.Salary from Employee e1
    INNER JOIN (
        Select DepartmentId, MAX(Salary) as Salary from Employee
        Group By DepartmentId
    ) e2 ON e1.Salary = e2.Salary AND e1.DepartmentId = e2.DepartmentId
) e3 ON d.Id = e3.DepartmentId;


-- Solution 2
SELECT 
    Department, Employee, Salary 
FROM (
    SELECT
        d.Name as Department,
        e.Name as Employee,
        e.Salary, 
        DENSE_RANK() OVER (
            PARTITION BY d.Id
            ORDER BY e.Salary DESC) salary_rank
    FROM 
        Employee e
        INNER JOIN Department d 
            ON d.Id = e.DepartmentId
    ) t
WHERE 
    salary_rank = 1;
```
