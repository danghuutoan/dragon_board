# useful link
- http://www.96boards.org/forums/topic/ap-mode-on-linux/#gsc.tab=0
- http://www.96boards.org/forums/topic/dragonboard-wifi-access-point-linux/#gsc.tab=0
# Disable graphical network management 

# Useful link
https://askubuntu.com/questions/180733/how-to-setup-an-access-point-mode-wi-fi-hotspot/180734#180734
http://www.96boards.org/forums/topic/ap-mode-on-linux/#gsc.tab=0
## /etc/hostapd/hostapd.conf
```
interface=wlan0
driver=nl80211
ssid=test
hw_mode=g
channel=1
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=3
wpa_passphrase=1234567890
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
```

Edit the file /etc/default/hostapd and modify the line of DAEMON_CONF like this:
```
DAEMON_CONF="/etc/hostapd/hostapd.conf"
```


