The last thing I was checking was the reset password page so let’s dig into it i went to the reset password page and tried to enter my email address and reset it until here there is no problem

![](https://miro.medium.com/v2/resize:fit:700/1*W6DtdILFNpPS8kMxeKD9pA.png)

The email address reset password

usually, I open the console and the local storage and cookie to check the data saved into it so I opened it and found some field called user_email

![](https://miro.medium.com/v2/resize:fit:700/1*dsQmDWC1Ci5oQ5h27Bkrqw.png)

and the value of it was my email I reset the password for it so I tried to change it to check if the value of the email in the page was taken from this local storage field and when I changed it changed in the page.

![](https://miro.medium.com/v2/resize:fit:700/1*pGgCWF_-z3t-WucjHzVc-w.png)

after I changed the local storage to the attacker's mail

so I thought it might be trying to inject anything but after one minute I told myself even if I injected anything it’s self so I clicked on the button to resend the email with dead hope but guess what? I got the reset link for the victim mail to the new mail I put in the local storage!!!!!!!!!!!!!!!

So let’s reproduce the bug:

1. go to the reset password link and put the victim's mail
2. after the first link goes to the victim's mail open the console and change the user_email to the attacker's mail
3. reload and resend the mail
4. open the attacker's mail and use the link to reset the victim's password
![](https://miro.medium.com/v2/resize:fit:700/1*tvOdIhg6tvfnoxXpz56MXg.png)

So let’s talk about this weird behavior :

the app when you make the reset password action returns the user data in some field called token in the local storage so when the user hits the resend email it should send the email to the email stored in that token but what the app does is get the email value from the user_email and send it to the user id stored in the token.


