# SystemD configuration files

## Auto restart domoticz service

Domoticz crashes if system time is changed (NTP synchronization after a long network loss or during boot).
- [Issue #3371](https://github.com/domoticz/domoticz/issues/3371).

A workaround is to add a systemd drop-in file to restart domoticz service in case of crash.

to Install it:
1. copy `./domoticz.service.d/restart.conf` to `/etc/systemd/system/domoticz.service.d/`
2. reload systemd daemon with `sudo systemctl daemon-reload`
3. check drop-in is loaded with `sudo systemctl status domoticz`. The two lines below should be present.
```
Drop-In: /etc/systemd/system/domoticz.service.d
           └─restart.conf
```

Now if domoticz crashes for any reason it will get restarted after 5 seconds but it is correctly stopped it won't get restarted.
