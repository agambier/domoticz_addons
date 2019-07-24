# SystemD configuration files

## Auto restart domoticz service

Domoticz crashes if system time is changed (NTP synchronization after a long network loss or during boot).
- [Issue #3371](https://github.com/domoticz/domoticz/issues/3371).
- [Booting from LUN is crashing domoticz](https://www.domoticz.com/forum/viewtopic.php?f=6&t=28738l)

A workaround is to add a systemd drop-in file to restart domoticz service in case of crash.

to Install it:
1. create `domoticz.service.d` with `sudo mkdir /etc/systemd/system/domoticz.service.d/`
2. copy `./domoticz.service.d/restart.conf` to `/etc/systemd/system/domoticz.service.d/`
3. reload systemd daemon with `sudo systemctl daemon-reload`
4. check drop-in is loaded with `sudo systemctl status domoticz`. The two lines below should be present.
```
Drop-In: /etc/systemd/system/domoticz.service.d
           └─restart.conf
```

Now if domoticz crashes for any reason it will get restarted after 5 seconds but if it's correctly stopped it won't get restarted.
