# RasberryPiSetup

## OS

Format SD card with FAT32. 

Exec `sudo dd bs=1m if=/Users/Chrissi/Downloads/2016-03-18-raspbian-jessie.img of=/dev/rdisk2` on the terminal. 

- [PiBaker](http://www.tweaking4all.com/hardware/raspberry-pi/macosx-apple-pi-baker/)
- [Raspbian Jessie](https://www.raspberrypi.org/downloads/raspbian/)
- [Raspberry SD Cards](https://www.raspberrypi.org/documentation/installation/sd-cards.md)

## Setup

### SSH

SSH is deactivated by default. To activate ssh via filesystem create a file `ssh` on the SD card.

`touch ssh`

Connect to Pi: `ssh IP` password is `raspberry`

### raspi-config

`sudo raspi-config`

- change password
- change boot option to `desktop auto`
- change locale
- change timezone
- advanced > memory split 256

### System Upgrade

use `sudo apt-get update && apt-get upgrade -y`

### Display Settings

use `sudo nano /boot/config.txt` 

and add 
```
display_rotate=1
hdmi_force_hotplug=1
overscan_left=-25
overscan_right=-25
overscan_top=-25
overscan_bottom=-25
```

### /etc/xdg/lxsession/LXDE-pi/autostart

`sudo nano /etc/xdg/lxsession/LXDE-pi/autostart`

Disable everything here with a `#`.

add
```
@xset s off
@xset -dpms
@xset s noblank
```

### /etc/lightdm/lightdm.conf

Edit _/etc/lightdm/lightdm.conf_.

`sudo nano /etc/lightdm/lightdm.conf`

Below `[SeatDefault]` add `xserver-command=X -s 0 -dpms`.

### Power Saving

Disable power saving to avoid ssh dropouts.

`sudo nano /etc/modprobe.d/8192cu.conf`

```
# Disable power saving 
options 8192cu rtw_power_mgnt=0 rtw_enusbss=1 rtw_ips_mode=1
```

### WiFi

Add network settings: 

`sudo nano /etc/wpa_supplicant/wpa_supplicant.conf`

```shell
network={
    ssid="The_ESSID_from_earlier"
    psk="Your_wifi_password"
}
```

### Usage

Type `sudo halt` to stop the pi.
Type `pm2 restart mm` to restart magic mirror.
