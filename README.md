# AsusP8H67-Mojave
The steps that I followed to install Mac OS Mojave on Asus P8H67-M EVO

## **_CURRENTLY UNDER DEVELOPMENT_**


## Hardware setup
Asus P8H67-M EVO, i5 2500K, 7200rpm Hard Drive, MSI Armor RX 570 4GB, USB mouse/keyboard. No Wi-Fi (onboard Ethernet is used).

## Tools
- A working Mac OS environment;
- 2x USB sticks, one with at least 8GB of memory.

## Known issues & info
- No HDMI output (seems a common problem with AMD GPUs, use DisplayPort instead);
- USB 3.0 ports not working;
- slow speeds on USB 2.0 (under investigation...).

- Apple has dropped support for Sandy Bridge CPUs starting from Mojave (the iGPU doesn't support Metal API), then a supported GPU is needed;
- Mac OS will be installed in a dedicated Hard Drive (no dual boots etc.) that will be completely wiped;
- this is not meant to be an hackintosh guide, it's made just for fun.

## 0. BIOS settings

- Version: 3703;
 
 All default parameters except:
 
 - Advanced\Configuration\SATAModeSelection: AHCI;
 - Advanced\OnboardDevicesConfiguration\SerialPortConfiguration\SerialPort: Disabled;
 - Advanced\SystemAgentConfiguration\GraphicsConfiguration\PrimaryDisplay: PCIE.
 
## 1. Download Mac OS Mojave

Download Mac Os Mojave from the App Store and [create a Mac OS install disk](https://support.apple.com/hr-hr/HT201372) using the >= 8GB USB Drive.

## 2. Install Clover on USB Drive

[Download Clover bootloader](https://sourceforge.net/projects/cloverefiboot/) on your Mac. Insert the other USB Drive and format it in Disk Utility with "Mac Os Extended with GUID".
Open the CLover .pkg, select Continue on the Introduction and Read Me tab. In the Destination Select tab select Change Install Location and select the USB Drive that has been just formatted. In the Installation Type tab select Customize and select Clover for UEFI booting only, Install Clover in the ESP. Select Recommended drivers and Human Interface Devices. In Filesystem Drivers, select ApfsDriveLoader and VboxHfs. In Memory Fix drivers select only OsxAptioFix3Drv. Finally, click on Install.
After installation, the USB EFI partition (EFI) should be automatically mounted on you Mac.

## 3. Configure the EFI

Download the following kexts and copy them (Release version) to EFI/CLOVER/kexts/Other:
- [AppleALC](https://github.com/acidanthera/applealc/releases)
- [WhateverGreen](https://github.com/acidanthera/WhateverGreen/releases)
- [Lilu](https://github.com/acidanthera/lilu/releases)
- [VirtualSMC](https://github.com/acidanthera/VirtualSMC/releases) together with SMCProcessor and SMCSuperIO
- [RealtekRTL8111](https://github.com/Mieze/RTL8111_driver_for_OS_X)

Copy the config.plist file attached in this repository on EFI/COLVER

Download [Clover Configurator](https://mackie100projects.altervista.org/download-clover-configurator/)
Open the config.plist with Clover Configurator, in the SMBIOS tab set iMac 17.1 with the two arrows button on the right and save (CMD+S or File/Save in the top menu).

## 4. Install Mac OS

Connect the Target Hard Drive on which Mojave will be installed and the two USB Drives to the Asus computer. Press F8 on startup and select the USB (UEFI) on which Clover bootloader has been installed. Launch the installation from the Mojave USB Drive, format the target Hard Drive with Disk Utility and start the Mojave Installer. During the installation process the computer will be restarted a couple of times: be sure to boot with the Clover USB and select the Target Hard Drive every time. If you have errors similar to  “error loading kernel cache (0x9)” just reboot.

## 5. Post installation

- In order to boot without the need of Clover USB Drive, repeat steps 3 and 4 using the Target Hard Drive on which Mojave has been installed as target. After completing these steps, the Mojave Hard Drive can also be set as primary boot device in BIOS settings.

-[Disable hibernation](https://osxlatitude.com/forums/topic/9966-how-do-i-disable-hibernation-for-sleep/
)
- Disable "wake for network access" and "put hard disk to sleep when possbile" in Preferences/EnergySaver

- If you incur in instant wakes after sleep (but also if you don't) I suggest to patch DSDT using [this guide](https://www.tonymacx86.com/threads/guide-patching-laptop-dsdt-ssdts.152573/).
I have applied the following common suggested patches:
 - "Fix WAK Arg0 v2"
 - "HPET Fix"
 - "SMBUS Fix"
 - "IRQ Fix"
 - "RTC Fix"
 - "OS Check Fix" (Win7)
 - "6-Series USB"
 - "Fix Mutex with non-zero SyncLevel"
 - "Add IMEI"
 - "USB3_PRW 0X0D" (this in particular resolves istant wake problem)

- If you plan to use your Apple ID with this machine, I suggest to follow [this guide](https://www.tonymacx86.com/threads/an-idiots-guide-to-imessage.196827/) (at least!).


