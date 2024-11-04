
A few months ago, I received an invitation to a private bug bounty program on **HackerOne**. Initially, I did my usual testing and I discovered and reported various bugs, such as BAC, leaking Authorization Tokens of other users, etc...

After reporting these bugs to the program, I noticed that XSS is considered Out Of Scope according to their policy. The program business is “_an online content management system and website builder”._ Upon creating an account, users receive a unique subdomain like `<YOUR-SUB>.target.com`that can be customized.

Considering the app’s structure, XSS is limited to being self, and the program excludes XSS on `<YOUR-SUB>.target.com` from their scope. This encouraged me to explore finding a self-XSS and chaining it with another bug to show an Impact.

**I discovered several chains for XSS that escalated its impact. Since there is only one resolved XSS chain report, I will only write a write-up about it. When the other reports are resolved, I plan to write separate write-ups for each of them. Now, let’s dive into the story.**

Finding Self-XSS didn’t take much time.

![](https://miro.medium.com/v2/resize:fit:700/1*SuzimnuUPcVcVZBia6XBWw.png)

Out-Of-Scope XSS

Now, it’s time to find another bug to chain with XSS. I began testing the website with the goal of identifying bugs to chain with the XSS. One of the bugs I tested for was CORS misconfiguration. I prefer testing it using the [**CORS* Burp Extension**](https://portswigger.net/bappstore/420a28400bad4c9d85052f8d66d3bbd8)**.**

![](https://miro.medium.com/v2/resize:fit:700/1*yCu2QpgXpgq1J4Te7aa4IA.png)

CORS* Burp Extention

To use this extension, simply click on the “**_Activate CORS* checkbox”_** and browse your target to let the extension do its magic. It will attempt different CORS bypass techniques for all requests passing through your Burp proxy. All you need to do is to check the results.

![](https://miro.medium.com/v2/resize:fit:700/1*CnNMYbohWLqJA_RqRKTubQ.png)

CORS* Burp Extension Results

After activating the extension I found a possible CORS misconfiguration in `www.target.com/api/me`. This API request is responsible for fetching user PII such as **_first name, last name, email, and account ID_**_._

> When sending a request with

Origin: 7odamoo-target.com

> The response was

Access-Control-Allow-Credentials: true  
Access-Control-Allow-Origin: 7odamoo-target.com

![](https://miro.medium.com/v2/resize:fit:700/1*P3GRl_x6Axp2geTXr30D3w.png)

CORS Misconfiguration

Awesome, seems I got a bug now, in normal cases I should register the domain `7odamoo-target.com`and upload a **_CORS PoC_** on it to show the exploit to the team, but when I checked the cookie flags I found that the problem was in the [**_SameSite cookie_ _flag_**](https://owasp.org/www-community/SameSite)**. T**he browser would not include the cookie in the request unless the origin is allowed.

I think you get what I will do next, I will use the Out-Of-Scope XSS to send the request so the cookie will be included.

So I Injected this script on my own subdomain `<MY-SUB>.target.com` so when anyone visits my subdomain a request will be sent to `www.target.com/api/me`and his PII will be displayed on an alert Popup as a PoC

function cors() {  
  var xhttp = new XMLHttpRequest();  
  xhttp.onreadystatechange = function() {  
    if (this.readyState == 4 && this.status == 200) {  
      document.getElementById("demo").innerHTML = alert(this.responseText);  
    }  
  };  
  xhttp.onload = cors;  
  xhttp.open("GET", "https://www.target.com/api/me", true);  
  xhttp.withCredentials = true;  
  xhttp.send();  
}  
cors();

![](https://miro.medium.com/v2/resize:fit:700/1*OSMlOVIgncqcabsFtAlkzg.png)

Bypass the SameSite Cookie using Self XSS

Cool, I successfully chained the CORS Misconfiguration with the Out-Of-Scope XSS to bypass the origin check for the SameSite cookie.

The team promptly addressed the vulnerability by fixing the CORS misconfiguration, as they no longer allowing `*.target.com`to read the response from `www.target.com`

![](https://miro.medium.com/v2/resize:fit:700/1*CPwaOJDsrU_3GCoVEkSarg.png)

CORS Misconfiguration Fix

As highlighted earlier in the write-up, once the remaining XSS chains are resolved, I’ll write separate write-ups for each of them.

That was all for this write-up! If you have any questions or feedback, please don’t hesitate to DM me on [**LinkedIn**](https://www.linkedin.com/in/7odamoo/) or [**Twitter**](https://twitter.com/7odamoo). See you in the next write-up!

