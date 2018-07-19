
# Reach remote dockerhost

```
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://dockerhost:2376"
export DOCKER_CERT_PATH="/home/alex/.docker/machine/machines/dockerhost"
export DOCKER_MACHINE_NAME="dockerhost"
```

Certs in /home/alex/.docker/machine/machines/dockerhost
```
lrwxrwxrwx 1 alex alex   24 13. Mär 08:21 ca.pem -> docker-ca-test.crt
lrwxrwxrwx 1 alex alex   34 13. Mär 08:21 cert.pem -> alex.test.crt
lrwxrwxrwx 1 alex alex   34 13. Mär 08:21 key.pem -> alex.test.key
```

# Eval

```
eval $(docker-machine env dockerhost)
```


# Config

```
$ docker-machine config dockerhost \
--tlsverify \
--tlscacert=".docker/machine/machines/dockerhost/ca.pem" \
--tlscert=".docker/machine/machines/dockerhost/cert.pem" \
--tlskey=".docker/machine/machines/dockerhost/key.pem" \
-H tcp://dockerhost:2376
```


```
{
    "ConfigVersion": 3,
    "Driver": {
        "IPAddress": "blafasl",
        "MachineName": "test",
        "SSHUser": "",
        "SSHPort": 0,
        "SSHKeyPath": "",
        "StorePath": "/home/alex/.docker/machine",
        "SwarmMaster": false,
        "SwarmHost": "",
        "SwarmDiscovery": "",
        "URL": "http://blafasl"
    },
    "DriverName": "none",
    "HostOptions": {
        "Driver": "",
        "Memory": 0,
        "Disk": 0,
        "EngineOptions": {
            "ArbitraryFlags": [],
            "Dns": null,
            "GraphDir": "",
            "Env": [],
            "Ipv6": false,
            "InsecureRegistry": [],
            "Labels": [],
            "LogLevel": "",
            "StorageDriver": "",
            "SelinuxEnabled": false,
            "TlsVerify": true,
            "RegistryMirror": [],
            "InstallURL": "https://get.docker.com"
        },
        "SwarmOptions": {
            "IsSwarm": false,
            "Address": "",
            "Discovery": "",
            "Agent": false,
            "Master": false,
            "Host": "tcp://0.0.0.0:3376",
            "Image": "swarm:latest",
            "Strategy": "spread",
            "Heartbeat": 0,
            "Overcommit": 0,
            "ArbitraryFlags": [],
            "ArbitraryJoinFlags": [],
            "Env": null,
            "IsExperimental": false
        },
        "AuthOptions": {
            "CertDir": "/home/alex/.docker/machine/certs",
            "CaCertPath": "/home/alex/.docker/machine/certs/ca.pem",
            "CaPrivateKeyPath": "/home/alex/.docker/machine/certs/ca-key.pem",
            "CaCertRemotePath": "",
            "ServerCertPath": "/home/alex/.docker/machine/machines/test/server.pem",
            "ServerKeyPath": "/home/alex/.docker/machine/machines/test/server-key.pem",
            "ClientKeyPath": "/home/alex/.docker/machine/certs/key.pem",
            "ServerCertRemotePath": "",
            "ServerKeyRemotePath": "",
            "ClientCertPath": "/home/alex/.docker/machine/certs/cert.pem",
            "ServerCertSANs": [],
            "StorePath": "/home/alex/.docker/machine/machines/test"
        }
    },
    "Name": "test"
}
```
