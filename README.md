# Lenovo Ideapad 330s-14IKB Hackintosh
Full guide to create a Lenovo Ideapad 330s-14ikb Hackintosh

### Feel free to help a broke student out at the bottom of the page. :)

#### Read this guide in...
[English](README.md) | [Deutsch](README-DE.md)

***DISCLAIMER***
The project is still in its beta/testing state.
Proceed at your own risk, I shall not take responsibility for any damages caused.

## My Ideapads's Hardware Configuration:
- CPU: i3-8130U @ 2.21GHz
- 4GB RAM
- Intel UHD 620
- Display: HD 1366 x 768
- 128 GB SSD
- WiFi and Bluetooth card: Lenovo Branded Broadcom BCM94352Z

## Issues
- Sometimes sleep doesn't work while closing the lid. (Very Random)
- Keyboard mute shortcut. (Displays muted but doesn't actually mute)
- iMessage and Facetime. (I tried, but didn't get it to work)
- Trackpad gestures not quite working. Maybe I'll find a fix for that.
- One ACPI Error while booting. Can be ignored. (Hoping someone can help me with this) | Disable verbose (-v) mode to just hide it...

## Let's Get Started

### What you need:
- Lenovo Ideapad 330s-14IKB (i3 or i5 Model)
- macOS or OS X downloaded from the Mac App Store
- 8GB USB stick
- Keyboard, Mouse and a USB Hub (That stuff works after install)

### BIOS Settings
- Upgrade to the latest BIOS.
- If yours came with Intel Optane, you need to disable that and use AHCI Legacy mode (Not RST).
- Disable secure boot and unload optimized defaults for windows 10.
- Disable Virtualization

## 1. Make Install USB (You will need a mac for this | Don't have a Mac? [Look at this tutorial](MacVM.md))
First, connect your 8GB (or more) USB drive to your mac.

Open Diskutil and format it to Mac OS Journaled and name it "install_osx"

Download macOS Mojave from the Mac App Store, after the download process has finished, create the USB installer by opening terminal and writing the following command:

``` sudo "/Applications/Install macOS Mojave.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --nointeraction ```

Thats it for part 1!

## 2. Installing Clover
Download the latest version of clover bootloader from [here](https://sourceforge.net/projects/cloverefiboot/).<br>
Open Clover bootloader installer, click on continue, agree, continue and when you reach the screen "Installtion Type", click on "Change Install Location".<br>
Choose your USB disk which should be labelled as "install_osx" as the install location.<br>
Next click on "Customize". Make sure the following options are selected:<br>
- Clover for UEFI booting only
- Install Clover in the ESP
- Themes
- UEFI Drivers (Under Drivers, uncheck SMCHelper-64, as we will be using VirtualSMC)
**Click Install**

## 3. Copying relevant drivers and kext files (Go to Releases to get the kexts etc)
Copy the files from the "drivers64UEFI" (NvmExpressDxe-64 needed only for NVMe drives) and "kexts" folder to your USB where you have installed clover.<br>
Replace the config.plist with the config.plist from my folder.<br>

## 4. Installation

### Step 1:
Plugin your USB, Power on your laptop, after the laptop screen turns on, press F1 repeatedly to enter into the BIOS.<br>
Change the boot order to set the USB as the first boot device. Save and exit the BIOS.<br>
Now it should bring you into the Clover Bootloader menu, select Install macOS Mojave (USB Drive) and press enter.<br>
The Installer now should boot and reach installation menu.<br>

### Step 2:
From the installation menu, open Disk Utility, select the partition that you plan to install macOS, format it as Mac OS Journaled and name for the purpose of this guide we will name it "macOS". Exit Disk Utility after the format process has finished, this will bring you back to the Installer Main Menu. <br>
Now select install macOS Mojave, agree to the "terms and conditions", select your HDD/SSD that you formatted and the installation process will begin. this will be the part 1 install. Part 1 should take around 5 minutes. <br>

### Step 3:
Laptop will automatically reboot when Part 1 installation ends. now as soon as Clover Bootloader menu shows up, this time you select the "macOS" partition to boot from, the installer will continue with Part 2 now and show the progress bar with time remaining under the Apple boot logo. <br>
Note: Sometimes as soon as the time remaining shows up under the Apple boot logo, the laptop will reboot once more, if this happens, choose to boot from the "macOS" partition and Part 2 installation will continue and complete. <br>
After the installation has been completed, laptop will reboot and bring you to the Part 3 - first boot user setup.<br>

### Step 4:
Select Language, Continue, Connecting to Internet is optional or you can skip it for now.<br>
When you reach the menu to sign with your Apple ID, make sure to skip this step, it will be important if you want to setup iMessage & FaceTime.<br>

## 5. Post Installation
### Step 1: 
Open terminal and enter the following command:

``` sudo spctl --master-disable ```

This allows you to install Applications downloaded from Internet / Outside of the Mac App Store.

### Step 2:
Open Clover Bootloader installer and continue with bootloader installation into the HDD/SSD that we installed macOS.<br>
The procedures are exactly the same as on the Creating USB Installer, except that this time, instead of the USB Drive, we select the "macOS" HDD/SSD that we installed macOS. Also copy drivers from the "drivers64UEFI" folder to the "drivers64UEFI" folder on the Hard drive.<br>

### Step 3:

Now we need to install all the needed kexts into the HDD/SSD where we installed macOS. <br>
All kexts should be installed into /Library/Extensions. Easiest way to Install kexts is with HackinTool. [Guide](https://www.tonymacx86.com/threads/guide-installing-3rd-party-kexts-el-capitan-sierra-high-sierra-mojave.268964/). Install all the kexts from the Library/Extensions folder I have attached. <br>
Remove AppleIntelLpssI2C.kext and AppleIntelLpssI2CController.kext from /System/Library/Extentions or disable them with clover configurator (rebuild cache with hackintool) <br>
Remove all kexts except for Lilu,VirtualSMC and WhateverGreen from your \EFI\CLOVER\kexts\Other <br>
Reboot and press F4 and Fn+F4 at the bootloader. (This will generate you DSDT and SSDT files) <br>
Boot into the system and copy the DSDT and SSDT-PNLF from my Clover folder to EFI\CLOVER\ACPI\patched. (You should ideally create these on your own, but mine should work fine.) <br>

That's it! Ideally if you have the same config you should be done, but I would always recommend the Vanilla way and fix issues one by one. (I have made simple Guides for this attached in my folder).

### Step 4:
Use Hackintool to fix hibernation and for USB port patching. (Guides in the folder)

## Credits:
- Thanks to [RehabMan](https://www.tonymacx86.com/members/429483/) for his guides.
- Thanks to [muchmore](https://www.tonymacx86.com/members/698774/) for his battery patch and [Whab](https://www.tonymacx86.com/members/2096263/) for some suggestions in the 15IKB thread on tonymacx86.
- Thanks to [Sniki](https://www.tonymacx86.com/members/1501160/) for his V330 guide.

## Changelog:
### 23/8/2019: Initial Release
- Updated iMessage info.

### 22/8/2019: Initial Release
- Guide is completed.
- Files have been added.

## Help me out:
- [PayPal](https://www.paypal.com/paypalme2/quiiddev)