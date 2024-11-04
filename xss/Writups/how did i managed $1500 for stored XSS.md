


Hi i am aman-singh bug bounty hunter security researcher 🥀. because of college issues life is very unbalanced. that why i am unable to wrote write up. but i am back again with another fresh writeup.

**let’s start**

![](https://miro.medium.com/v2/resize:fit:480/1*kGrS8Hai8A8-nwIvdbHBPg.gif)

In jan 2024, i picked a private programe. i can’t reveal the original name of the website . let’s call it evil.com. so the website is very popular and they used **_to schedule meetings, appointments, and events for individuals and organizations_**_._

> **let me explain first what is cross site scripting vulnerability those who don’t know.**

cross site scripting is client side vulnerability that allows an attacker to inject malicious code into a web page viewed by other viewed by other users, usually in a script. When other users view the compromised page, the injected code can execute and steal sensitive information or perform malicious actions on their behalf.using this vulnerability attacker can takeover any victim account.

**Finding**

i was hunting since last month and test all the fields but i didn’t get anything after next day i woke up and again try my luck so i already told you the website is event base. so i created a event and set the text reminder . In text reminder i put a XSS payload:- ”><img src=x onerror=alert(document.cookie)>” after save the text reminder .immediately i got XSS POP which means xss was successfully execute in the website.

![](https://miro.medium.com/v2/resize:fit:700/1*oKcGOAgyNr8GCMoHElLL8A.png)

stored xss pop image

so without wasting any time i reported a clean report hackerone team.

STEP THAT I HAD REPRODUCE:

1: navigate to home page :- [https://evil.com/event_types/user/me](https://calendly.com/event_types/user/me).

2: click on event after open up.

3: click on Communication section. you will get basic notifications.

4: click edit on Text reminders. & add basic paylaod `“><img src=x onerror=alert(document.cookie).

5: save and close. payload will triggred.

after next day hackerone triage team replied me and said “_We were able to validate your report, and have submitted it to the appropriate remediation team for review_”

after one week company rewarded me bounty.

![](https://miro.medium.com/v2/resize:fit:700/1*Jbeq60M7Vk9TkzxWtaZeng.png)