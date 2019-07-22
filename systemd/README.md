# SystemD configuration files

## Auto restart domoticz service

Domoticz crashes if system time is changed (NTP synchronization after a long network loss or during boot).
- [Issue #3371](https://github.com/domoticz/domoticz/issues/3371).

A workaround is to add a systemd drop-in file to restart domoticz service in case of crash.




