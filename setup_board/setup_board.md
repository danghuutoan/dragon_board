# fast boot
https://github.com/96boards/documentation/wiki/Dragonboard-410c-Installation-Guide-for-Linux-and-Android#install-android-or-debian-using-fastboot
# configure wifi 
https://wiki.debian.org/WiFi/HowToUse
https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md
## Auto-start wifi
`/etc/network/interfaces`:
```
auto lo

iface lo inet loopback
iface eth0 inet dhcp

allow-hotplug wlan0
iface wlan0 inet manual
wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
iface default inet dhcp
```
## Board ip address
192.168.0.105
# smb server
http://askubuntu.com/questions/203585/how-do-i-connect-to-an-smb-share-requiring-a-user-name-and-password