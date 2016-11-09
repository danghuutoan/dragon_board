# Instruction to configure wifi manually for dragon board
## Step 1:
chmod 0600 /etc/network/interfaces
## Step 2:
Use the WPA passphrase to calculate the correct WPA PSK hash for your SSID by altering the following example: 

```
$ wpa_passphrase myssid my_very_secret_passphrase
```
then you will get something like this

```
network={
        ssid="myssid"
        #psk="my_very_secret_passphrase"
        psk=ccb290fd4fe6b22935cbae31449e050edd02ad44627b16ce0151668f5f53c01b
}
```
## Step 3:
```
allow-hotplug wlan0
auto wlan0
iface wlan0 inet dhcp
        wpa-ssid myssid
        wpa-psk ccb290fd4fe6b22935cbae31449e050edd02ad44627b16ce0151668f5f53c01b
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

# Turn off network manager

refer to this link 
http://xmodulo.com/disable-network-manager-linux.html

```
$ sudo systemctl stop NetworkManager.service
$ sudo systemctl disable NetworkManager.service
```
