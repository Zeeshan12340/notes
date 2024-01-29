# C
```text-x-csrc
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

#define die(e) do { fprintf(stderr, "%s\n", e); exit(EXIT_FAILURE); } while (0);

void pwncollege(){
	
}
int main() {
  int link[2];
  pid_t pid;
  //fprintf(stdout, "%d\n", getpid());

  char foo[4096];

  if (pipe(link)==-1)
    die("pipe");

  if ((pid = fork()) == -1)
    die("fork");

  if(pid == 0) {

    dup2 (link[1], STDOUT_FILENO);
    close(link[0]);
    close(link[1]);
    execl("embryoio_level1", "embryoio_level1", "-1", (char *)0);
    die("execl");

  } else {

    close(link[1]);
    int nbytes = read(link[0], foo, sizeof(foo));
    printf("Output: (%.*s)\n", nbytes, foo);
    wait(NULL);

  }
  return 0;
}
```

#include and #define
--------------------

I'll try to break down the program for my own understanding. `#include` and `#define` are pre-processor directives that are compiled before anything else in the program, can be used for declaring constants or expressions.

here, we're using `#define` to define a function, which uses `fprintf`to print the the string value passed into the `die` function to standard error and then exits with `exit(EXIT_FAILURE)`, If you want to write perfectly portable code use,`EXIT_FAILURE` for failure , case. the value of EXIT\_FAILURE is 8.

pid\_t
------

The `pid_t`is used for getting process ids and it's usage is shown in a commented line.

pipe()
------

`pipe()` :Pipe is one-way communication only i.e we can use a pipe such that One process write to the pipe, and the other process reads from the pipe. It opens a pipe, which is an area of main memory that is treated as a _**“virtual file”**_.

**int pipe(int fds\[2\]);** **Parameters :** **fd\[0\]** will be the fd(file descriptor) for the read end of pipe. **fd\[1\]** will be the fd for the write end of pipe. **Returns :** 0 on Success. **\-1** on error so if it's an error code, we call the `die` function with the error “pipe”.

fork()
------

Fork system call is used for creating a new process, which is called _**child process**_, which runs concurrently with the process that makes the fork() call (parent process). After a new child process is created, both processes will execute the next instruction following the fork() system call. A child process uses the same pc(program counter), same CPU registers, same open files which use in the parent process. 

_**Negative Value**_: creation of a child process was unsuccessful.   
_**Zero**_: Returned to the newly created child process.   
_**Positive value**_: Returned to parent or caller. The value contains process ID of newly created child process.

wait()
------

A call to wait() blocks the calling process until one of its child processes exits or a signal is received. After child process terminates, parent _**continues**_ its execution after wait system call instruction. 

```text-x-csrc
// C program to demonstrate working of wait()
#include<stdio.h>
#include<stdlib.h>
#include<sys/wait.h>
#include<unistd.h>

int main()
{
	pid_t cpid;
	if (fork()== 0)
		exit(0);		 /* terminate child */
	else
		cpid = wait(NULL); /* reaping parent */
	printf("Parent pid = %d\n", getpid());
	printf("Child pid = %d\n", cpid);

	return 0;
}
```

dup() and dup2()
----------------

The dup() system call creates a copy of a file descriptor.

*   It uses the lowest-numbered unused descriptor for the new descriptor.
*   If the copy is successfully created, then the original and copy file descriptors may be used interchangeably.
*   They both refer to the same open file description and thus share file offset and file status flags.

The dup2() system call is similar to dup() but the basic difference between them is that instead of using the lowest-numbered unused file descriptor, it uses the descriptor number specified by the user.   
**Syntax:**

```text-x-csrc
int dup2(int oldfd, int newfd);
oldfd: old file descriptor
newfd new file descriptor which is used by dup2() to create a copy.
```