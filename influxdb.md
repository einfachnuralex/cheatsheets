# Influxdb

## Docker

```
docker run -d -p 8086:8086 influxdb
```

## Create DB

```
curl -i -XPOST http://192.168.2.55:8086/query --data-urlencode "q=CREATE DATABASE ha"
```

```
curl -i -XPOST 'http://192.168.2.55:8086//write?db=ha' --data-binary 'cpu_load_short,host=server01,region=us-west value=0.64 1434055562000000000'
```

## query

```
curl -G 'http://192.168.2.55:8086/query?pretty=true' --data-urlencode "db=ha" --data-urlencode "q=SELECT \"°C\" FROM \"binary_sensor\""
```
