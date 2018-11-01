# Container from Scratch

## What is container? 

Why is it not a simple syscall and it's all done for us? The fact is that container's don't exist, they are made up. 
There is no such thing as a "linux container" in the kernel. A container is a userland concept. Containers are composed using multiple independent features.

- On Linux, containers rely on "namespaces, cgroups, and some filesystem magic."
- Security also requires features like capabilities, seccomp, LSMs...

## Key Linux concepts

* namespace: 
  * limits what you see so that you can use. 
  * These namespaces are available in modern kernels:
    - pid
    - net
    - mnt
    - uts
    - ipc
    - user
  * Each process belongs to one namespace of each type

* cgroups (Control groups):
  * limits you can use
  * provide resource *metering* and *limiting* on many aspects
    - memory
    - CPU
    - block I/O
    - network (with cooperation from iptables/tc)
    - huge pages (a special way to allocate memory)
    - RDMA (resources specific to InfiniBand / remote memory transfer)
    - a "pids" cgroup to limit the number of processes in a given group.
    - a "devices" cgroup to control access to device nodes

* Security
  * Seccomp
  * Capabilities
  * App Armor
  * SELinux

* Volumes
* Network


## Labs
Here are some labs I made from studying various sources found on internet. 
Most lab follow the two different ways to use the key concepts above. 

### from bash
Creating namespace is easy, just a single syscall with one argument, unshare. The unshare command line tool gives us a nice wrapper around this syscall and lets us setup namespaces manually.

### from syscall
[go's syscall package](https://golang.org/pkg/syscall/) makes it easy.

## Reference
* [Containers from Scratch from Eirc Chiang](https://ericchiang.github.io/post/containers-from-scratch/)
* [Containers from Scratch - Eric Chiang, CoreOS](https://www.youtube.com/watch?v=wyqoi52k5jM)
* [Containers from scratch: The sequel - Liz Rice](https://www.youtube.com/watch?v=_TsSmSu57Zo)
* [github from Liz Rice](https://github.com/lizrice/containers-from-scratch)
* [Deep dive into container internals](https://github.com/jpetazzo/container.training/blob/master/slides/containers/Namespaces_Cgroups.md)