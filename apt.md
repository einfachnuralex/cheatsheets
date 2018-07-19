# apt cache

```
apt cache policy
```

# Update expired GPG key

> apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EA312927

# Disable proxy pipeline

```
echo "Acquire::http::Pipeline-Depth \"0\";" > /etc/apt/apt.conf.d/00no-pipeline
```

# Get packages and install on new system

```
dpkg --get-selections | grep 'install$='| awk '{print $1}' > installedpackages
aptitude update
cat installedpackages | xargs sudo aptitude install
```
```
dpkg --get-selections > apt-selections.txt
dpkg --set-selections < apt-selections.txt
apt-get -u dselect-upgrade
```

# Reinstall package with config

Search for config file

```
dpkg -S apache2.conf
```

Reinstall packages

```
apt-get -o Dpkg::Options::="--force-confmiss" install --reinstall apache2
```
