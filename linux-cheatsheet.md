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

# progress copy or dd | dd cheat
```bash
dd if=/dev/urandom of=/dev/null status=progress bs=1G count=1 oflag=direct
dd if=/dev/urandom | pv | dd of=/dev/null
```
- **bs** : sets the if and of sizes to bytes; block size (base 10 integer, 1G=1024×1024×1024 bytes = 1.073 GB);
- **count** : number of blocks (1 means that 1 block of 1G is copied);
- **oflag=direct** : uses direct I/O data, avoiding the buffer cache; it speeds up the process

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
# sed
## intro sed
Replace **cat** with **dog**
```bash
sed 's/cat/dog/' old_file > new_file #First
sed 's/cat/dog/5' old_file > new_file #5 times
sed 's/cat/dog/g' old_file > new_file #All
sed '/dragon/s/cat/dog/g' old_file > new_file #Only lines with dragon
sed '/dragon/!s/cat/dog/g'old_file > new_file #All, except lines with dragon
```

## Remove blank lines
```bash
sed '/^$/d' old_file > new_file
```

## Converting between UNIX and Windows
```bash
sed 's/.$//' dos_file > unix_file
sed 's/$'"/`echo \\\r`/" unix_file > dos_file #bash
sed 's/$/\r/' unix_file > dos_file # gsed 3.02.80 or higher
```

# grep
## grep files without comments
```bash
grep -v -e '^#' -e '^$' squid.conf
```
- **e** : regex (^# : #, ^$ : empty line)
- **v** : invert match

# watch for cpu wait

```bash
watch -n 1 "(ps aux | awk '\$8 ~ /D/ { print \$0 }')"
```
