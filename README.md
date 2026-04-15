# vivobook-x1407qa-linux
<sub>Patches and Devicetree changes to make GNU/Linux excellent on this affordable model!</sub>
<sup>Once completed (100%), I plan to push to mainline changes</sup>
--
Currently using a Vivobook s15 device tree, working on a custom one to fix USB support!
## Feature Matrix

* WIP - Something I am already working on
* TBH - Something I could work on, but not started / no sufficient progress was made
* QC  - Something I cannot work on, depends on Qualcomm's upstream support

| Feature                 | Status | Notes                                                                                                        |
| ----------------------- | -----: | ------------------------------------------------------------------------------------------------------------ |
| Battery Charging        |     ✅ |                                                                                                              |
| Battery Info            |     ✅ | Requires firmware extract                                                                                    |
| Bluetooth               |     ✅ |                                                                                                              |
| Iris/HW decoder         |    TBH | Will not work, due to this being a Purwa device                                                              |
| Camera                  |    TBH | Will NOT work, due to this being a Purwa device                                                              |
| Display                 |     ✅ | FHD OLED and LCD on UX3407QA, 3K OLED on UX3407RA                                                            |
| GPU Acceleration        |     ✅ | Requires firmware extract                                                                                    |
| Keyboard                |     ✅ |                                                                                                              |
| Microphone              |     ✅ |                                                                                                              |
| NVMe                    |     ✅ |                                                                                                              |
| Speakers                |     ✅ | ~Requires userland configuration, see below.~ Works with latest upstream alsa-ucm-config, linux-firmware     |
| Audio Jack              |     ✅ |                                                                                                              |
| Suspend                 |    WIP | Suspends tolerably, lid switch working, but fan stays on. Power drop in sleep isn't best, nothing I can fix. |
| Touchpad                |     ✅ |                                                                                                              |
| TPM                     |     ❌ | Firmware TPM                                                                                                 |
| USB-A 3.0               |    WIP | Requires devicetree work for hotplug to function (coldplugs fine)                                            |
| USB-C 3.0               |    WIP | Requires devicetree work for hotplug to function (coldplugs fine)                                            |
| USB-C Booting           |     ✅ |                                                                                                              |
| USB-C DP Alt Mode       |    WIP |                                                                                                              |
| USB-C DP over dock      |    WIP |                                                                                                              |
| HDMI                    |    WIP |                                                                                                              |
| Wi-Fi                   |     ✅ | Requires firmware extraction and patching.                                                                   |
| EC                      |     ❌ | Similar to out-of-tree EC driver for Lenovo Slim 7x.                                                         |

## Notes
<sub>Currently working on Ubuntu 26.04 BETA*</sub>
<sup>*With Kernel 6.19 for some reason...</sup>
--

#### Setup Guide
<sub>READ THOROUGHLY, AND MAKE AN ASUS RECOVERY USB! I AM NOT RESPONSIBLE IF YOU MAKE A MISTAKE AND BRICK YOUR LAPTOP!</sub>
--

### Requirements
<sub>You MUST HAVE ALL OF THEM TO PROCEED</sub>
--

## MAKE SURE YOU HAVE AN X1407QA, Check the bottom label! It MUST SAY x1407q for this to work!

--

--

 *Asus x1407QA (Snapdragon X) running Windows (With the ORIGINAL ASUS IMAGE AND ALL PREINSTALLED DRIVERS)
 *Usb Drive (min. 16+GB) For the Ubuntu Install AS WELL AS A BACKUP OF THE DRIVER STORE!
 *ANOTHER Usb Drive (Preferably 32+GB, BUT as little as a 2GB has a chance to work) For the ASUS Recovery Media
 *ALL DATA ON THE VIVOBOOK BACKED UP IF YOU WANT TO KEEP IT
 *DECENT KNOWLEDGE OF LINUX AND TROUBLESHOOTING, OR INHUMAN AMOUNTS OF STACKEXCHANGE READING
 *Usb-Ethernet Adapter OR An Android phone and USB Tethering cable
--

### Initial Install

--

## Step 1
# Make Recovery Media!
 Double check that you have the right model, THEN you can download the recovery imager from ASUS at https://www.asus.com/us/laptops/for-home/vivobook/asus-vivobook-14-x1407q/helpdesk_knowledge?model2Name=X1407QA
 Use the tool in Windows to make a recovery image (Selecting your USB Drive)
 *The tool can be a bit iffy... Sometimes you have to make a win10 USB or OTHER fat32 BOOTABLE USB and delete all the files... for some reason...
 *YOU CAN MAKE THE IMAGE FROM ANY WINDOWS 10/11 64-BIT DEVICE, INTEL OR ARM!
 
## Step 2
# Download stuff!
 Download the Resolute ISO from the comment on Ubuntu Discourse:
 https://discourse.ubuntu.com/t/looking-for-support-on-installing-ubuntu-on-snapdragon-x/74615/13
 (I didn't find any modifications other than forcing a device tree, BUT if you're paranoid, just copy the x1p42100-vivobook-s15 devicetree to a stock resolute ISO and force it using the argument below AT THE BOTTOM LINE of the Grub boot editor)
``` 
 devicetree XXXXXXX.dtb 
```
 Download the modified qcom-firmware-extract script.
 
## Step 3
# Make Ubuntu USB
 NOTE: You MUST BE ABLE TO ACCESS THE USB FROM WINDOWS OR HAVE A WAY TO OTHERWISE GET FILES TO IT!
 Preferably use Rufus in FileCopy mode to image it, as you DO NEED TO DO SOME MODIFYING!
 (https://rufus.ie)
 
## Step 4
# Update your Vivobook's Windows Install
 This is so you get up to date firmware and drivers!

## Step 5
# BACKUP THE DRIVER STORE!!!!!!!!!
 Make a folder on the root of the USB (Ubuntu), and copy the ENTIRE C:/Windows/System32/DriverStore/FileRepository folder to it
 THIS WILL BE CRITICAL IF YOU CHOOSE TO WIPE THE WINDOWS PARTITION (Recommended)!!!!!

## Step 6
# BIOS CHANGES
 Enter the boot menu by holding ESC as the Vivobook powers on!
 Choose BIOS Setup, and enter the Security tab.
 Disable Secure Boot, and enter the Boot tab.
 Disable Fast Boot, and save and exit (Press F10)

## Step 7
# BOOT The USB
 Turn OFF the vivobook, plug in the USB (Ubuntu), and then turn it back on. Avoid having both the Ubuntu and the Recovery USB plugged in simultaneously!
 Enter the boot (again) menu by holding ESC as the Vivobook powers on!
 Choose the USB boot option.
 Select the closest option to "Asus Vivobook S15 (x1p42100) Install"
 Wait for it to boot.

## Step 8
# Install Ubuntu (and make it bootable!)
 Run the installer OFFLINE! 
 Follow the steps, but DO NOT REBOOT when finished!
 COPY THE x1p42100-vivobook-s15.dtb DEVICETREE TO /target/boot/ (May need to use sudo) 
 (TEMPORARILY) Edit /target/boot/grub/grub.cfg, adding this line at the END of the default boot option (after initrd), and replace /boot/your_devicetree.dtb with the exact name and path you copied the dtb to (i.e /boot/x1p42100-asus-vivobook-s15.dtb)
```
 devicetree /boot/your_devicetree.dtb
```
 Reboot (and PRAY it works)

## Step 9
# Driver Installation and Final Steps!
 EDIT QCOM-FIRMWARE-EXTRACT (The version in this repo) to change this 
```
if [ -z "$part" ]; then
	search_path="/home/${USER}/Documents/repo"
	#IF You delete Windows, BACKUP the "FileRepository" out of Windows/System32/DriverStore, and put its path in the line above this comment! This is a TEMPORARY FIX!!!!!!!
fi
```
 to this
```
if [ -z "$part" ]; then
	search_path="/path/to/FileRepository/Backup"
	#IF You delete Windows, BACKUP the "FileRepository" out of Windows/System32/DriverStore, and put its path in the line above this comment! This is a TEMPORARY FIX!!!!!!!
fi
```
 (Not needed if you managed to keep Windows installed)
 (Working on making it "just work"(tm)
 Run the Qcom-Firmware-Extract script (with the USB mounted and correct paths edited in OR the windows partition present)...
```
    sudo cp /lib/firmware/qcom/x1e80100/*.jsn /lib/firmware/qcom/x1p42100/
    sudo ln -sf /usr/lib/firmware/qcom/x1e80100/gen70500_sqe.fw /lib/firmware/qcom/gen70500_sqe.fw
    sudo ln -sf /usr/lib/firmware/qcom/x1e80100/gen70500_gmu.bin /lib/firmware/qcom/gen70500_gmu.bin
    sudo ln -sf /usr/lib/firmware/qcom/x1p42100/gen70500_zap.mbn.zst /lib/firmware/qcom/gen70500_zap.mbn
    sudo update-initramfs -u -k all
```
 ADD the devicetree to /etc/default/grub (so changes persist)
 Update grub
 Update Ubuntu (apt full-upgrade)
 (IF you have issues booting, try using the 6.19 kernel in the default boot option)
 Follow the guide at https://github.com/alexVinarskis/linux-x1e80100-zenbook-a14 for wi-fi and audio!
 Update initramfs (again)
 Reboot and it SHOULD work!
--

--

# Credits
 https://github.com/alexVinarskis/linux-x1e80100-zenbook-a14 
<small>Feature Matrix Template, Initial Inspiration, Contains 90% of the work to make this model work.</small>
 https://github.com/aarch64-laptops
<small>Made the MAJORITY of the devicetree</small>
https://discourse.ubuntu.com/t/looking-for-support-on-installing-ubuntu-on-snapdragon-x/74615/13
<small>This guy made an ISO that I was able to get booting for initial setup!</small>
## Temporary command dump lol


