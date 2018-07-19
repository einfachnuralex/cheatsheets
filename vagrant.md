# Minimal config

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  config.vm.provision :shell, :inline => "echo 'ssh-rsa AAAAB3NzaC...1HnQ== alex' > /root/.ssh/authorized_keys", :privileged => true
  config.vm.provision :shell, :inline => "apt-get -y install python-apt", :privileged => true
end
```

# Providers

## Install provider

```bash
vagrant plugin install virtualbox
```

## Default provider

```bash
export VAGRANT_DEFAULT_PROVIDER=virtualbox
```

## Openstack provider

https://github.com/ggiamarchi/vagrant-openstack-provider
https://blog.scottlowe.org/2015/09/28/using-vagrant-with-openstack/
https://github.com/cloudbau/vagrant-openstack-plugin
https://henning.kropponline.de/2014/09/28/provisioning-cluster-using-vagrant-openstack/

Debug:

```
export VAGRANT_OPENSTACK_LOG=debug
```

# Config

## SSH

```
$ vagrant ssh-config
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /home/alex/work/netbox/.vagrant/machines/default/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL
```
