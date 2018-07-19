
# Links

curl to python requests
https://curl.trillworks.com/

# proxy

https://stackoverflow.com/questions/9445489/performing-http-requests-with-curl-using-proxy

```
curl -x http://proxy_server:proxy_port --proxy-user username:password -L http://url
```

# With response header

```
curl -i  https://golem.de
```

# Resolve dns

https://stackoverflow.com/questions/3390549/set-curl-to-use-local-virtual-hosts

```bash
curl --resolve 'doku.axoom.com:443:157.97.109.40' https://doku.axoom.com/something
```

# Ignore SSL

```bash
curl -k https://test.lan
```

# JSON output

```bash
curl -k https://test.lan | jq
```

# my ip

```sh
curl http://v4.ipv6-test.com/api/myip.php
```

# What is my ip oneliner

```
curl https://ifconfig.co
```
