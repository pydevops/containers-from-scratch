This lab is to show how to create a new pid namespace and new /proc.

## with `unshare` command

```
# Establish a PID namespace with a new /proc
$ sudo unshare --fork --pid --mount-proc bash
root@was-1:/home/yongweiy# ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.2  19968  3936 pts/2    S    00:29   0:00 bash
root         2  0.0  0.1  38308  3256 pts/2    R+   00:29   0:00 ps aux


# Establish a PID namespace, ensure we're PID 1 in it against a newly mounted procfs instance.
$ sudo unshare --fork --pid --mount-proc readlink /proc/self
1

```

## syscall in go
Establish a PID namespace and mount 

### Download a root file system
The tarball below holds something that looks like a Debian file system and will be our playground for isolating processes.

```
$ wget https://github.com/ericchiang/containers-from-scratch/releases/download/v0.1.0/rootfs.tar.gz
$ sha256sum rootfs.tar.gz 
c79bfb46b9cf842055761a49161831aee8f4e667ad9e84ab57ab324a49bc828c  rootfs.tar.gz
$ sudo tar -C /root -zxf rootfs.tar.gz
```

### Run

```
root@was-1:~/go# go run pid.go run /bin/bash
Parent:Running [/bin/bash] as pid 27928
Child:Running [/bin/bash] as pid 1
root@cool-container:/# ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.0 102888  1576 ?        Sl   05:24   0:00 /proc/self/exe child /bin/bash
root         4  0.0  0.1  20272  3284 ?        S    05:24   0:00 /bin/bash
root         5  0.0  0.1  17496  2060 ?        R+   05:24   0:00 ps aux
```

