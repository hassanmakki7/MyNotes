
## Introduction

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/OAuth%20Misconfiguration.md#introduction)

The most infamous OAuth-based vulnerability is when the configuration of the OAuth service itself enables attackers to steal authorization codes or access tokens associated with other users’ accounts. By stealing a valid code or token, the attacker may be able to access the victim's account.

## Where to find

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/OAuth%20Misconfiguration.md#where-to-find)

In the SSO feature. For example the URL will be looks like this

```
https://example/signin?response_type=code&redirect_uri=https://callback_url/auth&client_id=FQ9RGtMkztAgmAApKOqACrBNq&state=7tvPJiv8StrAqo9IQE9xsJaDso4&scope=+profile+email+phone+group+role+resource
```

## How to exploit

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/OAuth%20Misconfiguration.md#how-to-exploit)

- OAuth token stealing by changing `redirect_uri` and Use IDN Homograph
    
    - Normal parameter
        
        ```
        &redirect_uri=https://example.com
        ```
        
IDN Homograph

```
&redirect_uri=https://еxamplе.com
```

- If you notice, im not using the normal `e`
    
- Create an account with [victim@gmail.com](mailto:victim@gmail.com) with normal functionality. Create account with [victim@gmail.com](mailto:victim@gmail.com) using OAuth functionality. Now try to login using previous credentials.
    
- OAuth Token Re-use.
    
- Improper handling of state parameter
    
    To exploit this, go through the authorization process under your account and pause immediately after authorization. Then send this URL to the logged-in victim
    
    - CSRF Attack
        
        ```html
        <a href="https://example.com/authorize?client_id=client1&response_type=code&redirect_uri=http://callback&scope=openid+email+profile">Press Here</a>
        ```
        
- Lack of origin check.
    
- Open Redirection on `redirect_uri` parameter
    
    - Normal parameter
        
        ```
        &redirect_uri=https://example.com
        ```
        
Open Redirect

```
&redirect_uri=https://evil.com
&redirect_uri=https://example.com.evil.com
etc.
```

1. If there is an email parameter after signin then try to change the email parameter to victim's one.
    
2. Try to remove email from the scope and add victim's email manually.
    
3. Check if its leaking `client_secret`
    

## References

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/OAuth%20Misconfiguration.md#references)

- [tuhin1729_](https://twitter.com/tuhin1729_/status/1417843523177484292)
- [c0d3x27](https://infosecwriteups.com/the-oauth-misconfiguration-15e66dd19a6e)

