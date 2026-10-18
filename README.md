# ADB Platform Tool

> ADB is Android Debug Bridge, a command-line tool that enables direct communication between a development machine and an Android device.


### Setup
- Extract folder `platform-tools` to root of any drive `with sys & admin permissions`

- `enable/activate` Developer Menu (from "About" android menu)
- USB debugging (from Developer menu) `enabled`
- `accept` incomming connection on target device, mainly when connecting/running first command => `adb connect`



### Useful commands

> adb connect <DEVICE_IP>:PORT
> adb shell



## 
Notes : sometimes it helps to execute commands from adb.exe and not in the shell directly -> skip `adb shell` commands as parameters and only run direct command with `adb.exe <COMMAND>` 