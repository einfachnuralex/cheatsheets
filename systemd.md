
# Troubleshooting

## reset-failed

If a service failed too often, systemd will not start the service until the failed state is reset.

```
systemctl reset-failed ceph-mgr@ceph1
```

# systemd timers

## systemd like cron

https://coreos.com/os/docs/latest/scheduling-tasks-with-systemd-timers.html
https://wiki.archlinux.org/index.php/Systemd/Timers

/etc/systemd/system/foo.timer

```
[Unit]
Description=Run foo weekly

[Timer]
OnCalendar=weekly
Persistent=true

[Install]
WantedBy=timers.target
```

OnCalendar format

```
OnCalendar=DayOfWeek Year-Month-Day Hour:Minute:Second
OnCalendar=Mon,Tue *-*-01..04 12:00:00
```

Test format/date

```
systemd-analyze calendar "Mon,Tue *-*-01..04 12:00:00"
```
