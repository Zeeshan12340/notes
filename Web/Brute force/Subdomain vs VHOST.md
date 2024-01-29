# Subdomain vs VHOST
For VHOST fuzzing:

```text-plain
wfuzz -c -z file,/usr/share/wordlists/wfuzz/general/common.txt -u "http://undiscovered.thm/" -H "Host: FUZZ.undiscovered.thm" --hw 26
```

`-c` is for colours, `-z` is for scan mode, 

A subdomain is a DNS thing -- it's a record that points at an IP address. A virtual host is a software thing -- a feature in webservers that allows them to host multiple sites differentiated by their hostname.

Say you have a domain: `example.com` You create a subdomain: `sub1.example.com` and set an A record (basically a forward lookup address) of 1.2.3.4 -- which is an IP address that is assigned to a webserver that you own.

Any traffic directed at sub1.example.com will now go to the server at 1.2.3.4 (that is a subdomain)

But what happens with the webserver? It's fine if there's only one site on the server -- it just serves the default one to anyone who connects, and all good, but what happens if you have two sites? Say you have another domain: `exampletwo.org` that also points at 1.2.3.4 -- how does the server know to serve the site for exampletwo.org when people connect using that domain, and the site for sub1.example.com when people connect using _that_?

That is VHosting -- when the webserver is set up to serve different content depending on the "host" (in this case, domain/subdomain).