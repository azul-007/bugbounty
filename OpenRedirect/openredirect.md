# Open Redirects

Open redirects occur when a developer mistrusts attacker-controlled input to redirect to another site, via a URL parameter, 
HTML <meta> refresh tags or the DOM window location property

**Example 1**
Suppose Google had the functionality to redirect users to Gmail by visiting the following url:
```HTML
https://www.google.com/?redirect_to=https://www.gmail.com
```
The *redirect_to* parameter will reroute the intended url to whatever URL is submitted to it.

```HTML
https://www.google.com/?redirect_to=https://www.attacker.com
```
## HTML Redirect
When looking for these vulnerabilities, keep an eye out for URL parameters that include certain names, such as:
- *url=*
- *redirect=*
- *next=*
- *domain_name=*
- *checkout_url=*

Redirect parameters might not always be obvious, they will vary from site to site. Parameters might be labeled with just single characters
such as r= or u=.


HTML <meta> tags and JavaScript can redirect browsers. <meta> tags can tell browsers to refresh a web page and make a GET request to a URL
defined in the tag's content attribute.
``` HTML
<meta http-equiv="refresh" content="0"; url=https://www.google.com/>
```
The content attribute defines how browsers make an HTTP request in two ways:
- Defines how long the browser waits before making the HTTP request to the URl; 0 seconds
- Specifies the URL parameter in the website the browser makes the GET request to; google.com

## JavaScript Redirect
JavaScript can also be used to modify the window's *location* property through the *Document Object Model (DOM)* - an API for HTML and XML 
documents that allows developers to modify the structure, style and content of a web page. The location property denotes where a request should be
redirected to.

```JavaScript
window.location=https://www.google.com/
window.location.href=https://www.google.com/
window.location.replace(https://www.google.com)
```

Opportunities to set the window.location value occur only where an attacker can execute JS, either via XSS or where the website intentionally allows
users to define a URL to redirect to.

When you're searching for open redirect vulns, you'll be monitoring your proxy history for a GET request sent to the site you're testing that includes a 
paramets specifying a URL redirect.
