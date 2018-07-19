
# filter logs

https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs

Following Logs

```
journalctl -f
```

Display logs from the current/last boot

```
journalctl -b
journalctl -b -1
```

List boots

```
journalctl --list-boots
```

Filter by unit. Unit names from systemd. Multiple unit possible.

```
journalctl -u nginx.service -u php-fpm.service
```

Displaying Kernel Messages like dmesg

```
journalctl -k
```

Filter by priority

```
journalctl -p err -b
```

# Configuration

Persistant logs

> /etc/systemd/journald.conf

```
[Journal]
Storage=persistent
```
