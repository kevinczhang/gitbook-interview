# Select



## Select

```sql
SELECT DISTINCT
    Name
FROM
    sales.customers
WHERE
    state = 'CA'
ORDER BY
    first_name ASC;
```

### Group

```sql
SELECT
    city,
    COUNT (*)
FROM
    sales.customers
WHERE
    state = 'CA'
GROUP BY
    city
HAVING
    COUNT (*) > 10
ORDER BY
    city DESC;
```

### Offset and fetch

```sql
ORDER BY column_list [ASC |DESC]
OFFSET offset_row_count {ROW | ROWS}
FETCH {FIRST | NEXT} fetch_row_count {ROW | ROWS} ONLY
```

&#x20;To skip the first 10 products and select the next 10 products, you use both `OFFSET` and `FETCH` clauses as follows:

```sql
SELECT
    product_name,
    list_price
FROM
    production.products
ORDER BY
    list_price,
    product_name 
OFFSET 10 ROWS 
FETCH NEXT 10 ROWS ONLY;
```

&#x20;To get the top 10 most expensive products you use both `OFFSET` and `FETCH` clauses:

```sql
SELECT
    product_name,
    list_price
FROM
    production.products
ORDER BY
    list_price DESC,
    product_name 
OFFSET 0 ROWS 
FETCH FIRST 10 ROWS ONLY;
```

### Top

Using `TOP WITH TIES` to include rows that match the values in the last row

```sql
SELECT TOP 3 WITH TIES
    product_name, 
    list_price
FROM
    production.products
ORDER BY 
    list_price DESC;
```

```sql
SELECT TOP 1 PERCENT
    product_name, 
    list_price
FROM
    production.products
ORDER BY 
    list_price DESC;
```

### Where

AND | OR

```sql
SELECT
    product_id,
    product_name,
    category_id,
    model_year,
    list_price
FROM
    production.products
WHERE
    list_price > 300 AND model_year = 2018
ORDER BY
    list_price DESC;
```

Between ... AND

```sql
SELECT
    product_id,
    product_name,
    category_id,
    model_year,
    list_price
FROM
    production.products
WHERE
    list_price BETWEEN 1899.00 AND 1999.99
ORDER BY
    list_price DESC;
```

In

```sql
SELECT
    product_id,
    product_name,
    category_id,
    model_year,
    list_price
FROM
    production.products
WHERE
    list_price IN (299.99, 369.99, 489.99)
ORDER BY
    list_price DESC;
```

LIKE | NOT LIKE

```sql
SELECT
    product_id,
    product_name,
    category_id,
    model_year,
    list_price
FROM
    production.products
WHERE
    product_name LIKE '%Cruiser%'
ORDER BY
    list_price;
```

* The percent wildcard (%): any string of zero or more characters.
* The underscore (\_) wildcard: any single character.
* The \[list of characters] wildcard: any single character within the specified set.
* The \[character-character]: any single character within the specified range.
* The \[^]: any single character not within a list or a range.
