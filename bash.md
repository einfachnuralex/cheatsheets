## add user

user=username
adduser --quiet --disabled-password --gecos "" $user
adduser $user sudo
echo $user':password' | chpasswd
chage -d0 $user


## loop

for i in $(ls); do echo $i ; done

## loop dd

for i in {1..20}; do dd if=/dev/zero of=file-$i.txt count=1024 bs=1024; done
