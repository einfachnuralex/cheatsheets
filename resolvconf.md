# resolvconf

### Add multiple domains to search

> /etc/resolvconf.conf

```
search_domains="psynet.lan test.lan"
```

### Activate configuration

```
resolvconf -u
```
