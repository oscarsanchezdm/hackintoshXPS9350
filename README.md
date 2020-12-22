# macOS on Dell XPS 9350
OpenCore EFI folder for Dell XPS 9350 laptop.

**Current bootloader version**
OpenCore 0.6.4 Release

Tested on **Dell XPS 9350**
  - 3K touch display
  - i7-6560U / Intel Iris HD 540
  - 8GB RAM
  - Sabrent M.2 Drive (replaced Samsung PM951 due to lack of power management)
  - DW1820A wireless card
  - macOS Big Sur 11.1

### What does work
- CPU/NVME Power Management
  - On idle, the CPU will run at 0.4GHz
- Audio
- Sleep
- Hibernation
- WiFi
- Bluetooth
- I2C trackpad (with multitouch gesture support)
- I2C touchscreen (with multitouch gesture support)
- Brightness control using keys
- IGPU with Hardware Acceleration
- SideCar
- Boot Chime

### What does not work
- **SD card reader** (disable it on BIOS to save energy)
- **USB-C hot-plug** Unplugging an USB-C device when macOS is running may cause Kernel Panics when sleeping
- **Camera** does not work in Big Sur. The image will stop working in ~30 seconds, then it will turn black until the next wake. It used to work in macOS Catalina.
- DRM (broken in IGPU-only laptops)

### Current issues
- Power management on WiFI card DW1820A (will cause an extra +0.7/+1.2W power consumption)
- OpenCanopy menu won't launch pressing ALT key (if ShowPicker is enabled, it will work)
- Audio may stop working randomly. When this happens, use the microphone in any app and the speaker will work again
- macOS will not auto-hibernate on low battery. You should shutdown the computer manually.

### Preparation
**Format the disk using 4K sector size**
Use the [followig guide](https://www.tonymacx86.com/threads/guide-sierra-on-hp-spectre-x360-native-kaby-lake-support.228302/). Make sure you have a compatible drive.

If you have issues with Alt/Windows swapped keys, enable SSDT-PS2K.aml under config.plist > ACPI > Add

### How to install
Clone this repository and copy the EFI folder inside your EFI partition. You will need to use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to generate serial and UUID. You should use MacBookPro13,1 as SMBIOS.

Once macOS is installed, install [ComboJack](https://github.com/hackintosh-stuff/ComboJack) (only the script, the kext is present inside the EFI folder) to get headphone port working.

To get OpenCanopy and Boot Chime working, download the Resources folder from [here](https://github.com/acidanthera/OcBinaryData)

### Credits
- [Dortania](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/skylake.html)
- [acidanthera](https://github.com/acidanthera/) for OpenCore, Lilu, WhateverGreen... and all the contributors
- ddegrasse for [guide for formatting disk to 4K sector size](https://www.tonymacx86.com/threads/guide-sierra-on-hp-spectre-x360-native-kaby-lake-support.228302/)
- [corpnewt](https://github.com/corpnewt/) for [CPUFriendFriend](https://github.com/corpnewt/CPUFriendFriend)
- [maz-1](https://github.com/maz-1) for [ComboJack](https://github.com/hackintosh-stuff/ComboJack)
- [syscl](https;//github.com/syscl) for [XPS 9350 macos guide](https://github.com/syscl/XPS9350-macOS)
- [hieplpvip](https://github.com/hieplpvip/) for  [SidecarEnabler](https://github.com/hieplpvip/SidecarEnabler)
- Apple for macOS
