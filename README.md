# Container from Scratch
Low-level container runtimes have a limited feature set and typically perform the low-level tasks for running a container. Most developers shouldn't use them for their day-to-day work. Low-level runtimes are usually implemented as simple tools or libraries that developers of higher level runtimes and tools can use for the low-level features. While most developers won't use low-level runtimes directly, it's good to know how they work for troubleshooting and debugging purposes.

Here are some labs I made from studying from various sources found on internet. 
It is about namespace, cgroups and other security features in the Linux kernel. 

## Labs

### unshare
Creating namespace is super easy, just a single syscall with one argument, unshare. The unshare command line tool gives us a nice wrapper around this syscall and lets us setup namespaces manually.

### syscall in go



## Reference
* [Containers from Scratch from Eirc Chiang](https://ericchiang.github.io/post/containers-from-scratch/)
* [Containers from Scratch - Eric Chiang, CoreOS](https://www.youtube.com/watch?v=wyqoi52k5jM)
* [Containers from scratch: The sequel - Liz Rice](https://www.youtube.com/watch?v=_TsSmSu57Zo)
* [github from Liz Rice](https://github.com/lizrice/containers-from-scratch)