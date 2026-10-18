# ADB Platform Tool

> ADB is Android Debug Bridge, a command-line tool that enables direct communication between a development machine and an Android device.



### Connect To Android TV

> adb connect <TV_IP>:5555
> adb shell

##

Here are steps for configuring <b>DoT</b> (DNS-over-TLS) and/or <b>DoH</b> (DNS-over-HTTPS) with custom DNS providers

Before investigation or changing any tv settings with `adb`, first lookup these userfriendly alternatives / apps :

- TDUK DNS Swicher
- DNS Switcher - Network Tools


## 

### Configure DoT / Private DNS
1. `settings put global private_dns_mode hostname`

2. `settings put global private_dns_specifier dns.adguard-dns.com`

### Reboot TV or Restart Device
`adb reboot`

#### Verify if settings was applied
> `adb shell settings get global private_dns_mode`

expected output:
`hostname`


then 
> `adb shell settings get global private_dns_specifier`

expected output:
`dns.adguard-dns.com`


### Verify applied DNS settings
Open any browser on TV and visit :
> https://dnsleaktest.com/
or
> https://browserleaks.com/dns
verify that <b>AdGuard DNS shows up and not ISP's DNS servers</b>


### Verify with ADB
> `adb shell dumpsys netd` and `adb shell dumpsys connectivity`

if you see `validated=true` for `dns.adguard-dns.com` the encrypted DoT connection is active

## 
Notes : sometimes it helps to execute commands from adb.exe and not in the shell directly -> skip `adb shell` commands as parameters and only run direct command with `adb.exe <COMMAND>` 