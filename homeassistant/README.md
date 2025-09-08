## Control USB devices and symbolic link mounts for known devices
```console
foo@bar:~$ lsusb
```
```console
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 003: ID 2109:3431 VIA Labs, Inc. Hub
Bus 001 Device 004: ID 1a86:7523 QinHeng Electronics CH340 serial converter
Bus 001 Device 005: ID 0658:0200 Sigma Designs, Inc. Aeotec Z-Stick Gen5 (ZW090) - UZB
Bus 001 Device 006: ID 1a86:55d4 QinHeng Electronics USB Single Serial
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 002 Device 002: ID 04e8:61f5 Samsung Electronics Co., Ltd Portable SSD T5
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```
Get relevant device ID's and put them (add them to) local rules file in udev:
```console
foo@bar:~$ sudo nano /etc/udev/rules.d/10-local.rules
```
so it looks like
```console
ACTION=="add", SUBSYSTEM=="tty", ATTRS{idVendor}=="0451", ATTRS{idProduct}=="16a8", SYMLINK+="cc2531", GROUP="dialout", MODE="0666"
ACTION=="add", SUBSYSTEM=="tty", ATTRS{idVendor}=="0658", ATTRS{idProduct}=="0200", SYMLINK+="zw090", GROUP="dialout", MODE="0666"
ACTION=="add", SUBSYSTEM=="tty", ATTRS{idVendor}=="1a86", ATTRS{idProduct}=="7523", SYMLINK+="rflink", GROUP="dialout", MODE="0666"
ACTION=="add", SUBSYSTEM=="tty", ATTRS{idVendor}=="1a86", ATTRS{idProduct}=="55d4", SYMLINK+="cc2652", GROUP="dialout", MODE="0666"
```
Then symbolic links like /dev/zw090 will be created on mount/boot and can be used inside containers (docker-compose.yaml).
