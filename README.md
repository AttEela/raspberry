# raspberry
Short description of how to start with a Raspberry Pie when you don't have keybord nor mouse.  

### Burn the image on the sd card

First, format the SD Card with SD Card Formater (https://www.sdcard.org/downloads/formatter/)

Then, follow instuctions from :
https://www.raspberrypi.org/documentation/installation/installing-images/README.md  
I took Raspbian Stretch Lite image.

At the end of this stage, you'll have an SD Card with a `/boot` partition. Don't disconnect the SD Card, you'll need it for the next step.

### Configurations for SSH and Wifi

Before turning on the RPi, you must do some configurations to connect with SSH.
SSH connections on the RPi are disabled by default, so first you'll need to enable it.

From you laptop, add a file `ssh` (without any extension and with nothing in it) to the root of the `/boot` partition of the SD Card:
```
touch ssh
```

Then, you will have to configure the Wifi connection, to do so, create a file `wpa_supplicant.conf` where you just placed the `ssh` file.

```
vi wpa_supplicant.conf
```

The file `wpa_supplicant.conf` will contain the following lines:
```
country=fr
update_config=1
ctrl_interface=/var/run/wpa_supplicant

network={
 scan_ssid=1
 ssid="your_box_ssid"
 psk="you_wifi_password"
}
```

Replace `your_box_ssid` and `you_wifi_password` with yours. (keep the quotes).  
Note : `country=fr` is for France, you can change this as you want.

### SSH Connection to the Rpi with your laptop

Turn on the RPi, wait for a minute, red light should be on and the green one should blink.

Find the IP of the RPi with you Router's DHCP configuration. You can take this opportunity to attribute to the RPi a static IP.

Then connect with :
```
ssh pi@YOUR_RPI_IP
```

If this is your first time (as it should be), the password should be `raspberry`.  
You can then change this password with `passwd`command.

### Installations of tools

`sudo apt-get update`  
`sudo apt-get install git`  
`sudo apt-get install tmux`  
`sudo apt-get install vim-gui-common`  
`sudo apt-get install vim-runtime`

For Python 3.6, find instructions here :http://www.knight-of-pi.org/installing-python3-6-on-a-raspberry-pi/ :  
```
sudo apt-get install python3-dev libffi-dev libssl-dev -y
wget https://www.python.org/ftp/python/3.6.3/Python-3.6.3.tar.xz
tar xJf Python-3.6.3.tar.xz
cd Python-3.6.3
./configure
make
sudo make install
sudo pip3 install --upgrade pip
```
