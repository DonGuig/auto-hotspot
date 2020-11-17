# Auto Access Point
This script is intended for the Raspeberry Pi. It will automatically create a hotspot, based on the given conf file. 
It will use [`systemd-networkd`][1], `wpa_supplicant` and `wpa_cli`.
The hotspot will be purely local, no internet connection.

[Not Tested] Check if ethernet connectivity also works

You need to have a wpa_supplicant-_device_.conf file similiar to this.

```
country=FR                                                                        
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev                           
update_config=1                                                                   
ap_scan=1

### auto hotspot ###      # has to be the first network section!                                                                                  
network={
    priority=0            # Lowest priority, so wpa_supplicant prefers the other networks below 
    ssid="autohotspot"    # your access point's name                                                            
    mode=2                                                                       
    key_mgmt=WPA-PSK                                                             
    psk="passphrase"      # your access point's password                                    
    frequency=2462                                                               
}

```

After having installed the script (see below) you can start a hotspot manually by running `auto-hotspot` 

[Not tested] If there is a wired network connection the Pi will work as a repeater

How it works is also discussed here: 
https://raspberrypi.stackexchange.com/questions/100195


## Install

```
git clone https://github.com/DonGuig/auto-hotspot.git
cd auto-hotspot
chmod +x auto-hotspot install.sh
sudo ./install.sh
```

[1]:https://raspberrypi.stackexchange.com/questions/108592/use-systemd-networkd-for-general-networking/108593

