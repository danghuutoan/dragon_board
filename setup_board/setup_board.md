# fast boot
https://github.com/96boards/documentation/wiki/Dragonboard-410c-Installation-Guide-for-Linux-and-Android#install-android-or-debian-using-fastboot
# configure wifi 
https://wiki.debian.org/WiFi/HowToUse
https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md
## Auto-start wifi
```bash
# chmod 0600 /etc/network/interfaces
```
`/etc/network/interfaces`:
```
auto lo

iface lo inet loopback


allow-hotplug wlan0
iface wlan0 inet dhcp
wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
iface default inet dhcp
```
## Ping: icmp open socket: Operation not permitted
```bash
sudo chmod u+s `which ping`
```
## Board ip address
192.168.0.105
# smb server
http://askubuntu.com/questions/203585/how-do-i-connect-to-an-smb-share-requiring-a-user-name-and-password
# Customize the kernel

http://www.96boards.org/db410c-getting-started/Configuration/EnableSPI.md/
# Dragon board tutorial
https://www.linux.com/learn/embedded-linux-using-dragonboard-410c