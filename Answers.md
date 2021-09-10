Simran Sandhu - Winter 2022 Data Science Intern Challenge

# Question 1

a. Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. 

Average order value (AOV) is used to track average dollars spent per order. Like other average metrics, the shortcoming of AOV is its sensitivity to outliers. For this dataset, there are a small number extraordinarily large orders that cause severe right skewness to the data. Due to the skewness, the AOV is not a true reflection of customer purchasing habits. Instead, the AOV falsely inflates order values rendering it meaningless for effective analysis. This suspicion is confirmed by a brief look at the first 20 values of the dataset, skewness value much greater than 1, and distribution plot.

b. What metric would you report for this dataset?

Instead of AOV, the median order value (MOV) would be a better metric to track dollars spent per order. The median order value is less susceptible to outliers and can accurately reflect the centre of a skewed dataset. Alternatively, since the dataset doesn't have multiple clusters, the AOV could be utilized with outliers removed from the dataset or replaced with the median. This alternative is a feasible option since outliers only make up < 3% of the dataset.

c. What is its value?

AOV = 3145.13 without any modifications to dataset

**MOV = 284.0 without any modifications to dataset**

AOV = 293.72 with outliers removed from dataset

AOV = 293.44 with outliers replaced with median


# Question 2

a. How many orders were shipped by Speedy Express in total?
**SQL QUERY:**

SELECT Shippers.ShipperName, COUNT(Shippers.ShipperName) AS OrdersShipped
FROM Orders
INNER JOIN Shippers ON Orders.ShipperID=Shippers.ShipperID
WHERE ShipperName = 'Speedy Express'
GROUP BY ShipperName;

**Answer:**

54

b. What is the last name of the employee with the most orders?

**SQL QUERY:**

SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumOrders
FROM Orders
INNER JOIN Employees ON Orders.EmployeeID=Employees.EmployeeID
GROUP BY LastName
ORDER BY NumOrders DESC LIMIT 1;

**Answer:**

Peacock

c. What product was ordered the most by customers in Germany?

**SQL QUERY:**

SELECT Customers.Country, Products.ProductName, SUM(OrderDetails.Quantity) AS TotalOrdered
FROM Orders
INNER JOIN Customers ON Orders.CustomerID=Customers.CustomerID
INNER JOIN OrderDetails ON Orders.OrderID=OrderDetails.OrderID
INNER JOIN Products ON OrderDetails.ProductID=Products.ProductID
WHERE Country = 'Germany'
GROUP BY ProductName
ORDER BY TotalOrdered DESC LIMIT 1;

**Answer:**

Boston Crab Meat, TotalOrdered = 160
