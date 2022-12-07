--1--
select * from Products where UnitPrice between 30 and 40

--2--
select * from Products where CategoryID = 2

--3--
select ProductName,c.Description from Products as p inner join Categories as c on p.CategoryID = c.CategoryID
where Description like '%S%' order by ProductName

--4--
SELECT DISTINCT ProductName
FROM Products
        inner JOIN
    [Order Details] ON Products.ProductID =  [Order Details].ProductID
       inner JOIN
    Orders ON  [Order Details].OrderID = Orders.OrderID
       inner JOIN
    Customers ON Orders.CustomerID = Customers.CustomerID
WHERE
    Customers.CustomerID = 'ALFKI'

--5--
SELECT * FROM Orders where ShipCountry = 'Brazil' or ShipCity = 'London'

--6--
SELECT DISTINCT [Customers].CompanyName from Customers 
INNER JOIN Orders ON Customers.CustomerID = Orders.CustomerID 
INNER JOIN Shippers ON Shippers.ShipperID = Orders.ShipVia 
where Shippers.CompanyName like 'Federal Shipping'

--7--
CREATE PROCEDURE Section7 
@orderID int 
as begin 
select ProductName from Products where ProductID in (select ProductID from [Order Details] where OrderID = @orderID)
select OrderPrice = sum(UnitPrice) from [dbo].[Order Details] where OrderID = @orderID
end

exec Section7 10248

--8--
SELECT [CustomerID],[EmployeeID],[ShipVia],[Freight],[ShipName],[ShipAddress],[ShipCity],[ShipRegion],[ShipPostalCode],[ShipCountry]
FROM Orders where CustomerID  like 'B%' and ShipVia = 1 and (EmployeeID = 2 or EmployeeID = 5) and ShipName like 'B%'

--9--
select [dbo].[Order Details].OrderID, ProductID, UnitPrice, Quantity, Discount, OrderDate, EmployeeID,CustomerID from Orders inner join [Order Details] on [Order Details].OrderID = Orders.OrderID OR [Order Details].OrderID != Orders.OrderID
where [dbo].[Order Details].OrderID = 10248 and Orders.CustomerID like 'VINET' 
order by UnitPrice, EmployeeID

--10--
select CustomerID, Region, Country from Customers where Country like '%c%' and Country like '%a%' order by CustomerID