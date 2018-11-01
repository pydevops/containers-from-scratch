```
# create a README in container's mnt namespace
root@pg:~# go run mnt.go run /bin/bash
Parent:Running [/bin/bash] as pid 1402
Child:Running [/bin/bash] as pid 1
root@cool-container:/# mount
proc on /proc type proc (rw,relatime)
thing on /random type tmpfs (rw,relatime)
root@cool-container:/# touch random/HELLO
root@cool-container:/# exit
exit
# no README on host
root@pg:~# ls rootfs/random/
```