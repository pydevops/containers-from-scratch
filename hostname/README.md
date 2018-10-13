This lab is to demo UTS namespace

## change hostname with `unshare` command
`unshare -u` uses a new UTS space by unsharing from its parent. 
 We then run `hostname cool-container`  to set the hostname inside the new UTS namespace only. 

```
yongweiy@was-1:~$ hostname
was-1
yongweiy@was-1:~$ sudo unshare -u /bin/bash
root@was-1:/home/yongweiy# hostname cool-container
root@was-1:/home/yongweiy# hostname
cool-container
root@was-1:/home/yongweiy# exit
exit
yongweiy@was-1:~$ hostname
was-1
```

## change hostname in syscall

Please note the output from `readlink /proc/self/ns/uts` are different in host and container. These two bash processes are indeed running in different UTS namespaces.

```
root@was-1:~# hostname
was-1
root@was-1:~# go run hostname.go run /bin/bash
Running [/bin/bash]
Running [/bin/bash]
root@cool-container:~# readlink /proc/self/ns/uts
uts:[4026532211]
root@container:~# exit
exit

root@was-1:~# hostname
was-1
root@was-1:~# readlink /proc/self/ns/uts
uts:[4026531838]
```