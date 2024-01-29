# setuid
```text-x-c-src
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>
int main(){
setgid(1002);
setuid(1002);
system("/bin/bash");
}
```