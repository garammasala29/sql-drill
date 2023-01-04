# UNION ALLを使う
`UNION ALL`は2つの`SELECT`を1つにする

`SELECT`する列は同一数・同一型にする必要がある。
```sql
SELECT
  CustomerName AS 氏名
FROM
 Customers
UNION ALL
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
  DepartmentID AS ID
, DepartmentName AS 名前
FROM
  Departments
UNION ALL
SELECT
  CategoryID AS ID
, CategoryName AS 名前
FROM
  Categories
;

SELECT
  'Departments' AS テーブル名
, DepartmentID AS ID
, DepartmentName AS 名前
FROM
  Departments
UNION ALL
SELECT
  'Categories' AS テーブル名
, CategoryID AS ID
, CategoryName AS 名前
FROM
  Categories
ORDER BY
  テーブル名
, ID
;

SELECT
  DepartmentID AS ID
, DepartmentName AS 名前
FROM
  Departments
UNION ALL
SELECT
  CustomerClassID AS ID
, CustomerClassName AS 名前
FROM
  CustomerClasses
UNION ALL
SELECT
  CategoryID AS ID
, CategoryName AS 名前
FROM
  Categories
UNION ALL
SELECT
  ProductID AS ID
, ProductName AS 名前
FROM
  Products
;

SELECT
  'Departments' AS テーブル名
, DepartmentID AS ID
, DepartmentName AS 名前
FROM
  Departments
UNION ALL
SELECT
  'CustomerClasses' AS テーブル名
, CustomerClassID AS ID
, CustomerClassName AS 名前
FROM
  CustomerClasses
UNION ALL
SELECT
  'Categories' AS テーブル名
, CategoryID AS ID
, CategoryName AS 名前
FROM
  Categories
UNION ALL
SELECT
  'Products' AS テーブル名
, ProductID AS ID
, ProductName AS 名前
FROM
  Products
ORDER BY
  テーブル名
, ID
;

SELECT
  s.SaleID
, s.ProductID
, s.Quantity
, c.CustomerClassID
, c.CustomerName
FROM
  Sales AS s
    JOIN
  Customers AS c
    ON
  s.CustomerID = c.CustomerID
WHERE
  c.CustomerClassID = 2
AND
  s.Quantity >= 10
UNION ALL
SELECT
  s.SaleID
, s.ProductID
, s.Quantity
, c.CustomerClassID
, c.CustomerName
FROM
  Sales AS s
    JOIN
  Customers AS c
    ON
  s.CustomerID = c.CustomerID
WHERE
  c.CustomerClassID = 1
AND
  s.Quantity >= 100
;
```
