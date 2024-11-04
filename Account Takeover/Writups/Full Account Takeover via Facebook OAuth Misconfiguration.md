
hello everyone!

Today, Imma share with y’all an interesting bug I found in one of Bugcrowd’s programs. It was in a program that had a “Login via Facebook” feature.

Grab your coffee, and let’s get started! 😉

So, in the target login page, and there it was an option to log in with Facebook.

![](https://miro.medium.com/v2/resize:fit:700/1*8Co05iBWJQdiDUiCQAsYWA.png)

I clicked on it and logged in. After that, I found myself on the page where I could edit the access permissions (you might see it as “ modify access permissions” or “Edit Access” ):

![](https://miro.medium.com/v2/resize:fit:700/1*BJzponAXnvhquqVMYTlLdQ.jpeg)

I clicked on it and I unchecked the checkbox that shares my email address with the app:

![](https://miro.medium.com/v2/resize:fit:700/1*PR_Ar2MWy-GSMMGn7EE73Q.png)

![](https://miro.medium.com/v2/resize:fit:700/1*ewkbAbDW3RmjJqeOiudh9Q.png)

then, I clicked Continue to proceed with the login without sharing my email. After disabling email sharing, the target site prompted me to provide an email address since it couldn’t retrieve it from Facebook.

![](https://miro.medium.com/v2/resize:fit:511/1*6RKNfmdmXMMLaY2POQi_RQ.png)

So, I entered the victim’s email address (and this step didn’t require any verification or proof of ownership). to my surprise, I got redirected straight to the victim’s account! Just like that, I took over the account!

![](https://miro.medium.com/v2/resize:fit:640/0*Tzl466bxArVWU5Jr)

but yeah, of course happy endings only happen in movies. My report was marked as a duplicate of another pre-account report submitted four days before me, saying it was the same root cause (OAuth misconfiguration).

![](https://miro.medium.com/v2/resize:fit:700/1*3DB844XchN-qbtJUZmww2w.jpeg)

# Lesson Learned!

Always verify user data after OAuth login. Make sure the system properly checks critical details like email addresses, even if they aren’t shared by the OAuth provider. Test how the system handles missing or altered data to prevent account takeovers and ensure user security.


