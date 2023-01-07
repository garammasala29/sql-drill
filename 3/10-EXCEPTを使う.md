# EXPECTを使う
`EXPECT` = 1つ目の`SELECT` - 2つ目の`SELECT`

重複も削除するので注意
```sql
SELECT
  EmployeeName
FROM
  Employees
EXCEPT
SELECT
  e.EmployeeName
FROM
  Sales AS s
    JOIN
  Employees AS e
    ON s.EmployeeID = e.EmployeeID
;
```

## Railsの場合
```ruby
```
----
```sql
-- Customersテーブルのみと一緒
SELECT
  CustomerID AS ID
, CustomerName AS 氏名
FROM
  Customers
EXCEPT
SELECT
  EmployeeID AS ID
, EmployeeName AS 氏名
FROM
  Employees
ORDER BY
  ID
;

-- 結果は0
SELECT
  EmployeeID AS ID
, EmployeeName AS 名前
FROM
  Employees
EXCEPT
SELECT
  EmployeeID AS ID
, EmployeeName AS 名前
FROM
  Employees
ORDER BY
  ID
;

SELECT
  ProductID
FROM
  Products
EXCEPT
SELECT
  ProductID
FROM
  Sales
ORDER BY
  ProductID
;

-- 重複したCustomerIDとProductIDも削除している
SELECT
  CustomerID
, ProductID
FROM
  Sales
WHERE
  SaleDate BETWEEN '2006-10-01' AND '2006-12-31'
AND
  Quantity >= 10
EXCEPT
SELECT
  CustomerID
, ProductID
FROM
  Sales
WHERE
  SaleDate BETWEEN '2007-01-01' AND '2007-03-31'
AND
  Quantity >= 10
EXCEPT
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
EXCEPT
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
