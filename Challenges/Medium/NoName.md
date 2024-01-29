# NoName
web port is open, and an interactive web cli on port 2222 which doesn't save creds and stores a “buffer” value on port 9090(which is python tornado webserver),

overflowing the “buffer” on 2222 with ‘A’\*2000 shows the below directory: (need further enumeration)

`http://10.10.12.143:9090/40b5dffec4e39b7a3e9d261d2fc4a038/`