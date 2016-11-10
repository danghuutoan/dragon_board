# Follow the instruction in this link to get internet access
https://github.com/96boards/documentation/blob/master/ConsumerEdition/CE-Extras/Configuration/WifiCommandline.md

```
$ nmcli dev wifi list
$ nmcli con add con-name <connection's name> ifname wlan0 type wifi ssid <connection's SSID>
$ nmcli con modify <connection's name> wifi-sec.key-mgmt wpa-psk
$ nmcli con modify <connection's name> wifi-sec.psk <your password>
$ nmcli con up <connection's name>
```

# Install required package

## hostapd
## dnsmasq

```bash
sudo apt-get update
sudo apt-get install hostapd dnsmasq
```

# Configure static IP

Add the following line  into file `/etc/network/interfaces`

```
allow-hotplug wlan0  
iface wlan0 inet static 
	hostapd /etc/hostapd/hostapd.conf 
    address 192.168.1.1
    netmask 255.255.255.0
    network 192.168.1.0
    broadcast 192.168.1.255
```

# Configure hostapd

Create a new configuration file with sudo nano /etc/hostapd/hostapd.conf with the following contents:

```
interface=wlan0
driver=nl80211
ssid=DG-AP
hw_mode=g
channel=6
ieee80211n=1
wmm_enabled=1
ht_capab=[HT40][SHORT-GI-20][DSSS_CCK-40]
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_key_mgmt=WPA-PSK
wpa_passphrase=12345678
rsn_pairwise=CCMP
```
# Configure dnsmasq

Create new file `/etc/dnsmasq.conf `

Paste the following into the new file:

```
interface=wlan0      # Use interface wlan0  
listen-address=192.168.1.1 # Explicitly specify the address to listen on  
bind-interfaces      # Bind to the interface to make sure we aren't sending things elsewhere  
server=8.8.8.8       # Forward DNS requests to Google DNS  
domain-needed        # Don't forward short names  
bogus-priv           # Never forward addresses in the non-routed address spaces.  
dhcp-range=192.168.1.50,192.168.1.150,12h # Assign IP addresses between 172.24.1.50 and 172.24.1.150 with a 12 hour lease time  
```


disable NetworkManager

```
$ sudo systemctl stop NetworkManager.service
$ sudo systemctl disable NetworkManager.service
```

Resboot to apply the new configuration

```bash
$ sudo reboot
```

# test if the hostapd.conf file is working or not 

```bash
$ sudo /usr/sbin/hostapd /etc/hostapd/hostapd.conf
```

If it works then just start the hostapd and dnsmasq deamon

```bash
sudo service hostapd start  
sudo service dnsmasq start
```

You can use the following command to check if hostapd and dnsmasq is started or not

```bash
sudo service hostapd status  
sudo service dnsmasq status
```

or use `ps` to see if they are running or not

```bash
ps aux | grep hostapd
ps aux | grep dnsmasq
```
you may want to see the error log for debugging

```bash
$ sudo tail /var/log/syslog
```


reboot and see the result

enter

```bash
sudo iw wlan0 info
```

you should see something like this

```bash
Interface wlan0
	ifindex 3
		wdev 0x01
		ssid DG-AP
		type AP
		wiphy 0
```
# References:
1. https://frillip.com/using-your-raspberry-pi-3-as-a-wifi-access-point-with-hostapd/
2. http://www.96boards.org/forums/topic/ap-mode-on-linux/#gsc.tab=0
3. https://github.com/96boards/documentation/blob/master/ConsumerEdition/CE-Extras/Configuration/WifiCommandline.md