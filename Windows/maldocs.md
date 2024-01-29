# maldocs
run `oledump.py` on the file to see the structure, the first column (A1,A2,..) is the streams we can specify with `-s` to more about that part, small `m` is for default macros and large `M` (this is the most interesting) is for custom added macros, run:

```text-plain
oledump.py -s <stream> -v file.doc
```

without the -v, it dumps everything in a "hexeditor" format and with `-v` it dumps the raw malicious vbscript we need.