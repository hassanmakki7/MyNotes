
# What is null byte character?

> A null byte, often represented as ‘\0’, is a special character with a value of zero. In programming, it’s used to indicate the end of a string or data. Null byte injection involves manipulating this character to exploit vulnerabilities in a system.

# Password Reset Parsing confusion

i was testing this cdn application and decided to test the password reset functionality and i found a very interesting parameter called callbackUrl.

![](https://miro.medium.com/v2/resize:fit:700/1*-Sz7dqKreL8ciooJF7SjDg.png)

when i attempted to reset the password i attemped to to append /test at the end of the url and checked my email and i got the following url:

https://company.com/auth/reset-password/test?code=blabla

so i quickly tried to change domain in the callbackUrl to evil.com but unfortunately Got 400 Bad request status code

![](https://miro.medium.com/v2/resize:fit:561/1*mHFxdMSBSEPpGvhdXdJ_jg.png)

i got really frustrated but nevertheless i decided to spend some time on it since being able to control some parts of the password-reset **callbackUrl** was a red flag for me

![](https://miro.medium.com/v2/resize:fit:639/1*t8fGJNX5z1VmUhr-vxokPA.png)

> _Here aresome of the payloads that i tried_
> 
> [_http://evil.com@company.net/auth/reset-password_](http://evil.com@company.net/auth/reset-password)
> 
> [_http://evil.com%20@company.net/auth/reset-password_](http://evil.com%20@company.net/auth/reset-password)
> 
> [_http://evil.com\@company.net/auth/reset-password_](http://evil.com%20@company.net/auth/reset-password)
> 
> [_http://evil.com?@company.net/auth/reset-password_](http://evil.com%20@company.net/auth/reset-password)
> 
> [_http://evil.com#@company.net/auth/reset-password_](http://evil.com%20@company.net/auth/reset-password)

And many more they all returned

400 status code . then i had an idea to try null byte injection but since this a json request i can’t just insert the regular url encoded %00 so i did a little bit of research and read about the json RFC and figured out that i can insert unicode characters using the \u sequence

![](https://miro.medium.com/v2/resize:fit:595/1*oVUfxvvE4eZuIea0KNk3XQ.png)

> a string containing only a single reverse solidus character may be represented as \u005C

in this case the equivalent of url null byte character %00 in unicode is \u0000

So i tried this payload

> https://evil.com\u0000@company.net

![](https://miro.medium.com/v2/resize:fit:700/1*SlBiNSH6J7jsoLKjs4RLQQ.png)

![](https://miro.medium.com/v2/resize:fit:312/1*53rm1KAGwROMR9EJjWgwpQ.png)

And whola it worked!

# Path Traversal To XSS

in this app, i was fuzzing for some hidden params using param miner and param miner returned a parameter caught my eye immediately called templatename quickly requested it with the value of templatename=0xold and checked the server response

![](https://miro.medium.com/v2/resize:fit:700/1*bz-bUnCXGw42H6VhRDIU2g.png)

Encountered a 500 internal error, indicating a server-side issue on the backend. My initial assumption was that the server tried to include the file “0xold,” but the attempt failed, resulting in the 500 error — suggesting a potential Local File Inclusion (LFI). Before proceeding, I opted to investigate the operating system the website operates on before trying to inject any payload.

I Ran the following Command to identify the os

> nmap -A Company.com

![](https://miro.medium.com/v2/resize:fit:676/1*f42OJc-8YRQlyqudhbx8xQ.png)

So now we know that the website is running on windows we can now proceed and inject lfi windows payloads

I started off by injecting payloads such as

> login.asp
> 
> logout.asp
> 
> ../login.asp
> 
> ..\login.asp
> 
> ….//login.asp
> 
> ….//login.asp%00
> 
> ….\\login.asp
> 
> ../../windows\win.ini
> 
> ..\..\windows\win.ini

and hundreds of payloads i even ran json-haddix lfi’s wordlist from seclist repo nothing really worked all resulted in a 500-status code. i then decided to take a break and think a little bit about it. then i thought maybe the developer was doing some kind of whitelisting and returns a 500 status error if the templatename parameter isn’t in the whitelist to verify my theory i decided to use the tool cewl to generate a custom wordlist.

## What is Cewl

> CeWL (Custom Word List generator) is a ruby app which spiders a given URL, up to a specified depth, and returns a list of words which can then be used for password crackers such as John the Ripper. Optionally, CeWL can follow external links.

I Ran the following command to generate a wordlist

> cewl ‘https://company.net’ > wordlist

then

> ffuf -c -w wordlist -u ‘https://company.net/login.asp?templatename=FUZZ’ -mc all -fc 500

One of the values returned 200 OK status code ! It was the company’s name all along!

![](https://miro.medium.com/v2/resize:fit:700/1*o39QOoc2WacN9U8iVYWUdA.png)

![](https://miro.medium.com/v2/resize:fit:700/1*KiQhAJQ8YMOxN0JXhmjnlA.png)

the parameter value was being reflected in the http response so i decided to try inject some xss but still anything that doesnt equal the company’s name will return 500 STATUS code. how can we exploit it? Maybe using the ../ sequence? so i injected the following value in the templatename param and checked the response

company.com/0xoldSaysHi/../

![](https://miro.medium.com/v2/resize:fit:557/1*2_2k9syItqrhq9lv2qm1lA.png)

Awesome It worked! lets try to inject some xss now

i injected this simple payload to see if i can escape out of the html

> company/0xoldSaysHi”>/../

![](https://miro.medium.com/v2/resize:fit:522/1*XfXnyUNCLl-g3eUSqalCjg.png)

i was able to inject the double quote characters but the > characters wasn’t being refelected for some reason so i tried to inject null byte character after the > character to see what will happen

> company/0xoldSaysHi”>%00/../

![](https://miro.medium.com/v2/resize:fit:524/1*eRFh7CTaCEitIM-sGZXMsg.png)

It worked!! lets to pop up an alert real quick

> company/0xoldSaysHi”%00><%00img+src=x+onerror=alert(1337)%00>/../

![](https://miro.medium.com/v2/resize:fit:649/1*vb4qFDYycDvAn5QXE-6wTw.png)

# Bypassing an internal WAF through null byte injection

I was testing this app for sql injection and by throwing a regular ‘ in the error_category param the website returned a db error indicating that it is vulnerable to sql injection cool! i will just save the request and run sqlmap and let it do all the hardwork

![](https://miro.medium.com/v2/resize:fit:700/1*xqhW9ujP2dTz1U7CDPp2XA.png)

Saved the request to a file called r and ran the following command

python3 sqlmap.py -r r — batch — dbs — random-agent

![](https://miro.medium.com/v2/resize:fit:700/1*ttTtyIEWneIK-jOgB1i0pQ.png)

Shortly After sqlmap returned a connection time out i initially though the application couldn’t handle the number of requests that sqlmap sent and it went down. i ran a simple curl returned connection failed. tried it from my pc it works hmm maybe there are some kind of internal waf? i decided to exploit it manually through my pc it is not a big deal since it is an error based-SQLI

tried a simple union query ‘UNION+SELECT+1337 — — the server was hanging so i changed query to UnION/**/sElect+1337 still hangs tried to change the value to ‘test+test+1337 — — return a db error so after a little bit of trial and error i figured out how does their internal waf work. the waf was parsing the http requests and if it finds a malicious query it hangs and if i submitted 3 requests in a row and it hanged it will block my ip.

![](https://miro.medium.com/v2/resize:fit:700/1*4fQnB4M_-_4J8riP1WUqhQ.png)

Tried to inject null byte between each mysql keyword to confuse their WAF and it worked then after getting the db names i injected the following payload to get all the tables in the admin database

> f’+/**/UNION+%00seLecT+%00TABLE_NAME,TABLE_schema,NULL,NULL,NULL,NULL+FROM+%00INFORMATION_SCHEMA.tables+WHERE+table_schema=’AdminDB’%23

![](https://miro.medium.com/v2/resize:fit:700/1*4u0iN_nkEuV6IIX8yeORvg.png)

> Twitter: [https://twitter.com/0x0ld](https://twitter.com/0x0ld)
> 
> Hackerone: [https://hackerone.com/0xold](https://hackerone.com/0xold)


