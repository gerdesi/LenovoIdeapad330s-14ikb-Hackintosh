# Lenovo Ideapad 330s-14IKB Hackintosh
Full guide to create a fully working Lenovo Ideapad 330s-14ikb Hackintosh

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
- iMessage and Facetime. (Didn't bother as I don't use them)
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

## 1. Make Install USB (You will need a mac for this | Don't have a Mac? [Look at this tutorial](MacVM.md)
First, connect your 8GB (or more) USB drive to your mac.

Open Diskutil and format it to Mac OS Journaled and name it "install_osx"

Download macOS Mojave from the Mac App Store, after the download process has finished, create the USB installer by opening terminal and writing the following command:

``` sudo "/Applications/Install macOS Mojave.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --nointeraction ```

Thats it for part 1!

## 2. Installing Clover
Download the latest version of clover bootloader from here.<br>
Open Clover bootloader installer, click on continue, agree, continue and when you reach the screen "Installtion Type", click on "Change Install Location".<br>
Choose your USB disk which should be labelled as "install_osx" as the install location.<br>
Next click on "Customize". Make surethe following options are selected:<br>
-Clover for UEFI booting only<br>
-Install Clover in the ESP<br>
-Themes<br>
-UEFI Drivers (Under Drivers, uncheck SMCHelper-64, as we will be using VirtualSMC)<br>
**Click Install**

## 3. Copying relevant drivers and kext files (Go to Releases to get the kexts etc)
Copy the files from the "drivers64UEFI" (NvmExpressDxe-64 needed only for NVMe drives) and "kexts" folder to your USB where you have installed clover.<br>
Replace the config.plist with the config.plist from my folder.<br>
