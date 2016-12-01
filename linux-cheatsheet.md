# find files sorted by size
```bash
find . -printf '%s %p\n'| sort -nr | head -10
find . -type f -exec ls -sh {} \; | sort -n -r | head -10
```
https://www.cyberciti.biz/faq/how-do-i-find-the-largest-filesdirectories-on-a-linuxunixbsd-filesystem/

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

# progress copy or dd
```bash
dd if=/dev/urandom of=/dev/null status=progress
dd if=/dev/urandom | pv | dd of=/dev/null
```

# openssl magic
## Check a Certificate Signing Request (CSR)
```
openssl req -text -noout -verify -in CSR.csr
```


## Check a private key
```
openssl rsa -in privateKey.key -check
```

## Check a certificate
```
openssl x509 -in certificate.crt -text -noout
```

## Check a PKCS#12 file (.pfx or .p12)
```
openssl pkcs12 -info -in keyStore.p12
```


# debian update-rc.d
```
update-rc.d daemon defaults
update-rc.d -f daemon remove
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

# Ubuntu/Debian: re-generate ssh keys
```
rm -v /etc/ssh/ssh_host_*
dpkg-reconfigure openssh-server
```

# disable swapping
```
vm.swappiness = 0 in /etc/sysctl.conf
```
