
# openssl magic

## Self signed ca

```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ca-key.pem -out ca.pem
```

## Create key, cert & sign ca

```
openssl genrsa -out certs/alex-key.pem 2048
openssl req -new -key certs/alex-key.pem -out certs/alex.csr -subj "/CN=alex" -config openssl.conf
openssl x509 -req -in certs/alex.csr -CA ssl/ca.pem -CAkey ssl/ca-key.pem -CAcreateserial -out certs/alex.pem -days 3650 -extensions v3_req -extfile openssl.conf
```

## Extracting Certificate and Private Key Files from a .pfx File

Run the following command to export the private key:
```
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
```
Run the following command to export the certificate:
```
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
```
Run the following command to remove the passphrase from the private key:
```
openssl rsa -in key.pem -out server.key
```

## Create pfx from cert and key

```bash
openssl pkcs12 -inkey certs/somehost.psynet.lan.key -in certs/somehost.psynet.lan.crt -export -out certs/somehost.psynet.lan.pfx
```
Leave the password blank, otherwise IIS would need a password each time the service starts, which is not feasible. Then import the file to IIS.

Check a Certificate Signing Request (CSR)
```
openssl req -text -noout -verify -in CSR.csr
```

## Check snippets

Check a private key
```
openssl rsa -in privateKey.key -check
```

Check a certificate
```
openssl x509 -in certificate.crt -text -noout
```

Oneliner to display all certs in bundle

```
openssl crl2pkcs7 -nocrl -certfile /etc/ssl/certs/cert.bundle_2019.crt | openssl pkcs7 -print_certs -noout
```

Check a PKCS#12 file (.pfx or .p12)
```
openssl pkcs12 -info -in keyStore.p12
```

## OpenSSL client

```
openssl s_client -showcerts -connect ldaphost:636
```

## CSR decode

```
openssl req -in mycsr.csr -noout -text
```

# CA keystore

https://askubuntu.com/questions/645818/how-to-install-certificates-for-command-line

```
cp mycert.cer /usr/share/ca-certificates/mycert.pem
dpkg-reconfigure ca-certificates
update-ca-certificates
```
