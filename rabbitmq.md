
# Docker

```
docker run -d --hostname my-rabbit --name some-rabbit -p 5671:5671 -p 5672:5672 rabbitmq:3
```

Generate certs

```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ca-key.pem -out ca.pem
openssl genrsa -out srv-key.pem 2048
openssl req -new -key srv-key.pem -out srv.csr -subj "/CN=some-rabbit"
openssl x509 -req -in srv.csr -CA ca.pem -CAkey ca-key.pem -CAcreateserial -out srv.pem -days 3650 -extensions v3_req
```

In rabbitmq.conf

```
listeners.tcp.default = 5671
listeners.ssl.default = 5672
ssl_options.cacertfile = /etc/rabbitmq/ca.pem
ssl_options.certfile = /etc/rabbitmq/srv.pem
ssl_options.keyfile = /etc/rabbitmq/srv-key.pem
ssl_options.verify = verify_peer
ssl_options.fail_if_no_peer_cert = false
```
