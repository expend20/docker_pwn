# libc versions

* 19.10, libc 2.29
* 19.04, libc 2.29
* 18.10, libc 2.28
* 18.04, libc 2.27
* 16.04, libc 2.23
* 14.04, libc 2.19

# tips

* launch

  ```
  docker run -it --rm --cap-add=SYS_PTRACE --security-opt seccomp=unconfined -v $(realpath .):/ctf expend20/pwn:18.04 bash
  ```
