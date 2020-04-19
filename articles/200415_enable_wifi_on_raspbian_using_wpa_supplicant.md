
# Enable Wifi on Raspbian Using WPA Supplicant

## Step 1
Edit your `wpa_supplication` config file.

    sudo nano /etc/wpa_supplicant/wpa_supplicant.conf 
    
## Step 2
Then copy and paste the configurations below and edit the `SSID` and `WIFI PASSWORD`.

    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1
    country=PH
    
    network={
        ssid="[SSID]"
        psk="[WIFI PASSWORD]"
        scan_ssid=1
        proto=RSN
        key_mgmt=WPA-PSK
        pairwise=CCMP
        auth_alg=OPEN
    }

*Note: Double check your own Wifi settings and change the network configuration as you see fit. See WPA Supplicant Config Documentation for details. Also use `iwlist [NET INTERFACE] scan` to get more infor on your Wifi settings*

### References

1. [WPA Supplicant Configuration Documentation](http://w1.fi/cgit/hostap/plain/wpa_supplicant/wpa_supplicant.conf)

---
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NTQ5MDkxODMsLTE4ODY1OTYzMjhdfQ
==
-->