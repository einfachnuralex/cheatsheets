# Python

# Inspect object

https://stackoverflow.com/questions/34439/finding-what-methods-a-python-object-has

```python
dir(object)
```

# Uninstall

https://stackoverflow.com/questions/1550226/python-setup-py-uninstall

python setup.py install --record files.txt
cat files.txt | xargs rm -rf

# install requirements.txt

https://stackoverflow.com/questions/7225900/how-to-pip-install-packages-according-to-requirements-txt-from-a-local-directory
pip install -r /path/to/requirements.txt

# uninstall requirements

https://stackoverflow.com/questions/7915998/does-uninstalling-a-package-with-pip-also-remove-the-dependent-packages

### install pip-autoremove

```
pip install pip-autoremove
```

### remove "somepackage" plus its dependencies:

```
pip-autoremove somepackage -y
```

### SSL

https://stackoverflow.com/questions/42982143/python-requests-how-to-use-system-ca-certificates-debian-ubuntu

```
export REQUESTS_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt
```
