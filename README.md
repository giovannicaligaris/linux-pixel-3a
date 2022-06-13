<p align="center"><img src="https://user-images.githubusercontent.com/26255347/151196900-1128790c-eb07-4f7c-9966-d93cf9f381d6.png" width=40% height=40%></p>

# Linux on Google Pixel 3a (Bonito &amp; Sargo) 
Instructions on how to install Droidian, Manjaro ARM and UBPorts on Google Pixel 3a and 3a XL (Bonito & Sargo)

## Android 9
<p>For all 3 systems, Android 9 is required. 
   <br><b>BEWARE:</b> Installing and downgrading to Android 9 will wipe your entire phone.</p>

## Download
<p>TWRP (latest .img - rename it twrp.img) - https://dl.twrp.me/sargo/
<br>Android 9 (choose the latest 9.0 link) - https://developers.google.com/android/images </p>

## Unlock OEM
1. Enable OEM unlock in the Developer options under device Settings, if present.
2. Connect the device to your PC via USB.
3. On the computer, open a command prompt (on Windows) or terminal (on Linux or macOS) window, and type:
```adb reboot bootloader```
   You can also boot into fastboot mode via a key combination: With the device powered off, hold ```Volume Down + Power```
4. Once the device is in fastboot mode, verify your PC finds it by typing:
```fastboot devices```
5. Now type the following command to unlock the bootloader: ```fastboot flashing unlock``` 
6. If the device doesn’t automatically reboot, reboot it. It should now be unlocked.

## Flash Android 9
You will need to flash Android on both A & B partitions. Open the terminal inside the download Android 9 folder.

1. Flash partition B first
2. ```fastboot -ab```
3. ```fastboot reboot bootloader```
4. ```./flash-all.sh```
5. This will take a few minutes and it will then boot into Android. There is no need to setup the phone. Just go back into the bootloader by holding hold ```Volume Down + Power```
6. Flash A partition
7. ```fastboot -aa```
8. Follow steps 3 to 5 again

## Droidian
<p>Download the following files from https://github.com/droidian-images/rootfs-api28gsi-all/releases/tag/nightly
<br> This will install Debian Bookworm</p>

1. droidian-rootfs-api28gsi-arm64.zip
2. droidian-adaptation-google-sargo-arm64.zip

It is recommended to expand the rootfs size from <b>8GB to 48GB</b> inside <b>droidian-rootfs-api28gsi-arm64.zip.</b> Double click on the zip and enter inside the file <b>setup.sh.</b> Replace <b>8GB to 48GB.</b> Save and close the file. Then press <b>Update.</b> Make sure to do this everytime you download the latest droidian-rootfs-api28gsi-arm64.zip. `vim` can enable easier editing of the `zip` file without causing any error. Navigate to command prompt with vim, ```vim droidian-filename```, move the cursor to `setup.sh` and edit the line ```resize2fs -f /data/rootfs.img 48G```

<b>ATTENTION: If you are using Ubuntu 20.04 you will need the latest fastboot, otherwise you won't be able to flash Droidian. </b>
1. Download SDK Platform Tools for Linux from https://developer.android.com/studio/releases/platform-tools
2. Place your Droidian and TWRP files inside the downloaded folder. 
3. ```./``` infront of fastboot will be require

### Flashing Droidian</b>
1. ```fastboot -aa```
2. ```fastboot reboot bootloader```
3. ```fastboot format:ext4 userdata```
4. ```fastboot boot twrp.img```
5. Wait until it TWRP boots
6. Go into Advance and ADB Sideload
7. ```adb sideload droidian-rootfs-*.zip``` then sideload ```droidian-adaptation-*.zip```
8. When is done reboot ```slot A```
9. The phone will restart 2 or 3 times. 
10. Password: ```1234```
11. Open Software and upgrade system.
   
### SSH
It is recommended to setup SSH right after connecting to WIFI. Make sure your phone is connected with a USB cable.

```ssh droidian@10.15.19.82```

### Known Issues
1. Camera & Flashlight do not work
2. Battery life is short (better on Pixel 3a XL)
3. Waydroid installs but is very slow.
4. Finger reader does not work (on all Droidian devices)
5. Some KDE flatpak apps won't launch

### Add Staging Repo (Optional)

Change release to <b>bullseye</b> or <b>bookworm</b> depending on your release version. Add:

```deb http://staging.repo.droidian.org/ release main```

to ```/etc/apt/source.list```

### Join Droidian on Telegram
https://t.me/droidianlinux

## Manjaro ARM
Manjaro ARM is a bit slower than Droidian and it has the same known issues.

### Install
1. Download ```Manjaro-ARM-phosh-google-sargo-9.zip``` or ```Manjaro-ARM-nemomobile-google-sargo-9.zip``` from https://github.com/manjaro-libhybris/image-ci/releases
2. Enter into the phone's bootloader
3. ```fastboot -aa```
4. ```fastboot reboot bootloader```
5. ```fastboot format:ext4 userdata```
6. ```fastboot boot twrp.img```
7. Wait until it TWRP boots
8. Go into Advance and ADB Sideload
9. ```adb sideload Manjaro-ARM-*.zip```
10. Sideload might get stuck at 47%, just wait patiently
11. Reboot the phone after sideloading
12. Password: ```123456```

### Join Manjaro-ARM on Telegram
https://t.me/manjaroonhalium

## UBPorts
UBPorts has the most amount of support for Sargo & Bonito

https://devices.ubuntu-touch.io/device/sargo/

### Install
Check the UBPorts page on how to use their installer

https://devices.ubuntu-touch.io/installer/?pk_vid=7745a6d54b073d6c1642764968dafd25

### Join UBPorts on Telegram
https://t.me/ubports

##

[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fgiovannicaligaris%2Flinux-pixel-3a&count_bg=%23A56DE2&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=Views&edge_flat=false)](https://hits.seeyoufarm.com)

