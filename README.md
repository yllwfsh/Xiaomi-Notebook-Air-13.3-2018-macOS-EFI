# EFI Folder for 2018 Xiaomi Notebook Air 13.3" laptops
### Compatibility:
* macOS 10.13 High Sierra
* macOS 10.14 Mojave
* Xiaomi Notebook Air 2018 13.3" i5/i7

### How to use
* Create your macOS USB install media (e.g. https://support.apple.com/en-us/HT201372)
* Install Clover bootloader on USB stick. Select 'Install to ESP' (https://sourceforge.net/projects/cloverefiboot/files/latest/download)
* Mount the ESP (EFI System Partition) on your USB stick: (check that you mount the correct EFI partition, numbers will vary!!!)

```
diskutil list
sudo diskutil mount /dev/disk3s1
```
* Copy and overwrite the EFI/CLOVER folder from this website to the EFI folder on the ESP.
* Now boot the Xiaomi laptop from the install media
* Open Disk Utility and format the builtin SSD with APFS (will delete all your files!!!)
* Install macOS
* After install, boot from USB again but select SSD to boot from in Clover Bootloader
* Do initial macOS setup (use USB ethernet adapter for internet)
* Install Clover on the SSD. Select 'Install to ESP' (https://sourceforge.net/projects/cloverefiboot/files/latest/download)
* Mount the ESP (EFI System Partition) on your SSD (check that you mount the correct EFI partition, numbers will vary!!!)

```
diskutil list
sudo diskutil mount /dev/disk0s1
```
* Copy and overwrite the EFI/CLOVER folder from this website to the EFI folder on the ESP.
* Copy all the Kernel Extensions (kexts) in the PostInstall/Library/Extensions to your system's /Library/Extensions folder (this is important, otherwise keyboard/trackpad and display brightness control don't work)
* Execute these commands to rebuild Kernel Extension Cache:

```
sudo chmod -R 755 /System/Library/Extensions/
sudo chown -R root:wheel /System/Library/Extensions/
sudo chmod -R 755 /Library/Extensions/
sudo chown -R root:wheel /Library/Extensions/
sudo touch /System/Library/Extensions/
sudo touch /Library/Extensions/
sudo kextcache -i / && sudo kextcache -u /
```
* Done!

### Audio Problems
If you're having audio problems, especially with headphones, run the install.command script inside the ALCPlugFix folder. This will install a fix, then reboot. Audio should be better.

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
* FileVault File encryption (alway make a backup before switching it on!!!)

Not working:
* Wifi & Bluetooth (because Intel cards not supported under macOS)
* Nvidia GPU (Not supported under macOS)

### Feedback
Please give me feedback or send a pull request if you find some improvements to be made!

### Disclaimer!
Use these files and this howto at your own risk. I'm not responsible in any way for lost data, damage to software or hardware or anything else that might go wrong. This works for me but might not for you.
