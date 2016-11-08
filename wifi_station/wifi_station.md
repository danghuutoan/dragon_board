# Instruction to configure wifi manually for dragon board
## Step 1:
chmod 0600 /etc/network/interfaces
## Step 2:
modify `/etc/network/interfaces` as bellow:

```
allow-hotplug wlan0
iface wlan0 inet dhcp
wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
iface default inet dhcp
```
## Step 3:
Create `etc/wpa_supplicant/wpa_supplicant.conf` file
Modify its content as bellow

```
network={
    ssid="yourssid"
    psk="yourwifipassword"
}
```
## Step 4:
```bash
$ sudo ifup wlan0
```
or
```bash
$ sudo reboot
```
# References:
1. https://wiki.debian.org/WiFi/HowToUse
2. https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md


