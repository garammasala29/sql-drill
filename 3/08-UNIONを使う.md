# UNIONを使う
`UNION ALL`と違って`UNION`は重複を排除する

```sql
SELECT
  CustomerName AS 氏名
FROM
  Customers
UNION
SELECT
  EmployeeName AS 氏名
FROM
 Employees
;
```

## Railsの場合
```ruby
```
----
```sql
SELECT
  CustomerID AS ID
, CustomerName AS 氏名
FROM
  Customers
UNION
SELECT
  EmployeeID AS ID
, EmployeeName AS 氏名
FROM
  Employees
ORDER BY
  ID
;

-- UNIONする意味がない
SELECT
  EmployeeID AS ID
, EmployeeName AS 氏名
FROM
  Employees
UNION
SELECT
  EmployeeID AS ID
, EmployeeName AS 氏名
FROM
  Employees
ORDER BY
  ID
;

-- こちらもUNIONする意味がない
SELECT
  ProductID
FROM
  Products
UNION
SELECT
  ProductID
FROM
  Sales
ORDER BY
  ProductID
;

SELECT
  CustomerID
, ProductID
FROM
  Sales
WHERE
  SaleDate BETWEEN '2006-10-01' AND '2006-12-31'
AND
  Quantity >= 10
UNION
SELECT
  CustomerID
, ProductID
FROM
  Sales
WHERE
  SaleDate BETWEEN '2007-01-01' AND '2007-03-31'
AND
  Quantity >= 10
UNION
SELECT
  CustomerID
, ProductID
FROM
  Sales
WHERE
  SaleDate BETWEEN '2007-04-01' AND '2007-06-30'
AND
  Quantity >= 10
ORDER BY
  CustomerID
, ProductID
;

SELECT
  ProductID
FROM
  Sales AS s
    JOIN
  Customers AS c
    ON s.CustomerID = c.CustomerID
WHERE
  c.CustomerClassID = 2
AND
  s.Quantity >= 10
UNION
SELECT
  ProductID
FROM
  Sales AS s
    JOIN
  Customers AS c
    ON s.CustomerID = c.CustomerID
WHERE
  c.CustomerClassID = 1
AND
  s.Quantity >= 100
;
```
