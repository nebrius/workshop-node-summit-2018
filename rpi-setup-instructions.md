On the SD card from a laptop:

```
touch ssh
```

On the Raspberry Pi:

```
Change password and wifi with raspi-config
Change hostname (rpi##)
```

Reboot. On the Raspberry Pi again:

```
sudo apt-get update && curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get -y upgrade && sudo apt-get install -y vim git nodejs samba samba-common-bin
mkdir /home/pi/nodebot && sudo vim /etc/samba/smb.conf

# Add to smb.conf
[nodebot]
Comment = NodeBots source folder
Path = /home/pi/nodebot
Browseable = yes
Writeable = Yes
only guest = no
create mask = 0777
directory mask = 0777
Public = yes
Guest ok = yes
```
