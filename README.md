<details>
  <summary>
    1. Classes and objects
  </summary>
  <br>
  
  - A class is a template for objects, and an object is an instance of a class.
  - When the individual objects are created, they inherit all the variables and methods from the class.

</details>


<details>
  <summary>
    2. Properties
  </summary>
  <br>
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
<p>
  ## Example explained
  The Name property is associated with the name field. It is a good practice to use the same name for both the property and the private field, but with an uppercase     
  first letter.
  
  The get method returns the value of the variable name.
  
  The set method assigns a value to the name variable. The value keyword represents the value we assign to the property.
</p>
</details>


<details>
  <summary>
    3. Dependency Injection
  </summary>
  <br>
  <p>
    Dependency Injection (DI) is a design pattern in C# and other programming languages that promotes loose coupling between classes by providing dependencies from an external source rather than creating them inside a class. DI is commonly used in frameworks like ASP.NET Core to improve modularity, testability, and maintainability.
  </p>
  <p>
    The lifecycle of dependency injection (DI) in C# (especially in ASP.NET Core) refers to the way the Dependency Injection Container (DI container) manages the creation, lifespan, and destruction of dependencies.
  </p>

  ![image](https://github.com/user-attachments/assets/913e53b0-786b-49eb-b54c-8da961b9a1ff)
  <p>
    Let's use a real-life analogy: A car that requires an engine to run.
  1.	The Car depends on an Engine to function.
  2.	Instead of the car building its own engine, we inject the engine (as a dependency).
  3.	This way, we can replace or modify the engine easily without changing the car's code.
  </p>


</details>


<details>
  <summary>
    4. Dapper
  </summary>
  <br>
    
  ### Dapper:

  Known as a micro-ORM, it's lightweight and focuses on performance.
  Executes raw SQL queries and maps the results to objects with minimal overhead.
  Faster than Entity Framework because it doesn’t have features like change tracking or complex object state management.
  Suitable for high-performance applications where speed is critical.

  ### Entity Framework:

  A full-fledged ORM, offering features like LINQ-to-Entities, change tracking, and lazy loading.
  Relatively slower than Dapper due to the abstraction and extra features it provides.
  Performance might be an issue for large-scale or performance-critical applications.
</details>


<details>
  <summary>
    5. Stored Procedure?
  </summary>
  <br>
  
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
</details>



<details>
  <summary>
    6. CTE
  </summary>
  <br>
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

</details>
