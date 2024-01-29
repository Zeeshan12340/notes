# JWT
JSON Web Token(JWT) is one of the commonly used methods for authorization. This is a kind of cookie that is generated using HMAC hashing or public/private keys. So unlike any other kind of cookie, it lets the website know what kind of access the currently logged in user has. The only special thing about JWT is that they are in JSON format(after decoding).

Json Web Token's are a fairly interesting case, as it isn't a vulnerability itself. Infact, it's a fairly popular, and if done right very secure method of authentication. The basic structure of a JWT is this, it goes "header.payload.secret", the secret is only known to the server, and is used to make sure that data wasn't changed along the way. Everything is then base64 encoded.

JWT can be divided into 3 parts separated by a dot(.)

1) **Header:**  This consists of the algorithm used and the type of the token.

`{  "alg": "HS256", "typ": "JWT"}`

alg could be HMAC, RSA, SHA256 or can even contain None value.

2) **Payload:** This is part that contains the access given to the certain user etc. This can vary from website to website, some can just have a simple username and some ID and others could have a lot of other details.

3) **Signature:** This is the part that is used to make sure that the integrity of the data was maintained while transferring it from a user's computer to the server and back. This is encrypted with whatever algorithm or **alg** that was passed in the header's value. And this can only be decrypted with a predefined secret(which should be difficult to)

Now take this JWT token and then you can decode it part by part.

So if we decode the first part, which will do: `{"typ":"JWT","alg":"HS256"}`

and decoding the 2nd part, we will get: `{"exp":1586620929,"iat":1586620629,"nbf":1586620629,"identity":1}`

If you try to decode the 3rd part then you'll get some gibberish. But that is okay we only need the first and the second part.

Now if we notice the **identity** value that is probably being used to identify the user but if you'll just edit that then it won't work because as I said the 3rd part is encrypted. So to bypass this we will make changes in the header as well as the value of the identity.

Encode the following string with base64 and that will be our first part

`{"typ":"JWT","alg":"NONE"}`

For the second part, we'll encode the following string:

`{"exp":1586620929,"iat":1586620629,"nbf":1586620629,"identity":2}`

Notice how we changed the value of **identity** from **1**  to **2**.

Since we placed the alg value to None we don't have to add a 3rd part or the encrypted value so we can just put a dot(.) after 2nd part and leave it like that. So the final string would look like:

`eyJ0eXAiOiJKV1QiLCJhbGciOiJOT05FIn0K.eyJleHAiOjE1ODY3MDUyOTUsImlhdCI6MTU4NjcwNDk5NSwibmJmIjoxNTg2NzA0OTk1LCJpZGVudGl0eSI6MH0K.`

To brute force these secrets we'll be using a tool called [jwt-cracker](https://github.com/lmammino/jwt-cracker). The syntax of jwt-cracker is`jwt-cracker <token> [alphabet] [max-length]` where alphabet and max-length are optional parameters.