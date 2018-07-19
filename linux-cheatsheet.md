
# simple http server
```
python -m SimpleHTTPServer
python3 -m http.server
```
http://www.commandlinefu.com/commands/view/9841/an-alternative-to-python-m-simplehttpserver-for-arch-linux

# emulate webserver
```bash
nohup sudo nc -lk -p 80 -e echo -ne "HTTP/1.0 200 OK\r\nContent-Length: 9\r\n\r\nserver1\r\n" &
```

# su magic

## run command as other user

```bash
su rundeck -s /bin/bash -c "ansible all -m ping"
```

* Even when shell is /bin/false

# debian update-rc.d
```
update-rc.d daemon defaults
update-rc.d -f daemon remove
```

# disable swapping
```
vm.swappiness = 0 in /etc/sysctl.conf
```

# disable ipv6
disable ipv6 instantly
```bash
echo "1" > /proc/sys/net/ipv6/conf/all/disable_ipv6
```
disable ipv6 permanent
```
nano sysctl.conf

net.ipv6.conf.all.disable_ipv6=1
net.ipv6.conf.default.disable_ipv6=1
net.ipv6.conf.lo.disable_ipv6=1

sysctl -p
```

# bad block on HDD
```bash
badblocks -v /dev/hda1 > bad_blocks
fsck -t ext4 -l bad_blocks /dev/sda1
```

# watch for cpu wait

```bash
watch -n 1 "(ps aux | awk '\$8 ~ /D/ { print \$0 }')"
```

# LDAP magic

## LDAP testing

http://wiki.linuxwall.info/doku.php/en:ressources:astuces:ldapsearch

```
ldapsearch -LLL -x -h 192.168.33.11 -D "CN=srv-rundeck,OU=SRV-SA,DC=psynet,DC=test" -w Start123 -b DC=psynet,DC=test
ldapsearch -LLL -x -h 192.168.33.11 -D "CN=srv-rundeck,OU=SRV-SA,DC=psynet,DC=test" -w Start123 -b DC=psynet,DC=test -s sub '(sAMAccountName=admin)'
```

```
slapcat -b dc=linux,dc=test,dc=domain
```


## New LDAP config

```
slapcat -b cn=config
```

# Java

## Java keystore

```
keytool -import -alias test-ca -file test-ca.cer -keystore  /etc/rundeck/ssl/truststore -storepass adminadmin -noprompt
```

# Telnet

## telnet exit

* Strg + AltGr + }
