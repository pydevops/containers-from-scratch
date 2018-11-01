This lab shows how to create a new pid namespace and new /proc.

## implement in bash

### make a rootfs
`debootstrap` is used for creating a debian based root file system. 
```
root@pg:~# debootstrap stable rootfs http://deb.debian.org/debian/
```

### 
Establish a PID namespace, ensure  PID 1 in it against a newly mounted procfs instance.

```
root@pg:~# unshare --pid --fork --mount-proc=$PWD/rootfs/proc chroot rootfs /bin/bash
root@pg:/# ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1  18228  3256 ?        S    19:09   0:00 /bin/bash
root         2  0.0  0.1  36636  2812 ?        R+   19:09   0:00 ps aux
```

## implement in syscall

```
root@pg:~/go/src/containers-from-scratch# go run namespaces/pid/pid.go run /bin/bash
Parent:Running [/bin/bash] as pid 26653
Child:Running [/bin/bash] as pid 1
root@cool-container:/# ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.0 102888  1576 ?        Sl   19:08   0:00 /proc/self/exe child /bin/bash
root         4  0.0  0.1  18228  3180 ?        S    19:08   0:00 /bin/bash
root         5  0.0  0.1  36636  2852 ?        R+   19:08   0:00 ps aux
```

