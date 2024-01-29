# Requests--Burp
BurpSuite is used to intercept and modify web requests and to do other cool things.

Setup "foxyproxy" to intercept web requests.

Refer to [https://tryhackme.com/room/burpsuiteintruder](https://tryhackme.com/room/burpsuiteintruder) for credential brute-forcing involving CSRF tokens and session cookies.

Different attack types can be used, pretty self explanatory so nothing to mention.

_**Hashing in Decoder:**_

Decoder allows us to generate hashsums for data directly within Burp Suite; this works in much the same way as the encoding/decoding options we saw in the previous task. Specifically, we click on the "Hash" dropdown menu and select an algorithm from the list.

**Very Important:(file uploads, client-side filter)**
-----------------------------------------------------

When uploading a file that is blocked by a javascript script and but you're unable to completey block the script as it disables the website functionality we need too.

Intercept a request from the main website and keep forwarding requests until you reach the required js script, then right-click and “Do intercept -> response to this request” and then you should be able to modify it our purposes and forward it to the browser.