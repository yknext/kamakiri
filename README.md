# kamakiri
Another bootrom exploit for MediaTek devices 

https://forum.xda-developers.com/fire-tv/development/unlock-fire-tv-stick-2nd-gen-tank-t3907002/page3

Visualbox test success

Quote:
Originally Posted by k4y0z 
Read this whole guide before starting.

This is for the 2nd gen Fire TV Stick (tank)

What you need:

A Linux installation or live-system
A micro-USB cable
Something conductive (paperclip, tweezers etc)
Something to open the stick.

Install python3, PySerial, adb and fastboot. For Debian/Ubuntu something like this should work:
Code:
sudo apt update
sudo apt install python3 python3-serial android-tools-adb android-tools-fastboot
Make sure ModemManager is disabled or uninstalled:
Code:
sudo systemctl stop ModemManager
sudo systemctl disable ModemManager

NOTE: If you have issues running the scripts, you might have to run them using sudo.
Also try using different USB-ports (preferably USB-2.0-ports)

1. Extract the attached zip-file "amonet-tank-v1.0.zip" and open a terminal in that directory.
2. start the script:
Code:
./bootrom-step.sh
It should now say Waiting for bootrom.

Short CLK to GND (The metal shielding is also GND) according to the attached photo and plug it in.


NOTE:

In lsusb the boot-rom shows up as:
Code:
Bus 002 Device 013: ID 0e8d:0003 MediaTek Inc. MT6227 phone
If it shows up as:
Code:
Bus 002 Device 014: ID 0e8d:2000 MediaTek Inc. MT65xx Preloader
instead, you are in preloader-mode, try again.

dmesg lists the correct device as:
Code:
[ 6383.962057] usb 2-2: New USB device found, idVendor=0e8d, idProduct=0003, bcdDevice= 1.00

4. When the script asks you to remove the short, remove the short and press enter.

5. Wait for the script to finish.
If it stalls at some point, stop it and restart the process from step 2.

6. Your device should now reboot into unlocked fastboot state.

7. Run
Code:
./fastboot-step.sh
8. Wait for the device to reboot into TWRP.

9. Use TWRP to flash custom ROM, Magisk or SuperSU


NOTE:
Only ever flash boot/recovery images using TWRP, if you use FlashFire or other methods that are not aware of the exploit,
your device will likely not boot anymore (unless you flashed a signed image).
TWRP will patch recovery/boot-images on the fly.

NOTE:
This process does not disable OTA or does any other modifications to your system.
You will have to do that according to the other guides in this forum.


Very special thanks to @xyz` for making all this possible and putting up with the countless questions I have asked, helping me finish this.
Thanks to @hwmod for doing initial investigations and providing the attached image.
