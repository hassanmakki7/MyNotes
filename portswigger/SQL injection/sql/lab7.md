# Lab: [SQL injection UNION](https://portswigger.net/web-security/sql-injection/union-attacks) attack, determining the number of columns returned by the query

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. The first step of such an attack is to determine the number of columns that are being returned by the query. You will then use this technique in subsequent labs to construct the full attack.

To solve the lab, determine the number of columns returned by the query by performing a SQL injection UNION attack that returns an additional row containing null values.

[ACCESS THE LAB](https://portswigger.net/academy/labs/launch/c0cf223d86b3189ea471d7a4dfe43987f9306dcd549be77599964da1b517b307?referrer=%2fweb-security%2fsql-injection%2funion-attacks%2flab-determine-number-of-columns)

#### Solution

1. Use Burp Suite to intercept and modify the request that sets the product category filter.
2. Modify the `category` parameter, giving it the value `'+UNION+SELECT+NULL--`. Observe that an error occurs.
3. Modify the `category` parameter to add an additional column containing a null value:
    
    `'+UNION+SELECT+NULL,NULL--`
4. Continue adding null values until the error disappears and the response includes additional content containing the null values.



