# requirements
In order to successfully exploit the above bug three conditions must be satisfied:

*   The application must have a class which implements a PHP magic method (such as `__wakeup` or `__destruct`) that can be used to carry out malicious attacks, or to start a "POP chain".
*   All of the classes used during the attack must be declared when the vulnerable `unserialize()` is being called, otherwise object autoloading must be supported for such classes .
*   The data passed to unserialized comes from a file, so a file with serialized data must be present on the server.