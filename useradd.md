
# useradd script

```bash
#!/bin/bash
users=( alex pdau )

for user in "${users[@]}"
do
   adduser --quiet --disabled-password --gecos "" $user
   adduser $user sudo
   echo $user:'password' | chpasswd
   chage -d0 $user
   mkdir /home/$user/.ssh
   touch /home/$user/.ssh/authorized_keys
   chown -R $user:$user /home/$user/.ssh
done
```
