After testing the core functionalities, I decided to investigate the hosted stores more deeply. Each store offers a URL that is customized for its users, including login and account management features. One such URL I explored was `https://3adwy-store.xyz.com/products/account`, which provided a login page that sends users an email with a link to log in securely.

After some investigation to understand how these login emails were being sent, I discovered that the emails are sent by the server. But this raised another question: **How does the server know which store to reference in the signature of the email?**

Finally, I found the critical endpoint that handles these emails and noticed there were **no cookies or authorization headers** in the request. HOW?!

![](https://miro.medium.com/v2/resize:fit:700/1*9E7EIY-FJnl0i8Cedr-RPw.png)

## Analysis time

in this request there is three critical fields in this request

- **Store ID**: The unique identifier for the target store (e.g., `107527149`).
- **Victim’s Email**: The email address where the sign-in link is sent.
- **siteUrl(store url)**: The URL used for sign-in redirection.<our vulnarable paramater 👾>

When I tested the `siteUrl` parameter, I found that there was **no validation** on it, and it would be directly included in the email sent to the victim. So now, we have a valid malicious link in the victim's mailbox.

This is already a valid bug, but I wanted to add some creativity, so let’s move on to the more interesting part of this story 🥱.

## Fun Time: Breaking It Down

In the email, there’s a key parameter in the link that acts like a token for one-time use for logging in. This key is essential because it allows a user to securely log in without needing their password.

Now, the question is: **If we send a malicious link, will the key parameter be sent to our malicious website?**

before you go with your mind, key will be sent to our malicious website but in with little different structure

**After analyzing the behavior, I figured out how the developer handles this:**

1. **Valid Request:**

- The developer retrieves the **store URL** from the database by **Store ID**.
- Compares it with the **siteUrl** parameter from the request.
- If it matches, a login token for the user is generated and added to the `key` parameter in the URL:

> [https://ahmed--store.xyz.com/products/account?key=generated_value](https://ahmed--store.xyz.com/products/account?key=generated_value)

![](https://miro.medium.com/v2/resize:fit:700/1*An-4_4ZmpZQPI55NWRkm6Q.png)

mail example

**2. Invalid/Malicious Request:**

- If the `siteUrl` parameter does not match the real store URL for the given Store ID, a token is still generated, but for some security 😁 it is not placed in the parameter. Instead, it's put in the hash query:

> `[https://fake--store.xyz.com/#!/~/account/key=fZAtATZNYbVG](https://fake--store.xyz.com/#!/~/account/key=fZAtATZNYbVG)`

![](https://miro.medium.com/v2/resize:fit:635/1*WdcxZ2LShECPD9KfG5l_JA.png)

From this, we know that if we use our malicious website, we won’t get the key parameter directly. I tried this with Burp Collaborator and, unfortunately, didn’t receive any parameters.

# Creativity Time: The JavaScript Solution

I didn’t get frustrated! Instead, I used some creativity.

I built my own server and tested if I could capture the key. Initially, I had no luck, but I thought of a new approach: **extract the key from the hash query using JavaScript**.

Here’s how it worked:

`<script>  
// Function to extract the key from the URL hash  
function getKeyFromHash() {  
    // Get the full hash from the URL  
    const hash = window.location.hash;  
    console.log('Hash:', hash);  
  
    // Check if the hash contains the 'key' parameter  
    if (hash.includes('key=')) {  
        // Extract the 'key' value from the hash  
        const key = hash.split('key=')[1];  
        console.log('Extracted Key:', key);  
  
        // display it to my test or send it to a server to store it  
        document.getElementById('keyDisplay').textContent = `Key: ${key}`;  
    } else {  
        console.log('Key not found in hash.');  
    }  
}  
  
// Run the function after the page loads  
window.addEventListener('load', getKeyFromHash);  
`</script>

With this code, the attacker can extract the token to log into the victim’s account and potentially change their email, view their orders, balance, and more. This results is a **full account takeover**.
