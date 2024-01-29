# cryptography
Ciphers
-------

If unsure what cipher it is, best to throw it in a bunch of cipher identifiers before randomly bruteforcing different algorithms, 

cyberchef, [https://www.dcode.fr/cipher-identifier](https://www.dcode.fr/cipher-identifier) , [https://www.boxentriq.com/code-breaking/text-analysis](https://www.boxentriq.com/code-breaking/text-analysis)are good starting points.

Scytale Cipher, old greek cipher.

Diffie-Hellman Exchange:
------------------------

[https://www.dcode.fr/diffie-hellman-key-exchange](https://www.dcode.fr/diffie-hellman-key-exchange) 

[https://pequalsnp-team.github.io/writeups/crypto300\_1](https://pequalsnp-team.github.io/writeups/crypto300_1) 

```text-plain
p = 9975298661930085086019708402870402191114171745913160469454315876556947370642799226714405016920875594030192024506376929926694545081888689821796050434591251
g = 7
a = 330
b = 450
g_c = 6091917800833598741530924081762225477418277010142022622731688158297759621329407070985497917078988781448889947074350694220209769840915705739528359582454617

A = (g ** a) % p
B = (g ** b) % p

secretA = (B ** a) % p
secretB = (A ** b) % p

print(secretA,secretB)
```

Diffie–Hellman key agreement is not limited to negotiating a key shared by only two participants. Any number of users can take part in an agreement by performing iterations of the agreement protocol and exchanging intermediate data (which does not itself need to be kept secret). For example, Alice, Bob, and Carol could participate in a Diffie–Hellman agreement as follows, with all operations taken to be modulo _p_:

1.  The parties agree on the algorithm parameters _p_ and _g_.
2.  The parties generate their private keys, named _a_, _b_, and _c_.
3.  Alice computes _ga_ and sends it to Bob.
4.  Bob computes (ga)b = _gab_ and sends it to Carol.
5.  Carol computes (gab)c = _gabc_ and uses it as her secret.
6.  Bob computes _gb_ and sends it to Carol.
7.  Carol computes (gb)c = _gbc_ and sends it to Alice.
8.  Alice computes (gbc)a = _gbca_ = _gabc_ and uses it as her secret.
9.  Carol computes _gc_ and sends it to Alice.
10.  Alice computes (gc)a = _gca_ and sends it to Bob.
11.  Bob computes (gca)b = _gcab_ = _gabc_ and uses it as his secret.

An eavesdropper has been able to see _ga_, _gb_, _gc_, _gab_, _gac_, and _gbc_, but cannot use any combination of these to efficiently reproduce _gabc_.

```text-plain
from math import *
##given data
p = 9975298661930085086019708402870402191114171745913160469454315876556947370642799226714405016920875594030192024506376929926694545081888689821796050434591251
g = 7
a = 330
b = 450
g_c = 6091917800833598741530924081762225477418277010142022622731688158297759621329407070985497917078988781448889947074350694220209769840915705739528359582454617


#A = (g ** a) % p
#B = (g ** b) % p
#C = g_c % p
#c = ceil(log(g_c)/log(g))

#secretA = (B ** a) % p
#secretB = (A ** b) % p

s = g_c**a % p
secret = s**b % p

print(secret)
```