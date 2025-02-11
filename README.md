# Solutions-to-the-SQL-Assignment


## Basic SELECT Queries
1. **Retrieve all customers**
```Python
SELECT * FROM Sales.Customer;
```

2. **Retrieve all products with their names and prices**
```Python
SELECT ProductID, Name, ListPrice FROM Production.Product;
```

## Filtering with WHERE Clause
3. **Retrieve products that cost more than $1000**
```Python
SELECT ProductID, Name, ListPrice 
FROM Production.Product
WHERE ListPrice > 1000;
```

4. **Retrieve orders placed after January 1, 2023**
```Python
SELECT SalesOrderID, OrderDate, CustomerID 
FROM Sales.SalesOrderHeader
WHERE OrderDate > '2023-01-01';
```

## Sorting Data
5. **Retrieve the top 10 most expensive products**
```Python
SELECT ProductID, Name, ListPrice 
FROM Production.Product
ORDER BY ListPrice DESC
LIMIT 10;
```

6. **Retrieve the top 5 most recent orders**
```Python
SELECT SalesOrderID, OrderDate, TotalDue 
FROM Sales.SalesOrderHeader
ORDER BY OrderDate DESC
LIMIT 5;
```

## Using Aggregate Functions

7. **Count the total number of customers**
```Python
SELECT COUNT(*) AS TotalCustomers FROM Sales.Customer;
```

8. **Calculate the average price of products**
```Python
SELECT AVG(ListPrice) AS AveragePrice FROM Production.Product;
```

9. **Find the highest and lowest product prices**
```Python
SELECT MAX(ListPrice) AS MaxPrice, MIN(ListPrice) AS MinPrice 
FROM Production.Product;
```

## Grouping Data with GROUP BY
10. **Count the number of products in each category**
```Python
SELECT ProductCategoryID, COUNT(*) AS ProductCount 
FROM Production.Product
GROUP BY ProductCategoryID;
```

11. **Find total sales by year**
```Python
SELECT YEAR(OrderDate) AS SalesYear, SUM(TotalDue) AS TotalSales 
FROM Sales.SalesOrderHeader
GROUP BY YEAR(OrderDate);
```

## Joins: Combining Multiple Tables
12. **Retrieve customer names with their order details**
```Python
SELECT C.CustomerID, P.FirstName, P.LastName, SOH.SalesOrderID, SOH.TotalDue
FROM Sales.Customer C
JOIN Person.Person P ON C.PersonID = P.BusinessEntityID
JOIN Sales.SalesOrderHeader SOH ON C.CustomerID = SOH.CustomerID;
```

13. **Retrieve products and their categories**
```Python
SELECT P.ProductID, P.Name AS ProductName, PC.Name AS CategoryName
FROM Production.Product P
JOIN Production.ProductSubcategory PSC ON P.ProductSubcategoryID = PSC.ProductSubcategoryID
JOIN Production.ProductCategory PC ON PSC.ProductCategoryID = PC.ProductCategoryID;
```

## Subqueries
14. **Retrieve products with prices above the average price**
```Python
SELECT ProductID, Name, ListPrice 
FROM Production.Product
WHERE ListPrice > (SELECT AVG(ListPrice) FROM Production.Product);
```

15. **Retrieve customers who have placed more than 5 orders**
```Python
SELECT CustomerID 
FROM Sales.SalesOrderHeader
GROUP BY CustomerID
HAVING COUNT(SalesOrderID) > 5;
```

## Data Modification (INSERT, UPDATE, DELETE)
16. **Insert a new customer**
```Python
INSERT INTO Sales.Customer (PersonID, StoreID, TerritoryID, AccountNumber)
VALUES (NULL, 932, 5, 'AW00099999');
```

17. **Update product price by 10%**
```Python
UPDATE Production.Product
SET ListPrice = ListPrice * 1.10
WHERE ProductID = 1;
```

18. **Delete a customer who has no orders**
```Python
DELETE FROM Sales.Customer
WHERE CustomerID NOT IN (SELECT DISTINCT CustomerID FROM Sales.SalesOrderHeader);
```


