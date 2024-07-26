---
title: Port Swigger Labs
# author: Gauranga
date: 2024-03-04 11:27:22 +00:00
# categories: [Writing]
tags: [Documentation]
pin: true
math: true
mermaid: true
image: https://pbs.twimg.com/profile_images/1271377080220033024/InZ0OCwH_400x400.png
#   path: /commons/devices-mockup.png
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
#   alt: Responsive rendering of Chirpy theme on multiple devices.
---


# Lab 1: SQL Injection Vulnerability Exploitation in Product Category Filter

## Lab Objective:

The objective of this lab is to showcase the ability to exploit SQL injection vulnerabilities to bypass security measures and gain unauthorized access to sensitive data.

## Lab Procedure:

1. **Accessing the Lab:**
    - Navigate to the provided lab URL to access the vulnerable web application.
2. **Identifying the Vulnerability:**
    - Upon accessing the application, observe the functionality related to product filtering, specifically focusing on the product category filter.
3. **Intercepting the Request:**
    - Open Burp Suite and configure it to intercept HTTP requests.
    - Navigate to the page where the product category filter is applied.
    - Initiate the action to set the product category filter.
4. **Modifying the Request:**
    - In Burp Suite, intercept the request that sets the product category filter.
    - Modify the `category` parameter in the intercepted request.
5. **Exploiting the SQL Injection Vulnerability:**
    - Change the value of the `category` parameter to `' OR 1=1--`.
    - This modification introduces a SQL injection payload into the SQL query executed by the application.
6. **Submitting the Request:**
    - Forward the modified request from Burp Suite to the vulnerable application.
7. **Verifying the Results:**
    - Observe the response from the application.
    - Verify that the response now contains one or more unreleased products, indicating successful exploitation of the SQL injection vulnerability.
    - Note: The unreleased products are displayed despite the intended restriction imposed by the `released = 1` condition in the original SQL query.

---

# Lab 2: SQL Injection Vulnerability Allowing Login Bypass

## Lab Objective:

The objective of this lab is to showcase the exploitation of a SQL injection vulnerability to bypass the authentication mechanism and log in as the administrator user.

## Lab Procedure:

1. **Accessing the Lab:**
    - Navigate to the provided lab URL to access the vulnerable web application.
2. **Identifying the Vulnerability:**
    - Access the login page of the application and inspect the authentication mechanism.
3. **Intercepting the Login Request:**
    - Open Burp Suite and configure it to intercept HTTP requests.
    - Navigate to the login page of the application.
4. **Modifying the Request:**
    - Intercept the login request in Burp Suite.
    - Modify the `username` parameter in the intercepted request.
5. **Exploiting the SQL Injection Vulnerability:**
    - Change the value of the `username` parameter to `administrator'--`.
    - This modification introduces a SQL injection payload into the SQL query executed by the application, causing it to ignore the password check.
6. **Submitting the Request:**
    - Forward the modified request from Burp Suite to the vulnerable application.
7. **Verifying Successful Login:**
    - Observe the response from the application.
    - Verify that the response indicates successful login as the administrator user.

---

# Lab 3: SQL Injection Attack, Querying the Database Type and Version on Oracle

## Lab Objective:

The objective of this lab is to showcase the exploitation of a SQL injection vulnerability to extract the database type and version information from an Oracle database.

## Lab Procedure:

1. **Accessing the Lab:**
    - Navigate to the provided lab URL to access the vulnerable web application.
2. **Identifying the Vulnerability:**
    - Access the page containing the product category filter of the application.
    - Observe the behavior of the application when filtering products by category.
3. **Intercepting the Request:**
    - Open Burp Suite and configure it to intercept HTTP requests.
    - Navigate to the page where the product category filter is applied.
4. **Determining the Number of Columns:**
    - Intercept the request that sets the product category filter in Burp Suite.
    - Modify the `category` parameter with a payload like `'+UNION+SELECT+'abc','def'+FROM+dual--` to determine the number of columns returned by the query and which columns contain text data.
5. **Displaying the Database Version:**
    - Use the payload `'+UNION+SELECT+BANNER,+NULL+FROM+v$version--` to extract the database version string.
    - Modify the `category` parameter with the above payload in Burp Suite and forward the request to the vulnerable application.
6. **Verifying the Results:**
    - Observe the response from the application.
    - Verify that the response contains the database version string, indicating successful extraction of database type and version information.

---

# Lab 4: SQL Injection Attack, Querying the Database Type and Version on MySQL and Microsoft

## Lab Objective:

The objective of this lab is to showcase the exploitation of a SQL injection vulnerability to extract the database type and version information from both MySQL and Microsoft SQL Server databases.

## Lab Procedure:

1. **Accessing the Lab:**
    - Navigate to the provided lab URL to access the vulnerable web application.
2. **Identifying the Vulnerability:**
    - Access the page containing the product category filter of the application.
    - Observe the behavior of the application when filtering products by category.
3. **Intercepting the Request:**
    - Open Burp Suite and configure it to intercept HTTP requests.
    - Navigate to the page where the product category filter is applied.
4. **Determining the Number of Columns:**
    - Intercept the request that sets the product category filter in Burp Suite.
    - Modify the `category` parameter with a payload like `'+UNION+SELECT+'abc','def'#` to determine the number of columns returned by the query and which columns contain text data.
5. **Displaying the Database Version:**
    - Use the payload `'+UNION+SELECT+@@version,+NULL#` to extract the database version string.
    - Modify the `category` parameter with the above payload in Burp Suite and forward the request to the vulnerable application.
6. **Verifying the Results:**
    - Observe the response from the application.
    - Verify that the response contains the database version string, indicating successful extraction of database type and version information.

---

# Lab 5: SQL Injection Vulnerability, Retrieving User Credentials

## Lab Objective:

The objective of this lab is to demonstrate the exploitation of a SQL injection vulnerability to retrieve user credentials stored in a database table. By using a UNION attack, we will determine the name of the table containing user credentials, the names of the columns within that table, and then retrieve the usernames and passwords to log in as the administrator user.

## Lab Procedure:

1. **Accessing the Lab:**
    - Navigate to the provided lab URL to access the vulnerable web application.
2. **Identifying the Vulnerability:**
    - Access the login function of the application and inspect the authentication mechanism.
3. **Intercepting the Request:**
    - Open Burp Suite and configure it to intercept HTTP requests.
    - Navigate to the login page of the application.
4. **Determining the Number of Columns:**
    - Intercept the request that sets the product category filter in Burp Suite.
    - Modify the `category` parameter with a payload like `'+UNION+SELECT+'abc','def'--` to determine the number of columns returned by the query and which columns contain text data.
5. **Retrieving Table Names:**
    - Use the payload `'+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--` to retrieve the list of tables in the database.
    - Identify the name of the table containing user credentials.
6. **Retrieving Column Names:**
    - Use the payload `'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_abcdef'--` (replace 'users_abcdef' with the actual table name) to retrieve the details of the columns in the table.
    - Identify the names of the columns containing usernames and passwords.
7. **Retrieving Usernames and Passwords:**
    - Use the payload `'+UNION+SELECT+username_abcdef,+password_abcdef+FROM+users_abcdef--` (replace 'users_abcdef' with the actual table name and column names) to retrieve the usernames and passwords for all users.
    - Find the password for the administrator user.
8. **Logging in as Administrator:**
    - Use the retrieved administrator password to log in as the administrator user.

---

# Lab 6: SQL Injection Attack, Listing the Database Contents on Oracle

## Lab Objective:

The objective of this lab is to demonstrate the exploitation of a SQL injection vulnerability to retrieve user credentials stored in a database table on an Oracle database. By using a UNION attack, we will determine the name of the table containing user credentials, the names of the columns within that table, and then retrieve the usernames and passwords to log in as the administrator user.

## Lab Procedure:

1. **Accessing the Lab:**
    - Navigate to the provided lab URL to access the vulnerable web application.
2. **Identifying the Vulnerability:**
    - Access the login function of the application and inspect the authentication mechanism.
3. **Intercepting the Request:**
    - Open Burp Suite and configure it to intercept HTTP requests.
    - Navigate to the login page of the application.
4. **Determining the Number of Columns:**
    - Intercept the request that sets the product category filter in Burp Suite.
    - Modify the `category` parameter with a payload like `'+UNION+SELECT+'abc','def'+FROM+dual--` to determine the number of columns returned by the query and which columns contain text data.
5. **Retrieving Table Names:**
    - Use the payload `'+UNION+SELECT+table_name,NULL+FROM+all_tables--` to retrieve the list of tables in the database.
    - Identify the name of the table containing user credentials.
6. **Retrieving Column Names:**
    - Use the payload `'+UNION+SELECT+column_name,NULL+FROM+all_tab_columns+WHERE+table_name='USERS_ABCDEF'--` (replace 'USERS_ABCDEF' with the actual table name) to retrieve the details of the columns in the table.
    - Identify the names of the columns containing usernames and passwords.
7. **Retrieving Usernames and Passwords:**
    - Use the payload `'+UNION+SELECT+USERNAME_ABCDEF,+PASSWORD_ABCDEF+FROM+USERS_ABCDEF--` (replace 'USERS_ABCDEF' with the actual table name and column names) to retrieve the usernames and passwords for all users.
    - Find the password for the administrator user.
8. **Logging in as Administrator:**
    - Use the retrieved administrator password to log in as the administrator user.

---

# Lab 7: SQL Injection UNION Attack, Determining the Number of Columns Returned by the Query

## Lab Objective:

The objective of this lab is to determine the number of columns returned by the query by performing a SQL injection UNION attack that returns an additional row containing null values.

1. **Browser:** Used for accessing the vulnerable web application.

## Lab Procedure:

1. **Accessing the Lab:**
    - Navigate to the provided lab URL to access the vulnerable web application.
2. **Identifying the Vulnerability:**
    - Access the page containing the product category filter of the application.
    - Observe the behavior of the application when filtering products by category.
3. **Intercepting the Request:**
    - Open Burp Suite and configure it to intercept HTTP requests.
    - Navigate to the page where the product category filter is applied.
4. **Performing a SQL Injection UNION Attack:**
    - Modify the `category` parameter with a payload like `'+UNION+SELECT+NULL--`.
    - Observe that an error occurs, indicating that the number of columns in the original query does not match the number of columns in the injected query.
5. **Determining the Number of Columns:**
    - Modify the `category` parameter to add an additional column containing a null value: `'+UNION+SELECT+NULL,NULL--`.
    - Continue adding null values until the error disappears and the response includes additional content containing the null values.
6. **Verifying the Number of Columns:**
    - Count the number of columns in the response that contain null values.
    - This number represents the total number of columns returned by the query.

---

# Lab 8: SQL Injection UNION Attack, Finding a Column Containing Text

## Lab Objective:

The objective of this lab is to perform a SQL injection UNION attack to identify a column containing text data. By injecting a specified value into the query results, we can determine which column accepts string values and use this information for further exploitation.

## Lab Procedure:

1. **Accessing the Lab:**
    - Navigate to the provided lab URL to access the vulnerable web application.
2. **Identifying the Vulnerability:**
    - Access the page containing the product category filter of the application.
    - Observe the behavior of the application when filtering products by category.
3. **Intercepting the Request:**
    - Open Burp Suite and configure it to intercept HTTP requests.
    - Navigate to the page where the product category filter is applied.
4. **Determining the Number of Columns:**
    - Modify the `category` parameter with a payload like `'+UNION+SELECT+NULL,NULL,NULL--`.
    - Verify that the query is returning three columns.
5. **Injecting Specified Value:**
    - Replace each `NULL` value with the specified random value provided by the lab, for example: `'+UNION+SELECT+'abcdef',NULL,NULL--`.
    - If an error occurs, try replacing each `NULL` value with the next specified random value provided by the lab.
6. **Identifying the Compatible Column:**
    - Observe the application's response to determine which column accepts the injected value without causing an error.
    - This column is compatible with string data and can be used for further exploitation.

---

# Lab 9: SQL Injection UNION Attack, Retrieving Data from Other Tables

## Lab Objective:

The objective of this lab is to demonstrate the exploitation of a SQL injection vulnerability to retrieve user credentials stored in a different table called users. By using a UNION attack, we will construct a SQL injection payload to retrieve all usernames and passwords from the users table and log in as the administrator user.

## Lab Procedure:

1. **Accessing the Lab:**
- Navigate to the provided lab URL to access the vulnerable web application.
2. **Identifying the Vulnerability:**
- Access the page containing the product category filter of the application.
- Observe the behavior of the application when filtering products by category.
3. **Intercepting the Request:**
- Open Burp Suite and configure it to intercept HTTP requests.
- Navigate to the page where the product category filter is applied.
4. **Determining the Number of Columns:**
- Modify the `category` parameter with a payload like `'+UNION+SELECT+'abc','def'--`.
- Verify that the query is returning two columns, both of which contain text data.
5. **Retrieving Data from Users Table:**
- Use the payload `'+UNION+SELECT+username,+password+FROM+users--` to retrieve the contents of the users table.
- Verify that the application's response contains usernames and passwords from the users table.
6. **Logging in as Administrator:**
- Use the retrieved usernames and passwords to log in as the administrator user.

---

# Lab 10: SQL Injection UNION Attack, Retrieving Multiple Values in a Single Column

## Introduction:

This lab contains a SQL injection vulnerability in the product category filter of an application. The results from the query are returned in the application's response, allowing us to use a UNION attack to retrieve data from other tables. The objective is to perform a SQL injection UNION attack to retrieve all usernames and passwords from a table called users, and use this information to log in as the administrator user.

## Lab Objective:

The objective of this lab is to demonstrate the exploitation of a SQL injection vulnerability to retrieve user credentials stored in a different table called users. By using a UNION attack, we will construct a SQL injection payload to retrieve all usernames and passwords from the users table and concatenate them into a single column separated by a specific delimiter (~).

## Lab Procedure:

1. **Accessing the Lab:**
- Navigate to the provided lab URL to access the vulnerable web application.
2. **Identifying the Vulnerability:**
- Access the page containing the product category filter of the application.
- Observe the behavior of the application when filtering products by category.
3. **Intercepting the Request:**
- Open Burp Suite and configure it to intercept HTTP requests.
- Navigate to the page where the product category filter is applied.
4. **Determining the Number of Columns:**
- Modify the `category` parameter with a payload like `'+UNION+SELECT+NULL,'abc'--`.
- Verify that the query is returning two columns, with only one column containing text data.
5. **Retrieving Data from Users Table:**
- Use the payload `'+UNION+SELECT+NULL,username||'~'||password+FROM+users--` to retrieve the contents of the users table.
- Verify that the application's response contains usernames and passwords concatenated into a single column separated by the specified delimiter (~).
6. **Logging in as Administrator:**
- Extract the usernames and passwords from the concatenated column in the response.
- Use the retrieved usernames and passwords to log in as the administrator user.

---

# Lab 11: Blind SQL Injection with Conditional Responses

## Lab Objective:

The objective of this lab is to demonstrate the exploitation of a blind SQL injection vulnerability to retrieve the password of the administrator user. By manipulating the tracking cookie value and observing the presence or absence of the "Welcome back" message in the application's response, we can infer the results of the SQL query and extract the password character by character.

## Lab Procedure:

1. **Accessing the Lab:**
    - Visit the front page of the shop and use Burp Suite to intercept and modify the request containing the TrackingId cookie. Let's say the original value of the cookie is TrackingId=<id>.
2. **Exploiting the Blind SQL Injection Vulnerability:**
    - Modify the TrackingId cookie, changing it to:
        
        ```
        TrackingId=<id>' AND '1'='1
        ```
        
    - Verify that the "Welcome back" message appears in the response.
    - Change the TrackingId cookie to:
        
        ```
        TrackingId=<id>' AND '1'='2
        ```
        
    - Verify that the "Welcome back" message does not appear in the response.
    - Change the TrackingId cookie to:
        
        ```
        TrackingId=<id>' AND (SELECT 'a' FROM users LIMIT 1)='a
        ```
        
    - Verify that the condition is true, confirming the existence of the table users.
    - Change the TrackingId cookie to:
        
        ```
        TrackingId=<id>' AND (SELECT 'a' FROM users WHERE username='administrator')='a
        ```
        
    - Verify that the condition is true, confirming the existence of the user administrator.
3. **Determining the Password Length:**
    - Change the TrackingId cookie to:
        
        ```
        TrackingId=<id>' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>1)='a
        ```
        
    - Verify that the condition is true, confirming that the password is greater than 1 character in length.
    - Send a series of follow-up values to test different password lengths using Burp Intruder.
4. **Determining the Password Characters:**
    - Use Burp Intruder to send suitable payloads to test the character at each position of the password.
    - Launch the attack by clicking the "Start attack" button or selecting "Start attack" from the Intruder menu.
5. **Logging in as Administrator:**
    - Once the password characters are determined, log in as the administrator user using the obtained password.

---

# Lab 12: Blind SQL Injection with Conditional Errors

## Lab Objective:

The objective of this lab is to demonstrate the exploitation of a blind SQL injection vulnerability to retrieve the password of the administrator user. By manipulating the tracking cookie value and observing the application's response to different conditions, we can infer information about the database structure and extract the password character by character.

## Tools Used:

1. **Burp Suite:** Used for intercepting and modifying HTTP requests.
2. **Browser:** Used for accessing the vulnerable web application.

## Lab Procedure:

1. **Accessing the Lab:**
    - Visit the front page of the shop and use Burp Suite to intercept and modify the request containing the TrackingId cookie. Let's say the original value of the cookie is `TrackingId=<id>`.
2. **Exploiting the Blind SQL Injection Vulnerability:**
    - Modify the TrackingId cookie, appending a single quotation mark to it:
        
        ```
        TrackingId=<id>'
        ```
        
    - Verify that an error message is received.
    - Change the TrackingId cookie to two quotation marks:
        
        ```
        TrackingId=<id>''
        ```
        
    - Verify that the error disappears, indicating a syntax error.
    - Construct a subquery using valid SQL syntax:
        
        ```
        TrackingId=<id>'||(SELECT '' FROM dual)||
        ```
        
    - Verify that no error is received, indicating the use of Oracle database.
    - Test an invalid query with valid SQL syntax:
        
        ```
        TrackingId=<id>'||(SELECT '' FROM not-a-real-table)||
        ```
        
    - Receive an error, confirming the processing of injection as a SQL query.
    - Verify the existence of the users table:
        
        ```
        TrackingId=<id>'||(SELECT '' FROM users WHERE ROWNUM = 1)||
        ```
        
    - Confirm that no error is received, indicating the existence of the table.
    - Test a condition:
        
        ```
        TrackingId=<id>'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||
        ```
        
    - Receive an error, demonstrating conditional error response.
    - Check if the username administrator exists:
        
        ```
        TrackingId=<id>'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||
        ```
        
    - Confirm the existence of the user by receiving an error.
3. **Determining the Password Length:**
    - Test the password length:
        
        ```
        TrackingId=<id>'||(SELECT CASE WHEN LENGTH(password)>1 THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||
        ```
        
    - Continue testing different password lengths until the error disappears.
4. **Determining the Password Characters:**
    - Use Burp Intruder to test the character at each position of the password.
    - Launch the attack and review the results to determine the value of each character.
5. **Logging in as Administrator:**
    - Once the password characters are determined, log in as the administrator user using the obtained password.

---