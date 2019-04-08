# EFI Folder for 2018 Xiaomi Notebook Air 13.3" laptops
### Compatibility:
* macOS 10.13 High Sierra
* macOS 10.14 Mojave
* Xiaomi Notebook Air 2018 13.3" i5/i7

### How to use
* Create your macOS USB install media (e.g. https://support.apple.com/en-us/HT201372)
* Mount the ESD (EFI System Partition) on your USB stick: (check that you mount the correct EFI partition, numbers will vary!!!)

```
diskutil list
sudo diskutil mount /dev/disk3s1
```
* Copy the EFI/CLOVER folder to the EFI folder on the ESD.
* Now boot the Xiaomi laptop from the install media
* Open Disk Utility and format the builtin SSD with APFS (will delete all your files!!!)
* Install macOS
* After install, boot from USB again but select SSD to boot from in Clover Bootloader
* Do initial macOS setup (use USB ethernet adapter for internet)
* Copy all the Kernel Extensions (kexts) in the PostInstall/Library/Extensions to your system's /Library/Extensions folder
* Execute these commands to rebuild Kernel Extension Cache:

```
sudo chown -R root:wheel /Library/Extensions/*
sudo chmod -R 755 /System/Library/Extensions/*
sudo kextcache -i / && sudo kextcache -u /
```
* Done!

### What works and what doesn't?
Working:
* CPU Power Management
* Sleep
* Builtin Intel GPU Acceleration
* Audio
* NVMe / SATA SSD's
* USB A/C ports
* Battery Management
* HDMI / Displayport(USB-C)
* Keyboard
* Trackpad (with near-perfect gesture emulation)
* Webcam
* Display brightness (remap keyboard shortcuts for it in System Preferences)

Not working:
* Wifi & Bluetooth (because Intel cards not supported under macOS)

### Feedback
Please give me feedback using the Issues tab if you find some improvements to be made!

### Disclaimer!
Use these files and this howto at your own risk. I'm not responsible in any way for lost data, damage to software or hardware or anything else that might go wrong. This works for me but might not for you.