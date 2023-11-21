# Introduction
- This project is used to automatically generate the **ArchLinuxARM** **aarch64** system image for the **Raspberry Pi** once a day
- The generated images contain the official closed-source firmware from Raspberry Pi

 ## download links

- **ArchLinuxARM-rpi-aarch64-latest.img.zip**：
  - https://github.com/eva0034/ArchlinuxARM-rpi-aarch64/releases/latest/download/ArchLinuxARM-rpi-aarch64-latest.img.zip
- **ArchLinuxARM-rpi-aarch64-latest.img.zip.sha256sum**：
  - https://github.com/eva0034/ArchlinuxARM-rpi-aarch64/releases/latest/download/ArchLinuxARM-rpi-aarch64-latest.img.zip.sha256sum
- **ArchLinuxARM-rpi-aarch64-latest.tar.gz**：
  - https://github.com/BurningC4/ArchlinuxARM-rpi-aarch64/releases/latest/download/ArchLinuxARM-rpi-aarch64-latest.tar.gz
- **ArchLinuxARM-rpi-aarch64-latest.tar.gz.sha256sum**：
  - https://github.com/BurningC4/ArchlinuxARM-rpi-aarch64/releases/latest/download/ArchLinuxARM-rpi-aarch64-latest.tar.gz.sha256sum

 ## The following software packages and their dependencies are installed

  ```
  base linux-rpi raspberrypi-bootloader crda dhcpcd dialog haveged iptables-nft nano net-tools netctl openssh rpi-eeprom vi which wireless_tools wpa_supplicant
  ```
  

 ## The following software packages and their dependencies are installed...


  ```
  haveged sshd systemd-networkd systemd-resolved systemd-timesyncd
  ```

  ## Basically equivalent to the official **rpi-aarch64** Mirror Installed **linux-rpi**

  ### IMG Additional customizations
  
  added and enabled **resize2fs_once.service**
  
  ```
  [Unit]
  Description=Resize the root filesystem to fill partition

  [Service]
  Type=oneshot
  ExecStart=/usr/local/bin/growpart /dev/mmcblk0 2 ; /usr/sbin/resize2fs /dev/mmcblk0p2
  ExecStartPost=/usr/bin/systemctl disable resize2fs_once.service ; /usr/bin/rm -rf /etc/systemd/system/resize2fs_once.service /usr/local/bin/growpart

  [Install]
  WantedBy=multi-user.target
  ```
  
  This file extends the root partition to the entire sd card size and deletes itself when completed
  
  Added From **cloud-guest-utils** 的 **growpart** ，This file is deleted when booting for the first time **resize2fs_once.service** Deletes after use
 
 ## Usage

 Default Root User : root
 Default Root Password : root
  
 Default Username : alarm 
 Default User Password : alarm
  
  Not installed by default **sudo**
