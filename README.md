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
- Display
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

