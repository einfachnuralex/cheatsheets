
# label

```
docker node update --label-add node.labels.elasticsearch.instance=1 nodename
```

```
docker node update --label-rm node.labels.elasticsearch.instance nodename
```

# volles error log

```
docker stack ps escluster --no-trunc
```

# löschen history

```
docker swarm update --task-history-limit 0
```
