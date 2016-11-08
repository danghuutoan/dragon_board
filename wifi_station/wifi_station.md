# Instruction to configure wifi manually for dragon board
## Step 1:
chmod 0600 /etc/network/interfaces
## Step 2:
modify `/etc/network/interfaces` as bellow:

```
allow-hotplug wlan0
auto wlan0
iface wlan0 inet dhcp
	wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
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
# Test
you can ping `www.google.com` to see if the wifi configuration is working or not
```bash
$ ping www.google.com
```
if you see something like `Ping: icmp open socket: Operation not permitted` then just enter the bellow command

```bash
sudo chmod u+s `which ping`
```
# References:
1. https://wiki.debian.org/WiFi/HowToUse
2. https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md


