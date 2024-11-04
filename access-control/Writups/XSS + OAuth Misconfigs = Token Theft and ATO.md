
all, In this blog post, I will walk through finding an ATO via OAuth misconfigurations and stealing Auth Tokens through collaborative work with my friends [Ynoof](https://app.intigriti.com/profile/ynoof) and [Refaat](https://bugcrowd.com/refaat1)

![](https://miro.medium.com/v2/resize:fit:700/1*O-y1mscdPbL4Nv0g92bikw.png)

The story begins with finding XSS at `sub1.target.com` The problem was that the program was paying lower bounties for this subdomain, so our target was to escalate this XSS to ATO on the main target app `app.target.com`since the program was paying much more for this subdomain.

Looking at the auth mechanism of `sub1.target.com`, we found that it was authenticated via a `cookie-based JWT token`, while the auth mechanism in `app.target.com` was via an `Authorization header-based JWT`. The JWT value on the two subdomains was different, but surprisingly, the JWT from `sub1.target.com` worked for authentication on `app.target.com`!

So, if we could leak the JWT auth token from `sub1.target.com`, we could use it for authentication on `app.target.com`.

![](https://miro.medium.com/v2/resize:fit:561/1*B6hZoZQt2_YcpB2hr5dWWQ.png)

Unfortunately, the cookie-based JWT token on `sub1.target.com` was protected with an `HttpOnly` flag, so it wasn't possible to access it via the XSS. However, during our analysis of the target’s oauth flow, we found another way to leak these JWT tokens!

We found this request, which had the JWT token in the response from another subdomain, `auth.target.com`.

![](https://miro.medium.com/v2/resize:fit:700/1*VDXMc64SmUwTDEjCeLih2A.png)

After further analysis, we found interesting behavior on the previous request. We found that if we changed the `response_mode` parameter value from `post` to `get`, the response will be different. Additionally, we could set any value for the `state` and `nonce` parameters and the server would still return the auth token.

![](https://miro.medium.com/v2/resize:fit:700/1*0ld_xTa3SUw4Xm4CF8Z3MQ.png)

Now with the XSS in `sub1.target.com`, we can create an iframe that loads the OAuth endpoint on `auth.target.com`. Fortunately there weren't any `X-Frame-Options` or `CSP` in place to prevent framing of this endpoint, However, the SOP will prevent access to the `contentWindow` object of an iframe from a different origin.

We considered if both subdomains set `document.domain = 'target.com'`, putting them into the "same origin" state.

> This technique was used to relax SOP between subdomains under the same second-level domain. If both subdomains explicitly set the `document.domain` property to the parent domain `domain.com`, they will share the same origin, allowing cross-origin access.

However, this technique is no longer supported by modern browsers like [chrome](https://developer.chrome.com/blog/immutable-document-domain/)

Instead, we found that CORS was configured to allow access between these subdomains, which enabled us to capture the token via the URL fragment `location.hash`.

var auth = document.createElement('iframe');  
xe.setAttribute('src',' https://auth.target.com/oauth?client_id=redacted&redirect_uri=https://auth.target.com/endpoint.jsp&response_mode=get&response_type=code&scope=redacted&state=redacted&nonce=redacted');  
auth.setAttribute('id','lol')  
token = new URLSearchParams(document.getElementById("lol").contentWindow.location.hash.split('#')[1]).get('token');

After initiating the request to get the token fragment from the URL, we can send it to the attacker’s server.

Since the JWT auth token was stolen from the authentication flow at `auth.target.com` using XSS on `sub1.target.com`, we can then include the stolen JWT auth token in requests to change victims' email addresses on `apps.target.com`to achieve ATO.

![](https://miro.medium.com/v2/resize:fit:700/1*IyAALMrBvaS60md5LTFXCw.png)

> The full attack flow can be shown as following:

![](https://miro.medium.com/v2/resize:fit:700/1*O-y1mscdPbL4Nv0g92bikw.png)

That was all for this write-up! If you have any questions or feedback, please don’t hesitate to DM me on [**LinkedIn**](https://www.linkedin.com/in/7odamoo/) or [**Twitter**](https://twitter.com/7odamoo). See you in the next write-up!

[

](https://medium.com/tag/bug-bounty?source=post_page-----d0837c44cd31--------------------------------)

