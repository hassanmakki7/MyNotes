
# Lab: [SQL injection](https://portswigger.net/web-security/sql-injection) attack, querying the database type and version on Oracle
This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query.

To solve the lab, display the database version string.

#### Solution

1. Use Burp Suite to intercept and modify the request that sets the product category filter.
2. Determine the [number of columns that are being returned by the query](https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns) and [which columns contain text data](https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text). Verify that the query is returning two columns, both of which contain text, using a payload like the following in the `category` parameter:
    
    `'+UNION+SELECT+'abc','def'+FROM+dual--`
3. Use the following payload to display the database version:
    
    `'+UNION+SELECT+BANNER,+NULL+FROM+v$version--`

