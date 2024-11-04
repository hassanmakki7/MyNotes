
# Lab: [Blind SQL injection](https://portswigger.net/web-security/sql-injection/blind) with time delays


This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information.

To solve the lab, exploit the SQL injection vulnerability to cause a 10 second delay.


#### Solution

1. Visit the front page of the shop, and use Burp Suite to intercept and modify the request containing the `TrackingId` cookie.
2. Modify the `TrackingId` cookie, changing it to:
    
    `TrackingId=x'||pg_sleep(10)--`
3. Submit the request and observe that the application takes 10 seconds to respond.


