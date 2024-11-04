

![](https://miro.medium.com/v2/resize:fit:700/1*bW67FdB2p20_4uxTkuxsnw.png)

> **Understanding Target**

ExamFront (Virtual name Of a Private Program) stands out as a specialized space for managing deals, partnerships, and collaborations. This platform is designed to streamline the intricate processes involved in deal-making, offering a centralized hub for organizations to orchestrate their business agreements seamlessly.

> **The Flow**

Typically, when a user is created in the organization, they are granted all the default permissions. To remove these permissions, the organization requires the to obtain membership privileges. However, I have identified a flaw that enables an attacker to bypass this requirement and remove the user’s permissions directly through the UI.

> **The Flaw in the System**

At the heart of this issue lies a subtle manipulation of the user interface (UI). The organization and users of the organization can change the permissions without membership by directly enabling the buttons throught the UI. This flaw pertains to the manipulation of the user interface (UI), offering a unique pathway for unauthorized changes to user permissions. For betterunderstanding check the below steps and PoC:

> Before we move on, if you like my write-ups, please support me by liking, sharing, and clapping up to 50 times here on Medium, it’s free. Thank you.

> **Steps to Reproduce**

- Login to the ExamFront platform as a company user.
- Navigate to the user management section or any relevant area that controls user permissions.

![](https://miro.medium.com/v2/resize:fit:700/1*iWugPJVq4fHbG7tGkJKbMw.png)

- Locate the account for which you want to remove permissions.
- Select the “Access” option for the user.
- In the user’s settings, locate the access rights or permissions section.
- Identify the specific permission you want to remove and locate the associated disable button or toggle by inspect the element.

> PoC for better understanding :- [https://drive.google.com/file/d/1MmBzz-S4ABVv4-NMKAPGUewpgWGEPrhW/view?usp=sharing](https://drive.google.com/file/d/1MmBzz-S4ABVv4-NMKAPGUewpgWGEPrhW/view?usp=sharing)

- Remove the disable button for the targeted access right by modifying the UI code or altering the HTML elements.
- Now you are able to see that the select button that active for that permission.
- Now deselect the permission.
- Save the changes.

> **The Bounty**

In acknowledgment of uncovering the UI vulnerability within ExamFront, the bug bounty program has duly rewarded me a bounty of $750.

![](https://miro.medium.com/v2/resize:fit:252/1*dRYP5JFb7Iczp2jW3kNtMg.png)

> **Takeaway**

This discovery highlights how crucial it is to carefully examine user interfaces for cybersecurity. The main lesson is simple — small changes in the User Interface might seem harmless but can actually put user permissions at significant risk. Whether you’re a security researcher or a developer, it’s important to stay alert. Even a minor mistake in the UI can lead to serious consequences.

> _Leave some clap if you enjoyed this read, leave your feedback in comment and consider following me for more exciting findings._

![](https://miro.medium.com/v2/resize:fit:200/0*SBVpp4hqTeSFkfgL.gif)

> _Find me on Twitter:_ [_@a13h1__](https://twitter.com/a13h1_)

# Thank you everyone

Keep Supporting, Keep Clapping, Keep Commenting.

