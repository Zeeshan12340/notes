# Nabbing
Reverse Tab Nabbing
-------------------

In a situation where an **attacker** can **control** the `**href**` argument of an `**<a**` tag with the attribute `**target="_blank" rel="opener"**` that is going to be clicked by a victim, the **attacker** **point** this **link** to a web under his control (a **malicious** **website**). Then, once the **victim clicks** the link and access the attackers website, this **malicious** **website** will be able to **control** the **original** **page** via the javascript object `**window.opener**`. If the page doesn't have `**rel="opener"**` **but contains** `**target="_blank"**` **it also doesn't have** `**rel="noopener"**` it might be also vulnerable.

A regular way to abuse this behaviour would be to **change the location of the original web** via `window.opener.location = https://attacker.com/victim.html` to a web controlled by the attacker that **looks like the original one**, so it can **imitate** the **login** **form** of the original website and ask for credentials to the user.