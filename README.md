# ZOTAC MAGNUS ONE ZBOX‑ECM73070C Hackintosh (macOS Tahoe)

This EFI is based on the original work from:  
https://github.com/farcop/hackintosh  
I updated it to the latest OpenCore, added fixes, and enabled support for macOS Tahoe (macOS 26.1).

![Device](pictures/zotac-magnus-one.jpeg)

## Hardware

Model: ZOTAC MAGNUS ONE ZBOX‑ECM73070C / 53060C

- CPU: Intel Core i7‑10700 (Comet Lake)
- Chipset: Intel H470
- iGPU: Intel UHD 630 (used for macOS)
- dGPU: NVIDIA RTX 3070 (unsupported in macOS)
- Ethernet 1: Killer E3000 2.5G
- Ethernet 2: Realtek RTL8168/8111
- Wi‑Fi / BT: Killer AX1650x (Intel AX200)
- Audio: Realtek ALC269
- RAM: 32GB (2×16GB) Kingston Fury DDR4‑2933
- SSD: Crucial P3 Plus 1TB NVMe

## Software

- Bootloader: OpenCore 1.0.6 (Debug)
- OS: macOS Tahoe 26.1

## What’s NOT working

- Bluetooth (Intel Bluetooth unstable on macOS)

## What IS working

- macOS installation and boot
- Intel UHD 630 with LSPCON patches
- Audio (ALC269)
- Ethernet (both ports)
- USB (mapped with SSDT‑UIAC)
- Intel Wi‑Fi (via itlwm + HeliPort)
- Sleep / Wake
- NVMe SSD
- iServices (iMessage, App Store, etc.)

## Device Layout

![Devices Layout](pictures/magnus-one-bus-anno-w-arrows.png)

## Installation

1. Download the macOS Tahoe installer vanilla image from Olarila:  
   https://olarila.com/topic/6278-olarila-vanilla-images-macos-installer/
2. Flash the image to a USB stick using balenaEtcher:  
   https://etcher.balena.io/
3. Mount the USB’s EFI partition (e.g., using MountEFI):  
   https://github.com/corpnewt/MountEFI
4. Clone this repository.
5. Copy the EFI folder from this repo to the USB’s EFI partition.
6. Boot from the USB stick and install macOS.

## Wi‑Fi Notes (Important for macOS Tahoe)

macOS 15 (Tahoe) does not support AirportItlwm.kext.

This EFI uses:

- itlwm_v2.3.0_stable.kext  
- HeliPort.app (required for Wi‑Fi control)

How to enable Wi‑Fi:

1. Boot macOS  
2. Install HeliPort.app from:  
   https://github.com/OpenIntelWireless/HeliPort/releases  
3. Reboot twice  
4. Open HeliPort and connect to your Wi‑Fi network

The macOS Wi‑Fi menu will not work. This is expected.

## BIOS Settings

- BIOS Version: 2K211028
- Enable iGPU
- Disable Secure Boot
- Disable Fast Boot
- SATA Mode: AHCI
- Boot Mode: UEFI only

## Troubleshooting
OpenCore not appearing in BIOS after you copy to HD EFI
under Windows CMD Admin : bcdedit /set {bootmgr} path \EFI\OC\OpenCore.efi


## Credits

- farcop for the original EFI  
- OpenCore team  
- OpenIntelWireless (itlwm / HeliPort)  
- Dortania guides
- Copilot and Chatgpt for config and debug help