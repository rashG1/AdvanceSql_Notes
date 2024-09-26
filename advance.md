# API

**What is an API?**

An API (Application Program Interface) is a set of rules and protocols that allows a program to interact with a database server. It enables an application to connect with the database server, send SQL commands, and fetch results.

**JDBC:**

JDBC is a Java API that provides a reliable environment for communicating with database systems that support SQL. It is independent of any particular database.

**Drivers:**

For every database, we need drivers. Drivers convert JDBC calls to database-specific calls. There are 4 types of drivers:

- Type-1: JDBC-ODBC Bridge Driver
- Type-2: Native API Driver
- Type-3: Network Protocol Driver
- Type-4: Thin Driver (fastest of all drivers)

***Embedded SQL***

Embedded SQL refers to the practice of including SQL statements directly within a host programming language, such as C, Java, or Python. It allows developers to seamlessly integrate database operations into their application code.

**Advantages of Embedded SQL:**

1. Ease of Database Usage: Embedded SQL simplifies database access by eliminating the need for extensive coding. Developers can directly include SQL statements within the host programming language, making it easier to interact with the database.

2. Security and Authorization: Embedded SQL allows for setting specific authorization procedures, ensuring secure access to sensitive data. Developers can control and manage user permissions within the application code.

3. Frontend and Backend Integration: Embedded SQL enables seamless integration between the frontend and backend of an application. This improves real-time data retrieval and enhances the overall user experience.

4. Error Prevention: By embedding SQL into the application code, embedded SQL reduces logical errors. This enhances security and reliability by ensuring that database operations are performed correctly.

**Disadvantages of Embedded SQL:**

1. Host Language Knowledge Required: Developers must have a good understanding of the host programming language to effectively use embedded SQL. This requires additional expertise and may pose a learning curve for developers who are not familiar with the host language.

2. Complex Development: Integrating SQL within the host language can be challenging, especially for larger systems. Developers need to carefully manage the integration of SQL statements with the host language code, which can increase the complexity of development.

3. Limited Flexibility: Embedded SQL relies on predefined queries, which can limit the application's adaptability to changing requirements. Modifying or adding new queries may require modifying the host language code, making it less flexible compared to dynamic SQL approaches.

**EXEC SQL statement is used to identify embedded SQL request to the preprocessor**

This structure may vary depending on the programming language. For instance:

**C/C++: Follows the EXEC SQL syntax.**
EXEC SQL SELECT * FROM employees WHERE employee_id = 1 END_EXEC;

**Java (JDBC): Uses #SQL { ... } for embedding SQL.**
#SQL { SELECT * FROM employees WHERE employee_id = 1 };

**How Embedding Helps Detect Errors Early:**

1. Static SQL in Java: SQLJ statements are embedded within Java code and processed during compilation. This allows for checking SQL syntax and type matching against Java variables at compile time.

2. Type Safety: SQLJ can ensure that the data returned by SQL queries matches the expected Java types, reducing type-related runtime errors.

**SQLJ Example:**

In this example, we are selecting department names and average salaries from an instructor table and printing them out.

```java
#sql iterator deptInfoIter (String dept_name, int avgSal);

deptInfoIter iter = null;

#sql iter = {
    SELECT dept_name, AVG(salary)
    FROM instructor
    GROUP BY dept_name
};

while (iter.next()) {
    String deptName = iter.dept_name();  // Fetch department name
    int avgSal = iter.avgSal();          // Fetch average salary
    System.out.println(deptName + " " + avgSal);
}

iter.close();

Explanation:

SQLJ Iterator Definition:

`#sql iterator deptInfoIter (String dept_name, int avgSal);`

This defines an iterator `deptInfoIter` that will hold two values: `dept_name` (a `String`) and `avgSal` (an `int` representing the average salary). It ensures that the SQL query will return values of the correct types.

SQL Execution:

`#sql iter = { SELECT dept_name, AVG(salary) FROM instructor GROUP BY dept_name };`

The SQL query is embedded in the Java code using the `#sql` block. The query groups instructors by department and calculates the average salary for each group.

Fetching and Using Results:

while (iter.next()) {
    String deptName = iter.dept_name();  // Retrieves department name
    int avgSal = iter.avgSal();          // Retrieves average salary
    System.out.println(deptName + " " + avgSal);
}

The while (iter.next()) loop iterates through the result set. Each time, it fetches the department name and average salary and prints them.

### Iterator Closure:

```java
iter.close();
```
After processing all results, the iterator is closed to free up resources.

### Why SQLJ is Beneficial:

- **Compile-Time Checking:** Ensures that SQL syntax and data types are checked at compile time, reducing the risk of runtime errors.
- **Easier Error Handling:** Developers can avoid handling certain errors at runtime, which simplifies the code.
- **Better Performance:** Because SQL is embedded and static, SQLJ can optimize SQL execution compared to the fully dynamic nature of JDBC.

### Difference between SQLJ and JDBC

SQLJ and JDBC are both Java APIs for interacting with databases but serve different purposes.

- **JDBC (Java Database Connectivity):** A dynamic API allowing applications to run SQL queries at runtime. It gives full control over query execution but requires manual error handling, with errors detected only during execution.

- **SQLJ:** A higher-level API for embedding static SQL directly into code. It checks SQL syntax and types at compile time, offering better safety but with less flexibility than JDBC. SQLJ internally relies on JDBC to connect to databases.

| Feature            | JDBC                                       | SQLJ                                      |
|--------------------|--------------------------------------------|-------------------------------------------|
| SQL Queries        | Dynamic (runtime)                          | Static (compile-time)                     |
| Error Checking     | At runtime                                 | At compile time (syntax and types)        |
| Control            | Full control over query construction       | Limited to predefined queries             |
| Usage              | Suitable for dynamic queries               | Suitable for static, predefined queries   |

### Very Important

SQLJ doesn’t handle the actual communication with the database itself. It relies on JDBC for that part. JDBC is the underlying mechanism used to connect to the database, send the SQL queries, and receive the results. SQLJ provides a more structured, static approach to writing queries, but when it comes to executing them, it passes those requests to JDBC.


































































References:
- Tutorialspoint.com
