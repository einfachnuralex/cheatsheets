

# showmapped

rbd showmapped

id pool                  image  snap device    
0  docker_swarm_test data   -    /dev/rbd0
1  docker_swarm_test backup -    /dev/rbd1

# list images in pool

rbd ls docker_swarm_ace_test

# status image

rbd status docker_swarm_ace_test/data

# info

rbd info docker_swarm_ace_test/data

# rbd logging

https://ceph.com/geen-categorie/ceph-collect-kernel-rbd-logs/

```
#!/bin/sh -x

p() {
echo “$*” > /sys/kernel/debug/dynamic_debug/control
}

echo 9 > /proc/sysrq-trigger
p ‘module ceph +p’
p ‘module libceph +p’
p ‘module rbd +p’
```

> dmesg
