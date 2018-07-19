
#

```


import paramiko

hosts = ['192.168.2.22']

client = paramiko.SSHClient()
client.load_system_host_keys()
client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
client.connect('127.0.0.1', username=username, password=password)
stdin, stdout, stderr = client.exec_command('ls -l')

client.connect('192.168.2.22', username="root", pkey=key)

```
