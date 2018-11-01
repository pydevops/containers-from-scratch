This lab shows how to create a UTS namespace

## implement in bash
`unshare -u` uses a new UTS space by unsharing from its parent. 
 We then run `hostname cool-container`  to set the hostname inside the new UTS namespace only. 

```
yongweiy@pg:~$ hostname
pg
yongweiy@pg:~$ sudo unshare -u /bin/bash
root@pg:/home/yongweiy# hostname cool-container
root@pg:/home/yongweiy# hostname
cool-container
root@pg:/home/yongweiy# exit
exit
yongweiy@pg:~$ hostname
pg
```

## implement in syscall

Please note the output from `readlink /proc/self/ns/uts` are different in host and container. These two bash processes are indeed running in different UTS namespaces.

```
root@pg:~# hostname
pg
root@pg:~# go run hostname.go run /bin/bash
Running [/bin/bash]
Running [/bin/bash]
root@cool-container:~# readlink /proc/self/ns/uts
uts:[4026532211]
root@container:~# exit
exit

root@pg:~# hostname
pg
root@pg:~# readlink /proc/self/ns/uts
uts:[4026531838]
```