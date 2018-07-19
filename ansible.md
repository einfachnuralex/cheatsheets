
# Filter

http://docs.ansible.com/ansible/latest/user_guide/playbooks_filters.html

default values

```
{{ some_variable | default(5) }}
```

# Local only

https://stackoverflow.com/questions/42982143/python-requests-how-to-use-system-ca-certificates-debian-ubuntu

```
- hosts: 127.0.0.1
  connection: local
```

## ansible setup

```
ansible -i inventory -m setup host-in-inv
```

# Check variable for host

https://stackoverflow.com/questions/43467180/how-to-decrypt-string-with-ansible-vault-2-3-0/43467369#43467369

```
ansible frvpdol050-help -m debug -a 'var=install_docker_py'
```

# Check ansible inventory

```
ansible -m ping all | grep "UNREACHABLE" | sort
```

# Search for local users

```
ansible all -m shell -a "awk -F ':' '\$3 > 999 && \$3 < 9999 \
{print \$1}' /etc/passwd" | less -R
```

With filter

```
ansible all -m shell -a "awk -F ':' '\$3 > 999 && \$3 < 9999 \
{print \$1}' /etc/passwd | grep username" | less -R
```
