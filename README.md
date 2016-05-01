# RasberryPiSetup

## OS

Format SD card with FAT32. 

Exec `sudo dd bs=1m if=/Users/Chrissi/Downloads/2016-03-18-raspbian-jessie.img of=/dev/rdisk2` on the terminal. 

- [PiBaker](http://www.tweaking4all.com/hardware/raspberry-pi/macosx-apple-pi-baker/)
- [Raspbian Jessie](https://www.raspberrypi.org/downloads/raspbian/)
- [Raspberry SD Cards](https://www.raspberrypi.org/documentation/installation/sd-cards.md)

##Setup

Connect to Pi: `ssh IP` password is `raspberry`

`sudo raspi-config`

- change password
- change boot option to `desktop auto`
- change locale
- change timezone
- advanced > memory split 256

`sudo nano /boot/config.txt` add `display_rotate=1` and `hdmi_force_hotplug=1`

`sudo nano /etc/xdg/lxsession/LXDE-pi/autostart`

Disable everything here with a `#`.

add
```
@xset s off
@xset -dpms
@xset s noblank
```


Use `sudo apt-get update && apt-get upgrade -y` to upgrade system.



### WiFi

Add network settings: `sudo nano /etc/wpa_supplicant/wpa_supplicant.conf`

```shell
network={
    ssid="The_ESSID_from_earlier"
    psk="Your_wifi_password"
}
```

### Usage

Type `sudo halt` to stop the pi.
