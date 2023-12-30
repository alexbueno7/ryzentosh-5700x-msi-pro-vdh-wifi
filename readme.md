<p></p>
<p align="center"><img src="https://i.imgur.com/HJnpvwQ.png" width="200" height="48"/> EFI</p>
<p align="center">
 <a href="https://www.apple.com/macos">
  <img src="https://img.shields.io/badge/Sonoma-14.2.1-informational.svg">
 </a>
 <a href="https://github.com/acidanthera/OpenCorePkg">
  <img src="https://img.shields.io/badge/OpenCore-0.9.7-informational.svg">
 </a>
 <a href="https://github.com/haxgun/Ryzentosh/blob/main/LICENSE">
  <img src="https://img.shields.io/github/license/haxgun/Ryzentosh">
 </a>
</p>
<br>

<h2></h2>

> **Warning**
>
> Use at your own risk. I built this EFI for myself and it does not guarantee 100% work with your hardware.
>
> MLB, ROM, Serial Number, SystemUUID sections are specifically left empty. Use GenSMBIOS to generate SMBios.
>

## Overview
Hi, this is the EFI file that is currently (mostly) working for me on *the current version of macOS Sonoma, wich is macOS 14.2.1, released on December 19.*. This is the version i am using with this EFI with Opencore version: 0.9.7.

After several studies, adjustments and tests with EFIs that somehow led me to building my own EFI and my first hackintosh, I am publishing it here so that I can somehow help someone with similar hardware, sharing what worked for me.

I would recommend you doing your own research and building your EFI by yourself according to the Dortania guide. When you're done and it does not work, come back compare it with mine see check for differences and issues i had.

<h2 align="center">📺 Build</h2>

| **Component** | **Model**                                                     |
| ------------- |---------------------------------------------------------------|
| CPU           | AMD Ryzen 5 5700X                                             |
| Motherboard   | MSI B550 PRO-VDH-WIFI                                         |
| GPU           | Asrock RX6600 Challenger 8GB                                  |
| RAM           | JUHOR DDR4 4x16GB @ 3400 MHz                                  |
| OS disk       | Kingston KC3000 M.2 2280 PCIe 4.0 1TB                         |
| Other disk    | KINGSTON M.2 2280 NV2 1TB,                                    |
| Other disk    | WD Blue 1 TB                                                  |
| macOS         | Sonoma 14.2.1, released on December 19                        |
| OpenCore      | 0.9.7 Release                                                 |

<h2 align="center">🔧 BIOS</h2>

<details>
    <summary><b>🔌 Settings</b></summary>

| **Component**                  | **Model**                                    |
|--------------------------------|----------------------------------------------|
| Fast boot                      | Enabled                                      |
| SVM Mode                       | Disabled                                     |
| Above 4G Decoding              | Enabled                                      |
| Resizable BAR                  | Disabled                                     |
| XHCI Hand-off                  | Enabled                                      |
| Boot Mode                      | UEFI                                         |
| Secure Boot                    | Enabled                                      |

<h2 align="center">🩼 Functional</h2>

## What works and what doesn't?
### Working
- iServices:
    - Facetime
    - Messages
    - Find my
    - iCloud
    - Store
- CPU Power management, Fan control
- Audio over USB headset / P2
- Mic
- Developer Tools / Xcode
- Sleep

### Not working
- Airdrop, Handoff (Wifi and Bluetooth): if you really need Wifi or Bluetooth buy one of the PCI-E cards mentioned on the [wireless buyer's guide](https://dortania.github.io/Wireless-Buyers-Guide/types-of-wireless-card/pcie.html) or adjust your EFI to use dongles. The Wifi/Bluetooth native from MB don't work with MacOs.
- Discord only works in browser as the desktop version uses some libraries that only work on Intel (at least thats what i understood). Read more about this issue and how to fix it [here](https://www.macos86.it/topic/5489-tutorial-for-patching-binaries-for-amd-hackintosh-compatibility/)

## Gathering EFI Files

### Kexts
Now this is the fun part. 

### For 5700X, RX6600
- [Lilu.kext](https://github.com/acidanthera/Lilu/releases)
- [VirtualSMC.kext](https://github.com/acidanthera/VirtualSMC/releases)
- [SMCAMDProcessor](https://github.com/trulyspinach/SMCAMDProcessor)
- [AMDRyzenCPUPowerManagement.kext](https://github.com/trulyspinach/SMCAMDProcessor/releases) For [AMD Power Gadget](https://github.com/trulyspinach/SMCAMDProcessor).
- [AppleMCEReporterDisable.kext](https://github.com/acidanthera/bugtracker/files/3703498/AppleMCEReporterDisabler.kext.zip)
- [RadeonSensor.kext](https://github.com/aluveitie/RadeonSensor)
- [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)
- [VirtualSMC.kext](https://github.com/acidanthera/VirtualSMC/releases)

### For MSI B550 PRO-VDH-WIFI:
- [USBToolBox.kext](https://github.com/USBToolBox/kext)
- Make sure that if you use the USBToolBox.kext above, you also map your USBs using [USBToolBox Tool](https://github.com/USBToolBox/tool)
- [RealtekRTL8111.kext](https://github.com/Mieze/RTL8111_driver_for_OS_X/releases)

### Others
- [NVMeFix](https://github.com/acidanthera/NVMeFix/releases)|Used for fixing power management and initialization on non-Apple NVMe.
[RestrictEvents](https://github.com/acidanthera/RestrictEvents/releases)|Better experience with unsupported processors like AMD, Disable MacPro7,1 memory warnings and provide upgrade to macOS Monterey via Software Updates when available.

# ACPI Tables - AMD
DSDT
SSDT-CPUR
SSDT-EC
SSDT-GPRW
SSD-HPET
SSDT-SBUS-MCHC
SSDT-EC-USBX

<h2 align="center">🔧 Tools</h2>

1. [Hackintool](https://github.com/benbaker76/Hackintool)
2. [OpenCore Configurator](https://mackie100projects.altervista.org/download-opencore-configurator/)
3. [CPU Name](https://github.com/corpnewt/CPU-Name)
4. [About This Hack](https://github.com/0xCUB3/About-This-Hack)

This should be all you need.

<h2 align="center">💡 Tips and alerts!</h2>
Update **config.plist** in PlatformInfo > Generic with YOUR informations
Please use [*genSMBIOS*](https://github.com/corpnewt/GenSMBIOS/archive/refs/heads/master.zip) for generate values for above itens.
<br>
Please use [*ProperTree*](https://github.com/corpnewt/ProperTree/archive/refs/heads/master.zip) for configure/edit your config.plist.

## Issues
### iServices not working?
Take a look at [this part of the guide](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#fixing-en0).