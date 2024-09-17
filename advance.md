# JDBC

what is an API?

API (Application Program Interface) is a set of rules and protocols that allows a program to interact with a database server.

An application can use an API to:

- Connect with the database server
- Send SQL commands to the database server
- Fetch tuples of results one-by-one into program variables

JDBC:

JDBC is a Java API that provides a reliable environment for communicating with database systems that support SQL. It is independent of any particular database.

Drivers:
For every database, we need drivers. Drivers convert JDBC calls to database-specific calls.

There are 4 types of drivers:

- Type-1: JDBC-ODBC Bridge Driver
- Type-2: Native API Driver
- Type-3: Network Protocol Driver
- Type-4: Thin Driver (fastest of all drivers)


# Embedded SQL

Embedded SQL refers to the practice of including SQL statements directly within a host programming language, such as C, Java, or Python. It allows developers to seamlessly integrate database operations into their application code.


Advantages of Embedded SQL:

Ease of Database Usage: Simplifies database access by eliminating the need for extensive coding.

Security and Authorization: Allows for setting specific authorization procedures, ensuring secure access to sensitive data.

Frontend and Backend Integration: Enables seamless integration, improving real-time data retrieval and user experience.

Error Prevention: Reduces logical errors by embedding SQL into application code, enhancing security and reliability.
Disadvantages of Embedded SQL:

Host Language Knowledge Required: Developers must understand the host language, requiring additional expertise.

Complex Development: Integrating SQL within the host language can be challenging, especially for larger systems.

Limited Flexibility: Predefined queries limit the application's adaptability to changing requirements.



**EXEC SQL statement is used to identify embedded SQL request to the preprocessor**
EXEC SQL <embedded SQL statement > END_EXEC


This structure may vary depending on the programming language. For instance:

**C/C++: Follows the EXEC SQL syntax.**
EXEC SQL SELECT * FROM employees WHERE employee_id = 1 END_EXEC;

**Java (JDBC): Uses #SQL { ... } for embedding SQL.**
#SQL { SELECT * FROM employees WHERE employee_id = 1 };














































References:
https://www.tutorialspoint.com/