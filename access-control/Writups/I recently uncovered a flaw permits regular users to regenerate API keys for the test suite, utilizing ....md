

![](https://miro.medium.com/v2/resize:fit:700/1*ylf9joAZ_fybMoR9g_V3XA.png)

> **Understanding Target**

Examkite(Virtual Name of bbp), a versatile continuous integration and delivery (CI/CD) platform, empowers development teams to streamline and automate their software delivery processes. This platform serves as the backbone for efficient collaboration, enabling teams to build, test, and deploy code seamlessly.

> **The Bug**

The vulnerability is a type of API access control concern, allowing regular users to exploit an API endpoint meant for higher-access users. This oversight may empower an attacker to perform actions beyond their intended capabilities. If exploited, an attacker could carry out unauthorized actions and enables regular Examkite users to regenerate an API key for the test suite through an API endpoint typically restricted to administrators.

> Before we move on, if you like my write-ups, please support me by clapping, sharing, and you can clap up to 50 times here on Medium, it’s free. Thank you.

## **Steps to Reproduce:**

1. Use two accounts one of admin and other of low level user.
2. Go to api key regeneration then click on generate.
3. Intercept the request and capture it.
4. Now go to low level user account.
5. Use the above captured request `POST /organizations/cdscs/analytics/suites/vdzdr/regenerate_api_key` with low level user.
6. Forward the request.
7. Now go to admin account and check the api key is get regerated.

> **The Bounty**

A bounty of $500 has been awarded for the responsible disclosure of this security vulnerability by Examkite team.

![](https://miro.medium.com/v2/resize:fit:252/1*zDTLq-cspVbaze1WaTetfA.png)

> **Takeaway**

This incident serves as a reminder for platform developers to consistently evaluate and reinforce access restrictions, safeguarding against potential breaches and ensuring the integrity of user actions.

> _Leave some clap if you enjoyed this read, leave your feedback in comment and consider following me for more exciting findings._

