# Sales Analysis System (AdventureWorksLT2019)

A step-by-step SQL Server project implementing a Sales Analysis System using AdventureWorksLT2019.  
The project demonstrates creation of a view, stored procedure, analytical queries, and execution logic.

---

## 📌 Project Steps

### Step 1: Create the View
```sql
CREATE VIEW vw_SalesOrderDetails AS
SELECT
    soh.SalesOrderID,
    CONCAT(c.FirstName, ' ', c.LastName) AS CustomerName,
    p.Name AS ProductName,
    sod.OrderQty,
    sod.UnitPrice,
    (sod.OrderQty * sod.UnitPrice) AS TotalPrice
FROM SalesLT.SalesOrderHeader soh
JOIN SalesLT.Customer c
    ON soh.CustomerID = c.CustomerID
JOIN SalesLT.SalesOrderDetail sod
    ON soh.SalesOrderID = sod.SalesOrderID
JOIN SalesLT.Product p
    ON sod.ProductID = p.ProductID;
```
![Step 1 Screenshot](Screenshots/Step1_Create_View.png)

---

### Step 2: Create the Stored Procedure
```sql
CREATE PROCEDURE UpdateProductPrice
    @ProductID INT,
    @NewPrice DECIMAL(10, 2)
AS
BEGIN
    DECLARE @CurrentPrice DECIMAL(10, 2);

    SELECT @CurrentPrice = ListPrice
    FROM SalesLT.Product
    WHERE ProductID = @ProductID;

    -- Check if the new price is valid
    IF @NewPrice < (@CurrentPrice * 0.5)
    BEGIN
        PRINT 'Error: New price cannot be less than 50% of the current price.';
        RETURN;
    END

    -- Update the price if valid
    UPDATE SalesLT.Product
    SET ListPrice = @NewPrice
    WHERE ProductID = @ProductID;

    PRINT 'Product price updated successfully.';
END;
```
![Step 2 Screenshot](Screenshots/Step2_Create_StoredProcedure.png)

---

### Step 3: Query the View
```sql
SELECT *
FROM vw_SalesOrderDetails
WHERE CustomerName = 'Andrea Thomsen'
ORDER BY TotalPrice DESC;
```
![Step 3 Screenshot](Screenshots/Step3_Query_View.png)

---

### Step 4: Execute the Procedure
```sql
EXEC UpdateProductPrice
    @ProductID = 680,
    @NewPrice = 50.00;
```
![Step 4 Screenshot](Screenshots/Step4_Execute_Procedure.png)

---

## 🛠 Tech Stack
- SQL Server 2019 / SSMS
- AdventureWorksLT2019 Sample Database

---

## 🎯 Learning Outcomes
- Creating and managing SQL Views
- Implementing Stored Procedures with validation rules
- Querying views for analytics
- Executing and testing procedures

---

✅ Project completed successfully as per provided PDF scenario.  
Suitable for GitHub and LinkedIn portfolio showcase.

---

## 📂 Repository Structure
```
Sales-Analysis-System/
│
├── README.md
├── Screenshots/
│   ├── Step1_Create_View.png
│   ├── Step2_Create_StoredProcedure.png
│   ├── Step3_Query_View.png
│   └── Step4_Execute_Procedure.png
```

---
