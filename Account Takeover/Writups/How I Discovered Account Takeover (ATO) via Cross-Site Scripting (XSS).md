## Free Article


](https://medium.com/@jeetpal2007 "An Ethical hacker Bug hunter & Developer Connect me on social media via https://linktr.ee/jeetpal2007 query:jeetpal2007@gmail.com")

[JEETPAL](https://medium.com/@jeetpal2007 "An Ethical hacker Bug hunter & Developer Connect me on social media via https://linktr.ee/jeetpal2007 query:jeetpal2007@gmail.com")

androidstudio · October 12, 2024 (Updated: October 12, 2024) · Free: No

Hello everyone,

Today, I want to share my experience of discovering an account takeover (ATO) vulnerability through Cross-Site Scripting (XSS). Let's dive right in!

While hunting for a program with millions of users — specifically a large blog website, which I'll refer to as redacted.com — I began by enumerating its subdomains. One subdomain I found was **jp.redacted.com**.

Next, I utilized Param Spider to gather all possible parameters. The command I used was:

```css
param spider -d jp.redacted.com -s  (to list in the terminal all possible parameters0
```

This command listed all possible parameters in the terminal. Among them, I discovered a parameter called **s=**, which allowed me to execute reflected XSS (RXSS) with a simple payload:

```xml
alert(1)
```

![None](https://miro.medium.com/v2/resize:fit:700/1*RoZet6wDPJj_WVBnv9x3iQ.png)

RXSS

Once I got I tried to escalate it to the ATO using a simple payload

However, this approach did not work, and I tried numerous payloads without success. After some experimentation, I decided to encode my payloads in Base64 before inputting them. To my surprise, this resulted in the payload being executed on the site, and I successfully captured victim cookies.

![None](https://miro.medium.com/v2/resize:fit:700/1*Y2y1BGAfk8SIIUha_AuRMQ.png)

ATO Via RXSS

I reported the ATO vulnerability via RXSS to the team, but unfortunately, I have not received a response in the last five months.

Thank you for reading if you enjoy it clap 50 times

connect me on social media via:[https://linktr.ee/jeetpal2007](https://linktr.ee/jeetpal2007)