
#

## Wifi

https://linuxundich.de/raspberry-pi/drei-wege-das-wlan-auf-einem-raspberry-pi-einzurichten/

https://pi-buch.info/wlan-schon-vor-der-installation-konfigurieren/

> wpa_supplicant.conf

```
# Datei wpa_supplicant.conf in der Boot-Partition (Raspbian Stretch)
country=DE  #omit if US
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
  ssid="wlanssid"
  scan_ssid=1
  proto=RSN
  key_mgmt=WPA-PSK
  pairwise=CCMP
  psk="7657646746546"
}
```

## SSH

Empty file

> ssh

# Watchdog

```
apt install watchdog
```

/etc/watchdog.conf

```
ping                    = 192.168.2.1
interface               = wlan0
watchdog-device = /dev/watchdog
log-dir         = /var/log/watchdog
realtime                = yes
priority                = 1
watchdog-timeout = 15
```
