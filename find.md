# find and exec

```
find /var/backups/files/mongodb/ -maxdepth 1 -mtime +6 -exec rm -rf {} \;
```

* maxdepth 1: Limit depth for recursive to 1
* mtime +6: Files or directories modified in the last 6 days

# find files sorted by size

```bash
find . -printf '%s %p\n'| sort -nr | head -10
find . -type f -exec ls -sh {} \; | sort -n -r | head -10
find / -type d -exec du -s {} \; | sort -n -r | head -30
```

https://www.cyberciti.biz/faq/how-do-i-find-the-largest-filesdirectories-on-a-linuxunixbsd-filesystem/

# correct dir & file permissions

```
find ./ -type d -exec chmod 755 {} \;
find ./ -type f -exec chmod 644 {} \;
```
