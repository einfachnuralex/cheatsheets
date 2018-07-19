# Mini router

## Erstellen von NAT-Rules mit IPTables

eth0:

```
sysctl -w net.ipv4.ip_forward=1

iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
iptables -A FORWARD -i eth0 -o vboxnet0 -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD -i vboxnet0 -o eth0 -j ACCEPT
```

wlan0:

```
sysctl -w net.ipv4.ip_forward=1

iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE
iptables -A FORWARD -i wlan0 -o vboxnet0 -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD -i vboxnet0 -o wlan0 -j ACCEPT
```

# Delete all rules in iptables
```
iptables -F
iptables -X
iptables -t nat -F
iptables -t nat -X
iptables -t mangle -F
iptables -t mangle -X
iptables -P INPUT ACCEPT
iptables -P OUTPUT ACCEPT
iptables -P FORWARD ACCEPT
```
