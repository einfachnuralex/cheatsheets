
# docker daemon settings

> /etc/docker/daemon.json

Limit log file size

> /etc/docker/daemon.json

```
{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "200m"
  }
}
```
Change default docker0 net

``https://success.docker.com/article/How_do_I_configure_the_default_bridge_(docker0)_network_for_Docker_Engine_to_a_different_subnet``

{
  "bip": "172.26.0.1/16"
}

# docker machine

## connect docker machine

```
eval $(docker-machine env dockerhost)
```

# Delete docker logs

```
echo "" > $(docker inspect --format='{{.LogPath}}' <container_name_or_id>)
```

All logs

```
truncate -s 0 /var/lib/docker/containers/*/*-json.log
```

# Delete all containers

```
docker rm $(docker ps -a -q)
```

# Delete all images

```
docker rmi $(docker images -q)
```

# List all volumes

```
docker inspect -f '{{ .Mounts }}' $(docker ps -q)
```

# cleanup

```
docker system prune
```

### docker container process ids

```
docker ps -q | xargs docker inspect --format '{{.State.Pid}}'
```

### docker stats

```
docker stats
```
