# QCA6174_aircrack
From https://forum.aircrack-ng.org/index.php/topic,1705.0.html

This was tested and works on an XPS 15 9560 with a Killer Wireless 1535 QCA6174

STEPS:
1- Download https://github.com/kvalo/ath10k-firmware/blob/master/QCA6174/hw3.0/4.4.1.c3/firmware-6.bin_WLAN.RM.4.4.1.c3-00059

2- Make a copy of /lib/firmware/ath10k/QCA6174/hw3.0/firmware-6.bin

3- Change downloaded file name, permissions(chmod), owner(chown) and group(chgrp) to match the original firmware-6.bin

4- Run this (replace wlp2s0 with your interface name):
```bash
sudo airmon-ng stop wlp2s0 && sudo airmon-ng check kill && sudo modprobe -r ath10k_pci && sudo modprobe -r ath10k_core
```

5- Replace /lib/firmware/ath10k/QCA6174/hw3.0/firmware-6.bin with the downloaded file

6- Restart PC

7- Unblock rfkill
```bash
sudo rfkill list
sudo rfkill unblock wifi; sudo rfkill unblock all
```

8- Run the following to enable/disable monitoring (replace wlp2s0 with your interface name):

ENABLE:
```bash
sudo modprobe -r ath10k_pci
sudo modprobe -r ath10k_core
sudo modprobe ath10k_core rawmode=1 cryptmode=1
sudo modprobe ath10k_pci
sudo airmon-ng check kill
sudo airmon-ng start wlp2s0
```

DISABLE:
```bash
sudo modprobe -r ath10k_pci
sudo modprobe -r ath10k_core
sudo modprobe ath10k_core rawmode=0 cryptmode=0
sudo modprobe ath10k_pci
sudo airmon-ng stop wlp2s0
sudo service network-manager start
```
9- Proceed
```bash
sudo airodump-ng wlp4s0
```
