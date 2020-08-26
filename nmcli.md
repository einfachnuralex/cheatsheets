# nmcli

some stuff for automating things
  * vlan for serveral usecases
  * for each vlan a brigde in case we setup VMs for dedicated VLANs (or other usecases)
  
room for improvment to add bonding also.

```bash
#!/usr/bin/env bash
 
vlanNames=(wan lan dmz)
vlanIds=( 5 10 100 )
lastOctet="100"
firstOctets="192.168"
parentNic="eth0"
 
DEBUG="echo"
 
for i in "${!vlanNames[@]}"
do
  vName=${vlanNames[$i]}
  vId=${vlanIds[$i]}
  ip4Addr="${firstOctets}.${vId}.${lastOctet}/24"
 
  $DEBUG  nmcli con add type bridge ifname $vName con-name $vName ip4 $ip4Addr
  $DEBUG  nmcli con add type vlan   ifname ${parentNic}.${vId} dev $parentNic id $vId master $vName slave-type bridge
 
done
```
