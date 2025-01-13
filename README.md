
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

## 8. Sql function
- Aggregate Functions in SQL
Aggregate functions perform calculations on multiple rows of a table and return a single value. Common aggregate functions include:

    - COUNT(): Counts rows.
    - SUM(): Adds up numeric values.
    - AVG(): Calculates the average of numeric values.
    - MIN(): Finds the smallest value.
    - MAX(): Finds the largest value.
- GROUP BY Clause
  - The GROUP BY clause is used to arrange identical data into groups. It’s often used with aggregate functions to perform calculations on each group.
- HAVING Clause
  - The HAVING clause is used to filter groups after the aggregation is applied (unlike the WHERE clause, which filters rows before aggregation).
- Combining GROUP BY and HAVING with WHERE
   - You can combine WHERE, GROUP BY, and HAVING for more control:
    
   - WHERE: Filters rows before grouping.
   - GROUP BY: Groups filtered rows.
   - HAVING: Filters groups based on aggregate values.
     
## 9. React Hooks 
*React Hooks allow developers to use state and other React features in functional components, making the code cleaner, more reusable, and easier to maintain. Let's dive into 
the core Hooks you mentioned and their usage.*
    
  1. useState
      - The useState Hook allows functional components to manage state. It returns an array with two values:
       - The current state.
       - A function to update the state.
       - Syntex
          ```jsx
          const [state, setState] = useState(initialValue);
          ```
       - Example
         ```jsx
          import React, { useState } from "react";

          function Counter() {
              const [count, setCount] = useState(0);
          
              return (
                  <div>
                      <p>Count: {count}</p>
                      <button onClick={() => setCount(count + 1)}>Increment</button>
                  </div>
              );
          }

         ```
  2. useEffect
  - The useEffect Hook lets you perform side effects, such as fetching data, subscribing to services, or updating the DOM.
  - It runs after the render and can optionally clean up after itself.

  - Syntax:
    ```jsx
    useEffect(() => {
        // Side effect code
        return () => {
            // Cleanup code (optional)
        };
    }, [dependencies]);
    ```
  - Example:
    ```jsx
    import React, { useState, useEffect } from "react";
    
    function Timer() {
        const [count, setCount] = useState(0);
    
        useEffect(() => {
            const interval = setInterval(() => {
                setCount((prevCount) => prevCount + 1);
            }, 1000);
    
            return () => clearInterval(interval); // Cleanup
        }, []); // Empty dependency array ensures this runs once when mounted
    
        return <div>Timer: {count}</div>;
    }
    ```
3. useContext
 - The useContext Hook provides an easy way to consume React's Context API.
 - It avoids prop drilling by allowing components to access shared state.

Syntax:
```jsx
const contextValue = useContext(ContextObject);
```
Example:
```jsx
import React, { useContext, createContext } from "react";

const ThemeContext = createContext("light");

function ThemedComponent() {
    const theme = useContext(ThemeContext);

    return <div>Current Theme: {theme}</div>;
}

function App() {
    return (
        <ThemeContext.Provider value="dark">
            <ThemedComponent />
        </ThemeContext.Provider>
    );
}
```
4. Custom Hooks
- Custom Hooks enable you to reuse stateful logic between components.
- They are regular functions but can call other Hooks.

- Example:
```jsx
import React, { useState, useEffect } from "react";

function useFetch(url) {
    const [data, setData] = useState(null);
    const [loading, setLoading] = useState(true);

    useEffect(() => {
        fetch(url)
            .then((response) => response.json())
            .then((data) => {
                setData(data);
                setLoading(false);
            });
    }, [url]);

    return { data, loading };
}

function App() {
    const { data, loading } = useFetch("https://api.example.com/data");

    if (loading) return <p>Loading...</p>;
    return <div>Data: {JSON.stringify(data)}</div>;
}
```
### Key Tips for Using Hooks:
*Order and Rules:*
- Always call Hooks at the top level of your component or custom Hook.
- Do not call Hooks inside loops, conditions, or nested functions.
*Dependencies in useEffect:*
- Ensure dependency arrays ([]) include all external variables used in the effect.
- Use eslint-plugin-react-hooks to help enforce these rules.
*Custom Hooks:*
- Name custom Hooks starting with "use" (e.g., useFetch, useToggle).
- Combine useState and useEffect to encapsulate reusable logic.
- By mastering these Hooks, you'll be able to build functional, efficient, and reusable components. Let me know if you'd like further clarification or advanced examples!

## 10. SPA
 - Single-page applications (SPAs) dynamically update the web page as the user interacts with it, without requiring a full page reload. Routing in SPAs enables users to navigate between views or pages while keeping the app loaded in the browser.
 - Basic Routing Example
   ```jsx
    import React from "react";
    import { BrowserRouter as Router, Routes, Route, Link } from "react-router-dom";
    
    function Home() {
      return <h2>Home Page</h2>;
    }
    
    function About() {
      return <h2>About Page</h2>;
    }
    
    function Contact() {
      return <h2>Contact Page</h2>;
    }
    
    function App() {
      return (
        <Router>
          <nav>
            <Link to="/">Home</Link> | <Link to="/about">About</Link> | <Link to="/contact">Contact</Link>
          </nav>
          <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<About />} />
            <Route path="/contact" element={<Contact />} />
          </Routes>
        </Router>
      );
    }
    
    export default App;

   ```
- Dynamic Routing
  ```jsx
    import React from "react";
    import { BrowserRouter as Router, Routes, Route, useParams } from "react-router-dom";
    
    function User() {
      const { userId } = useParams(); // Extracts userId from the URL
      return <h2>User Profile: {userId}</h2>;
    }
    
    function App() {
      return (
        <Router>
          <Routes>
            <Route path="/user/:userId" element={<User />} />
          </Routes>
        </Router>
      );
    }
    
    export default App;

  ```
  Explanation:
   - The path /user/:userId defines a route with a dynamic segment :userId.
   - The useParams hook retrieves the userId from the URL.
 
## 11. Axios
  - Axios is a popular library used for making HTTP requests in JavaScript applications. It provides a promise-based API that is simple to use and works well with asynchronous operations. Axios is often preferred for its ease of use and additional features like interceptors, automatic JSON parsing, and request cancellation
  - Basic Axios Requests
    - GET Request
    - Fetch data from an API endpoint.
      ```jsx
      import React, { useEffect, useState } from "react";
      import axios from "axios";
      
      function App() {
        const [data, setData] = useState([]);
        const [loading, setLoading] = useState(true);
      
        useEffect(() => {
          axios
            .get("https://jsonplaceholder.typicode.com/posts")
            .then((response) => {
              setData(response.data); // Set the fetched data
              setLoading(false); // Turn off loading
            })
            .catch((error) => {
              console.error("Error fetching data:", error);
              setLoading(false);
            });
        }, []);
      
        if (loading) {
          return <div>Loading...</div>;
        }
      
        return (
          <div>
            <h1>Posts</h1>
            <ul>
              {data.map((post) => (
                <li key={post.id}>{post.title}</li>
              ))}
            </ul>
          </div>
        );
      }
      
      export default App;

      ```
  - Explanation:
    - axios.get(url): Makes a GET request to the specified URL.
    - Handles the promise with .then() for success and .catch() for errors.
    - Stores the fetched data in the data state and handles loading state with loading.
- POST Request
- Send data to an API.
    ```jsx
    import React, { useState } from "react";
    import axios from "axios";
    
    function App() {
      const [title, setTitle] = useState("");
      const [body, setBody] = useState("");
      const [response, setResponse] = useState(null);
    
      const handleSubmit = (e) => {
        e.preventDefault();
        axios
          .post("https://jsonplaceholder.typicode.com/posts", {
            title,
            body,
            userId: 1,
          })
          .then((res) => setResponse(res.data))
          .catch((error) => console.error("Error posting data:", error));
      };
    
      return (
        <div>
          <h1>Create Post</h1>
          <form onSubmit={handleSubmit}>
            <div>
              <label>Title:</label>
              <input value={title} onChange={(e) => setTitle(e.target.value)} />
            </div>
            <div>
              <label>Body:</label>
              <textarea value={body} onChange={(e) => setBody(e.target.value)} />
            </div>
            <button type="submit">Submit</button>
          </form>
          {response && (
            <div>
              <h2>Response</h2>
              <p>ID: {response.id}</p>
              <p>Title: {response.title}</p>
              <p>Body: {response.body}</p>
            </div>
          )}
        </div>
      );
    }
    
    export default App;

    ```
Explanation:
- axios.post(url, data): Sends a POST request with data in the request body.
- The response from the API is displayed after submission.
