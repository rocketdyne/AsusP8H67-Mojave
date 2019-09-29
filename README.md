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

## BIOS settings

- Version: 3703;
 
 All default parameters except:
 
 - Advanced\Configuration\SATAModeSelection: AHCI;
 - Advanced\OnboardDevicesConfiguration\SerialPortConfiguration\SerialPort: Disabled;
 - Advanced\SystemAgentConfiguration\GraphicsConfiguration\PrimaryDisplay: PCIE.
 
