# RaspberryPiSetup

## OS

Get [Raspberry Pi Imager](https://www.raspberrypi.com/software/) and format SD with a recent version of Raspberry Pi OS.

### Advanced Settings

Press `Shift + CTRL + X` to open advanced settings.

- enable SSH
- change name
- change locale
- change timezone
- set WIFI
- set password

## Setup

### SSH

SSH is deactivated by default. To activate ssh via filesystem create a file `ssh` on the SD card.

`touch ssh`

Connect to Pi: `ssh IP` password is `raspberry`

### raspi-config

see https://www.radishlogic.com/raspberry-pi/how-to-disable-screen-sleep-in-raspberry-pi/

`sudo raspi-config`

- change password
- change boot option to `desktop auto`
- change locale
- change timezone
- advanced > memory split 256

### System Upgrade

use `sudo apt-get update && apt-get upgrade -y`

### Display Settings

see https://raspberrypi.stackexchange.com/a/111438/142968
https://pimylifeup.com/raspberry-pi-rotate-screen/

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

`display_rotation` does no longer work, instead this helped: https://raspberrypi.stackexchange.com/a/111438/142968

### Disable ScreenSaver

see https://www.geeks3d.com/hacklab/20160108/how-to-disable-the-blank-screen-on-raspberry-pi-raspbian/
 
#### /etc/xdg/lxsession/LXDE-pi/autostart

`sudo nano /etc/xdg/lxsession/LXDE-pi/autostart`

Disable everything here with a `#`.

add
```
@xset s off
@xset -dpms
@xset s noblank
```

#### /etc/lightdm/lightdm.conf

Edit _/etc/lightdm/lightdm.conf_.

`sudo nano /etc/lightdm/lightdm.conf`

Below `[SeatDefault]` add `xserver-command=X -s 0 -dpms`.

### Power Saving

see https://www.radishlogic.com/raspberry-pi/how-to-disable-screen-sleep-in-raspberry-pi/
see https://www.elektronik-kompendium.de/sites/raspberry-pi/1912231.htm

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

### Disk Size

see https://forum-raspberrypi.de/forum/thread/25004-kein-speicherplatz-mehr-verfuegbar/

### Usage

Type `sudo halt` to stop the pi.
Type `pm2 restart mm` to restart magic mirror.
