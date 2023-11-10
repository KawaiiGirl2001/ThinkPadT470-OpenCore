# High-quality ready-made OpenCore bootloader for ThinkPad T470. Built for macOS Sonoma. Designed with security and stability in mind.

<p align="center">
<a target="__blank" href="https://www.apple.com/in/macos/ventura/">
  <img src="https://img.shields.io/badge/Compatibility-macOS%20%7C%20Sonoma-yellow.svg?style=flat" />
</p>
  <p align="center">
    <a target="__blank" href="https://developer.apple.com/documentation/macos-release-notes">
  <img src="https://img.shields.io/badge/MacOS-14.X-orange.svg?style=flat" />
    </a>
    <a target="__blank" href="https://github.com/acidanthera/OpenCorePkg">
      <img src="https://img.shields.io/badge/OpenCore-0.9.5-darkblue.svg?style=flat">
    </a>
    <a target="__blank" href="https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-t-series-laptops/thinkpad-t470">
      <img src="https://img.shields.io/badge/Model-20HE-darkcyan?style=flat">
    </a>
    <a target="__blank" href="https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-t-series-laptops/thinkpad-t470">
      <img src="https://img.shields.io/badge/BIOS-1.72-red?style=flat">
    </a>
  </p>

### Description
+ OpenCore bootloader for ThinkPad T470 equipped with an intel wireless module. Stable and suitable for everyday use. The only supported OS version is macOS 14 Sonoma.
+ Unlike most OpenCore builds currently available on GiHub, this configuration fully supports UEFI Secure Boot, Apple Secure Boot model and comes with System Integrity Protection enabled.
### Hardware Support
**What's working?**
+ Dual Battery
+ All function keys
+ Intel Graphics HD 620 with acceleration (Metal 3 Supported)
+ Fan control
+ Power management
+ Wifi
+ Bluetooth
+ HDMI 
+ Apple HD Audio
+ Sleep and wake
+ SD Card slot
+ Type-C charging and video output
  
**What's not working?**
+ Fingerprint reader (Will not work)
+ TouchScreen(Kext for touchscreen is disabled because it breaks sleep on macOS Sonoma, May be fixed in the future)
  
**My hardware conifguration:**
+ ThinkPad T470 20HE with TouchScreen and IR-camera
+ Intel i5-7300U
+ Intel Graphics HD 620
+ Full HD IPS Touchscreen
+ 8Gb RAM
+ 256Gb NVMe SSD
  
***This OpenCore build was tested on this configuration only***
### Installation
**Preparing the OpenCore configuration:**
+ Before starting the installation, you need to personalize the configuration - add to config.plist the generated unique serial numbers to run Apple services and ApECID to provide Apple SecureBoot full security mode. 
+ Use corpnewt's GenSMBIOS utility to create the SMBIOS. You will need to create an SMBIOS for the MacBookPro15,2 model. After creating the SMBIOS, enter data in the fields of the PlatformInfo -> Generic section. 
+ Serial = SystemSerialNumber
+ Board Serial = MLB
+ SmUUID = SystemUUID
+ AppleROM = ROM
+ To generate your own ApECID value, you'll need some form of cryptographically secure random number generator that will output a 64-bit integer. Below is an example of how to do this using Python3:
```
python3 -c 'import secrets; print(secrets.randbits(64))'
```
+ With this unique 64-bit int, you can now enter it under Misc -> ApECID in your config.plist
+ Next, you need to configure the UEFI firmware and include SecureBoot keys for OpenCore in it. 
+ To do this, put UEFI Secure Boot into Setup Mode, run the KeyTool utility from the flash drive and install db.auth, KEK.auth and PK.auth from the "SecureBoot" folder into your UEFI firmware. Detailed instructions on how to use KeyTool can be found [here](https://github.com/profzei/Matebook-X-Pro-2018/wiki/Enable-BIOS-Secure-Boot-with-OpenCore).
+ After customizing the configuration and preparing the UEFI, create a macOS bootable flash drive following the [guide from dortania](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/).
### Post-installation steps
+ Disable hibernation and powernap
```
sudo pmset autopoweroff 0
sudo pmset powernap 0
sudo pmset standby 0
sudo pmset proximitywake 0
sudo pmset tcpkeepalive 0
```
+ Enable HiDpi by using this [beautiful tool](https://github.com/xzhih/one-key-hidpi)
