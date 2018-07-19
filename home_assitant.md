#

# systemd

/etc/systemd/system/hass.service

```
[Unit]
Description=Home Assistant
After=network-online.target

[Service]
Type=simple
#User=%i
ExecStart=/srv/homeassistant/bin/hass -c "/root/.homeassistant"

[Install]
WantedBy=multi-user.target
```

## influxdb

https://home-assistant.io/components/influxdb/

```
$ hass --script influxdb_migrator \
    -H IP_INFLUXDB_HOST -u INFLUXDB_USERNAME -p INFLUXDB_PASSWORD \
    -d INFLUXDB_DB_NAME

hass --script influxdb_migrator -H 192.168.2.55 -p 8086 -ha
```

```
hass --script influxdb_import --simulate --config /root/.homeassistant -H 192.168.2.55 -p 8086 -d ha --exclude_domains automation,configurator,sensor.yr_symbol,sun.sun,
```

https://home-assistant.io/blog/2015/12/07/influxdb-and-grafana/

## Groups

https://home-assistant.io/components/group/

#### Icons

```
icon: mdi:home
```

https://materialdesignicons.com/
