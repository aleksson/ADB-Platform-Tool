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
> https://dnsleaktest.com/ (extended test)
or
> https://browserleaks.com/dns
verify that <b>AdGuard DNS shows up and not ISP's DNS servers</b>

> https://ipleak.net/
Shows your public IP ans DNS Servers.


### Verify with ADB
> `adb shell dumpsys netd` and `adb shell dumpsys connectivity`

if you see `validated=true` for `dns.adguard-dns.com` the encrypted DoT connection is active


## Reset Private DNS
These commands restores previous settings and deleted the DNS specifier to default

> `adb shell settings put global private_dns_mode opportunistic`

> `adb shell settings delete global private_dns_specifier`


#### Verify if settings was restored / deleted
> `adb shell settings get global private_dns_mode`

expected output:
`opportunistic`


then 
> `adb shell settings get global private_dns_specifier`

expected output:
`null` - this means the cutoms hostname is no longer stored

From here <b>restart the TV (`adb reboot`) or disconnect and reconnect</b> to wifi again


## DNS Server Providers
- Cloudflare DoT (one.one.one.one) AS13335
- NextDNS
- AdGuard
- Google
- Quad9

## 
Notes : sometimes it helps to execute commands from adb.exe and not in the shell directly -> skip `adb shell` commands as parameters and only run direct command with `adb.exe <COMMAND>` 