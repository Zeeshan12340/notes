# CSRF
Cross Site Request Forgery, known as CSRF occurs when a user visits a page on a site, that performs an action on a different site. For instance, let's say a user clicks a link to a website created by a hacker, on the website would be an html tag such as 

`<img src="https://vulnerable-website.com/email/change?email=pwned@evil-user.net">`  

which would change the account email on the vulnerable website to "pwned@evil-user.net".  CSRF works because it's the victim making the request not the site, so all the site sees is a normal user making a normal request.

Putting <img src="http://localhost:3000/transfer?to=alice&amount=100"> into an html file and using SimpleHTTPServer to host it should change's Alice's balance by 100, user clicks on our attacker website and a request if "forged" which completes some malicious process(change email, transfer money etc.,)