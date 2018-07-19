
# Health

```bash
curl -XGET 'http://localhost:9200/_cluster/health?pretty=true'
```

# Dump/Snapshot

https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-snapshots.html

Define repo in elasticsearch.yml & restart elasticsearch

```
path.repo: ["/tmp"]
```

Get all snapshots

```bash
curl -XGET 'localhost:9200/_snapshot/_all?pretty'
```

Create Backup target

```bash
curl -XPUT 'localhost:9200/_snapshot/tmp_dump?pretty' -H 'Content-Type: application/json' -d'{"type":"fs","settings":{"location": "/tmp/esdump"}}'
```

Get list of indices

```bash
curl 'localhost:9200/_cat/indices' | grep filebeat_log | cut -d' ' -f4 | tr '\n' ','
```

Create snapshot

```bash
curl -XPUT 'localhost:9200/_snapshot/tmp_dump/snapshot_1?wait_for_completion=true&pretty' -H 'Content-Type: application/json' -d'{"indices":"filebeat_log_2018.02,filebeat_log_2018.03,filebeat_log_2017.08,filebeat_log_2017.09,filebeat_log_2017.10,filebeat_log_2017.12,filebeat_log_2017.07,filebeat_log_2018.01,filebeat_log_2017.11,filebeat_log_2018.04","ignore_unavailable": true,  "include_global_state": false}'
```

Result:

```json
{
  "snapshot" : {
    "snapshot" : "snapshot_1",
    "uuid" : "sadkajsdklasd",
    "version_id" : 5060699,
    "version" : "5.6.6",
    "indices" : [
      "filebeat_log_2017.10",
      "filebeat_log_2017.11",
      "filebeat_log_2018.04",
      "filebeat_log_2017.09",
      "filebeat_log_2017.12",
      "filebeat_log_2017.07",
      "filebeat_log_2018.02",
      "filebeat_log_2018.01",
      "filebeat_log_2018.03",
      "filebeat_log_2017.08"
    ],
    "state" : "SUCCESS",
    "start_time" : "2018-04-03T08:30:13.793Z",
    "start_time_in_millis" : 1522744213793,
    "end_time" : "2018-04-03T08:30:54.329Z",
    "end_time_in_millis" : 1522744254329,
    "duration_in_millis" : 40536,
    "failures" : [ ],
    "shards" : {
      "total" : 10,
      "failed" : 0,
      "successful" : 10
    }
  }
}
```
