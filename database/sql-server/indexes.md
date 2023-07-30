# Indexes

## Types of indexes

### Clustered index

A clustered index stores data rows in a sorted structure based on its key values. Each table has only one clustered index because data rows can be only sorted in one order. The table that has a clustered index is called a clustered table.

&#x20;A clustered index organizes data using a special structured so-called [B-tree](https://en.wikipedia.org/wiki/B-tree) (or balanced tree) which enables searches, inserts, updates, and deletes in logarithmic amortized time.

&#x20;When you create a table with a [primary key](https://www.sqlservertutorial.net/sql-server-basics/sql-server-primary-key/), SQL Server automatically creates a corresponding clustered index based on columns included in the primary key.

### Non-clustered indexes

If you add a primary key constraint to an existing table that already has a clustered index, SQL Server will enforce the primary key using a non-clustered index.

&#x20;A nonclustered index is a data structure that improves the speed of data retrieval from tables. Unlike a [clustered index](https://www.sqlservertutorial.net/sql-server-indexes/sql-server-clustered-indexes/), a nonclustered index sorts and stores data separately from the data rows in the table. It is a copy of selected columns of data from a table with the links to the associated table. Similar to a clustered index, a nonclustered index uses the B-tree structure to organize its data.

A table may have one or more nonclustered indexes and each non-clustered index may include one or more columns of the table.

Besides storing the index key values, the leaf nodes also store row pointers to the data rows that contain the key values. These row pointers are also known as row locators.

## Clustered and non clustered index

There are mainly two type of indexes in SQL, Clustered index and non clustered index. The differences between these two indexes is very important from SQL performance perspective.

1. One table can have only one clustered index but it can have many non clustered index. (approximately 250).&#x20;
2. clustered index determines how data is stored physically in table. Actually clustered index stores data in cluster, related data is stored together so it makes simple to retrieve data.
3. reading from a clustered index is much faster than reading from non clustered index from the same table.
4. clustered index sort and store data rows in the table or view based on their key value, while non cluster have a structure separate from the data row.

Clustered index alters the table and re-order the way in which the records are stored in the table. Data retrieval is made faster by using the clustered index.

A Non-clustered index does alter the records that are stored in the table but creates a completely different object within the table.

## Unique Index

A unique index ensures the index key columns do not contain any duplicate values. A unique index may consist of one or many columns. If a unique index has one column, the values in this column will be unique. In case the unique index has multiple columns, the combination of values in these columns is unique.

NULL is even not equal to itself. However, when it comes to unique index, SQL Server treats NULL values the same. It means that if you create a unique index on a nullable column, you can only have only one NULL value in this column.

### Unique index vs. `UNIQUE` constraint

&#x20;Both unique index and [`UNIQUE` constraint](https://www.sqlservertutorial.net/sql-server-basics/sql-server-unique-constraint/) enforce the uniqueness of values in one or many columns. SQL Server validates duplicates in the same manner for both unique index and unique constraint.

When you create a unique constraint, behind the scene, SQL Server creates a unique index associated with this constraint.
