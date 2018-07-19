
# ssh key

```
git config core.sshCommand "ssh -i ~/.ssh/id_rsa_example -F /dev/null"
```

# SSL

https://stackoverflow.com/questions/11621768/how-can-i-make-git-accept-a-self-signed-certificate

git -c http.sslVerify=false clone https://github.com/bla/foo
git config http.sslVerify false

# checkout

https://githowto.com/getting_old_versions

git checkout 911e8c9

# git clone tag

https://stackoverflow.com/questions/791959/download-a-specific-tag-with-git

```
git clone https://github.com/RocketChat/Rocket.Chat.Ansible.git
cd Rocket.Chat.Ansible
git checkout tags/v3.0.0
```

# git search

https://stackoverflow.com/questions/4705517/github-searching-through-older-versions-of-files

```
git log -S'get info' -p
```

# git log

All log

```
git log
```

Log for specific file or folder

```
git log .
git log file
```
