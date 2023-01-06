# INTERSECTを使う
`INTERSECT`は複数の`SELECT`分から共通行を取得する。

基本的には`UNION`と同様、2つの結果をくっつける。
```sql
SELECT
  e.EmployeeName AS 氏名
, s.SaleDate AS 日付
FROM
  Sales AS s
    JOIN
  Employees AS e
    ON s.EmployeeID = e.EmployeeID
INTERSECT
SELECT
  e.EmployeeName AS 氏名
, s.PayDate AS 日付
FROM
  Salary AS s
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
-- 共通行がないので何も表示されない
SELECT
  CustomerID AS ID
, CustomerName AS 名前
FROM
  Customers
INTERSECT
SELECT
  EmployeeID AS ID
, EmployeeName AS 名前
FROM
  Employees
ORDER BY
  ID
;

-- 共通行があるのでUNIONしたときと結果は一緒
SELECT
  EmployeeID AS ID
, EmployeeName AS 名前
FROM
  Employees
INTERSECT
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
INTERSECT
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
INTERSECT
SELECT
  CustomerID
, ProductID
FROM
  Sales
WHERE
  SaleDate BETWEEN '2007-01-01' AND '2007-03-31'
AND
  Quantity >= 10
INTERSECT
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
INTERSECT
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
