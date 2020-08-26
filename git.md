
# ssh key

```
git config core.sshCommand "ssh -i ~/.ssh/id_rsa_example -F /dev/null"
```

# remote

See remote

```
git remote -v
```

Set remote (on github)

https://help.github.com/articles/changing-a-remote-s-url/#switching-remote-urls-from-ssh-to-https

```
git remote set-url origin git@github.com:USERNAME/REPOSITORY.git
```

# github

Check SSH key on github

```
ssh -i ~/.ssh/einfachnuralex -T git@github.com
```

Response:
> Hi einfachnuralex! You've successfully authenticated, but GitHub does not provide shell access.


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

nachtraeglich commit anpassen mit anderem User / Email / Signatur
```
git rebase --exec 'git commit --amend --no-edit -n -S --author="user name <e@mail>"' -i commit-hash
```
d.h. in den fall alles vom commit-hash bis zum akutellen HEAD wird umgebaut(!).
