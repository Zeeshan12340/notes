# Securing
The Principle of Least Privileges:

Whilst this is an over-arching theme of InfoSec as a whole, we'll pertain this to Docker...

Remember Docker images? The commands in these images will execute as root unless told otherwise. Let's say you create a Docker image for your webserver, in this case, the service will run as root. If an attacker managed to exploit the web server, they would now have root permissions to the container

Docker  Seccomp 101:

Seccomp or "Secure computing" is a security feature of the Linux kernel, allowing us to restrict the capability of a container by determining the system calls it can make. [Docker uses security profiles](http://docs.docker.oeynet.com/engine/security/seccomp/#pass-a-profile-for-a-container) for containers. For example, we can deny the container the ability to perform actions such as using the mount namespace or any of the [Linux system calls.](https://filippo.io/linux-syscall-table/)

Securing your Daemon:

In later installs of the Docker engine, running a registry relies on the use of implementing self-signed SSL certificates behind a web server, where these certificates must then be distributed and trusted on every device that will be interacting with the registry. This is quite the hassle for developers wanting to setup quick environments - which goes against the entire point of Docker.