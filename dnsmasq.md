
# NetworkManager & dnsmasq

/etc/NetworkManager/dnsmasq.d/custom-dns

```
server=/example.com/xx.xx.xx.xx
server=/example.net/xx.xx.xx.xx
```

# DHCP Proxy & TFTP Server mit DNSMASQ

http://blog.sengotta.net/pxe-server-mit-dnsmasq/

### Install

```
apt-get install dnsmasq
```

edit /etc/dnsmasq.d/tftp

```
port=0
log-dhcp
enable-tftp
tftp-root=/srv/tftp
dhcp-range=192.168.178.0,proxy
pxe-prompt="Taste F8 zeigt Auswahl",5
pxe-service=x86PC, "Install Linux", pxelinux
```

```
systemctl restart dnsmasq
```