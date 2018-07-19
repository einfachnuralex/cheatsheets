
#

```
openstack server list | grep k8s | cut -d '|' -f3,5,7 |sort
```
