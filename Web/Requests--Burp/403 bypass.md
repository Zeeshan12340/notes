# 403 bypass
use  `403fuzzer` to bypass forbidden directories in websites. Basically, add's weird characters to the file or directories to make the server spill some files. (Side note: always ensure proper enumeration/dir-busting, missed two useful files cuz of not using `-e .php` in FUZZ)

you can also try stressing the server(by sending multiple requests with curl or python) which might result in it listing the files. (didn't work in this case tho :(