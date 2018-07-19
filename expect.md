
https://stackoverflow.com/questions/4780893/use-expect-in-bash-script-to-provide-password-to-ssh-command
https://stackoverflow.com/questions/84882/sudo-echo-something-etc-privilegedfile-doesnt-work-is-there-an-alterna
# 1

```bash
#!/usr/bin/expect
eval spawn ssh -oStrictHostKeyChecking=no -oCheckHostIP=no alex@localhost
#use correct prompt
set prompt ":|#|\\\$"
interact -o -nobuffer -re $prompt return
send "password\r"
interact -o -nobuffer -re $prompt return
send "ls -l\r"
interact -o -nobuffer -re $prompt return
send "df -h /\r"
interact
```

# 2

```bash
#!/usr/bin/expect

set timeout 20

set cmd [lrange $argv 1 end]
set password [lindex $argv 0]

eval spawn $cmd
expect "assword:"
send "$password\r";
interact
```
