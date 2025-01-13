
## 1. Classes and objects

  - A class is a template for objects, and an object is an instance of a class.
  - When the individual objects are created, they inherit all the variables and methods from the class.


## 2. Properties
  
  - A property is like a combination of a variable and a method, and it has two methods: a get and a set method:
  
  ```csharp
  
   class Person
    {
      private string name; // field
    
      public string Name   // property
      {
        get { return name; }   // get method
        set { name = value; }  // set method
      }
    }
  ```

  ## Example explained
  - The Name property is associated with the name field. It is a good practice to use the same name for both the property and the private field, but with an uppercase     
  first letter.
  
  - The get method returns the value of the variable name.
  
  - The set method assigns a value to the name variable. The value keyword represents the value we assign to the property.


## 3. Dependency Injection
 
- Dependency Injection (DI) is a design pattern in C# and other programming languages that promotes loose coupling between classes by providing dependencies from an external source rather than creating them inside a class. DI is commonly used in frameworks like ASP.NET Core to improve modularity, testability, and maintainability.
  
- The lifecycle of dependency injection (DI) in C# (especially in ASP.NET Core) refers to the way the Dependency Injection Container (DI container) manages the creation, lifespan, and destruction of dependencies.
  - Transient- New service created every time requested
  - Scoped - New service once per request
  - Singleton - New Service once per application lifetime
   
 
 
Let's use a real-life analogy: A car that requires an engine to run.
  - The Car depends on an Engine to function.
  - Instead of the car building its own engine, we inject the engine (as a dependency).
  - This way, we can replace or modify the engine easily without changing the car's code.
 

## 4. Dapper

  Known as a micro-ORM, it's lightweight and focuses on performance.
  Executes raw SQL queries and maps the results to objects with minimal overhead.
  Faster than Entity Framework because it doesn’t have features like change tracking or complex object state management.
  Suitable for high-performance applications where speed is critical.
## 5. Sql Basic
 - CREATE TABLE
   
   ```sql
   CREATE TABLE Products (
    ProductID INT PRIMARY KEY IDENTITY(1,1),
    Name NVARCHAR(100) NOT NULL,
    Price DECIMAL(10, 2) NOT NULL,
    Quantity INT NOT NULL
    );

   ```
    - ProductID: Primary key with auto-increment.
    - Name: Name of the product.
    - Price: Product price.
    - Quantity: Quantity available.
  
  - Insert Data
   
     ```sql
      INSERT INTO Products (Name, Price, Quantity)
      VALUES ('Laptop', 1200.00, 10);
      
      INSERT INTO Products (Name, Price, Quantity)
      VALUES ('Phone', 699.99, 25);
     ```

## 6. Stored Procedure?

  - A stored procedure is a prepared SQL code that you can save, so the code can be reused over and over again.
  - So if you have an SQL query that you write over and over again, save it as a stored procedure, and then just call it to execute it.
  - You can also pass parameters to a stored procedure, so that the stored procedure can act based on the parameter value(s) that is passed.

```sql
//Create a Stored Procedure to Retrieve Employees by Department
CREATE PROCEDURE GetEmployeesByDept
    @DeptID INT
AS
BEGIN
    SELECT EmployeeID, Name, Position
    FROM Employees
    WHERE DepartmentID = @DeptID;
END;

//Execute the Procedure
EXEC GetEmployeesByDept @DeptID = 1;

```

## 7. CTE
  - A Common Table Expression (CTE) can make it easier to manage and write complex queries by making them more readable and simple, like database views and derived tables. We can reuse or rewrite the query by breaking down the complex queries into simple blocks.

  ```sql
Get Top Earners in Each Department
sql
Copy code
WITH MaxSalaryByDept AS (
    SELECT DepartmentID, MAX(Salary) AS MaxSalary
    FROM Employees
    GROUP BY DepartmentID
)
SELECT e.Name, e.Salary, e.DepartmentID
FROM Employees e
JOIN MaxSalaryByDept m
ON e.DepartmentID = m.DepartmentID AND e.Salary = m.MaxSalary;

  ```

![image](https://github.com/user-attachments/assets/47e6a5c0-76be-41a2-a534-f23093511ca3)


