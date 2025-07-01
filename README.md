                                                #Task-6(Subqueries and Nested Queries)
# Customer-and-Orders-Database
 SQL Subqueries
 Subqueries are essential for building complex queries by allowing one query to be nested within another.
```
📁 Project Overview
```
This section showcases how to write and use subqueries in SQL to solve real-world database problems.

Subqueries are powerful tools used to:

Compare results from different queries
Filter data using conditions from another table
Return single or multiple values inside conditions
This project is part of my learning and internship submission, aimed at demonstrating my understanding of database design concepts.
```
📌 Tables:
1.Customers
2.Orders
```
🧾 SQL Script
```
Creating the data
```
```
-- Create Customers table
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Email VARCHAR(100) UNIQUE
);

-- Create Orders table
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    Amount DECIMAL(10, 2),
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```
Inserting the data
```
-- Insert into Customers
INSERT INTO Customers (CustomerID, Name, Email) VALUES
(1, 'Prajjawal', 'prajjwal26@gmail.com'),
(2, 'Pranshu', 'pranshu00@gmail.com'),
(3, 'Khusi', 'khusi@gmail.com'),
(4, 'Mayank','mayank09@gmail.com');

-- Insert into Orders
INSERT INTO Orders (OrderID, CustomerID, OrderDate, Amount) VALUES
(101, 1, '2025-02-01', 500.00),
(102, 2, '2025-03-05', 1500.00),
(103, 3, '2025-04-03', 2500.00),
(104, 4, '2025-05-30', 3000.00);
```
Subqueries
```
1️⃣ Scalar Subqueries
A scalar subquery returns a single value, often used in WHERE, SELECT, or HAVING clauses.
```
```
SELECT Name
FROM Customers
WHERE CustomerID IN (
    SELECT CustomerID
    FROM Orders
    GROUP BY CustomerID
    HAVING SUM(Amount) > (
        SELECT AVG(Amount) FROM Orders
    )
);
```
output

![image](https://github.com/user-attachments/assets/10d6baac-883d-4b8e-831c-57b5c024aabc)

```
2️⃣ Correlated Subqueries
```
A correlated subquery depends on a value from the outer query.
```
SELECT Name
FROM Customers c
WHERE EXISTS (
    SELECT 1
    FROM Orders o
    WHERE o.CustomerID = c.CustomerID AND o.Amount < 2000
);

```
Output

![image](https://github.com/user-attachments/assets/1f1c6259-7657-477b-a242-7bab759a2d3d)


```
3️⃣ Subquery with IN

```
SELECT Name
FROM Customers
WHERE CustomerID IN (
    SELECT CustomerID FROM Orders
);
```
Output
```
![image](https://github.com/user-attachments/assets/dc920429-4242-4179-adc1-211b5eb955be)

```
4️⃣ Subquery with EXISTS
```
SELECT Name
FROM Customers c
WHERE EXISTS (
    SELECT 1 FROM Orders o
    WHERE o.CustomerID = c.CustomerID
);
```
Output
```
![image](https://github.com/user-attachments/assets/5557381f-2ad4-432d-b694-ac51a78801b6)

```
5️⃣ Subquery with =

```
SELECT Name FROM Customers
WHERE CustomerID = (
    SELECT CustomerID
    FROM Orders
    ORDER BY Amount DESC
    LIMIT 1
);
```
Output
```
![image](https://github.com/user-attachments/assets/88cab3b2-d6cc-457c-b3be-7adf5126dad2)

```
