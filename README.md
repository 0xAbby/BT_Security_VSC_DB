# Purpose of this repository

This repository contains information about Bluetooth HCI Vendor-Specific Commands (VSCs) which are known to be security-relevant, as found across different vendors. The currently tracked VSC types of security interest are given below, along with a description of why they are security-relevant. It also documents the Vendor-Specific Events (VSEs) and their formats (when known), which are returned by a controller after a VSC is received.

* [Read Controller Registers](./type/Read_Regs.md)
* [Write Controller Registers](./type/Write_Regs.md)
* [Read Controller RAM](./type/Read_RAM.md)
* [Write Controller RAM](./type/Write_RAM.md)
* [Read Controller ROM](./type/Read_ROM.md)
* [Write Controller ROM Patches](./type/Write_ROM_Patches.md)
* [Read Controller Non-volatile Memory (e.g. SPI NOR Flash)](./type/Read_NVM.md)
* [Write Controller Non-volatile Memory (e.g. SPI NOR Flash)](./type/Write_NVM.md)
* [Set Bluetooth Classic / BLE Public BD_ADDR](./type/Set_BDADDR.md)
* [Set TX power level](./type/Set_TX_Power.md)
* [Send arbitrary LMP packets](./type/Send_LMP.md)
* [Send arbitrary LLCP packets](./type/Send_LLCP.md)

These are not all possible security-relevant VSCs, but they are some of those most commonly found across chip-makers.

## Known VSCs, organized by vendor

* [Broadcom](./vendor/Broadcom.md)
* [Cambridge Silicon Radio (CSR)](./vendor/CSR.md)
* [Cypress](./vendor/Cypress.md) (Purchased by Infineon)
* [Espressif](./vendor/Espressif.md)
* [Qualcomm](./vendor/Qualcomm.md)
* [Realtek](./vendor/Realtek.md)
* [Silicon Labs](./vendor/SiliconLabs.md)
* [Texas Instruments](./vendor/TexasInstruments.md)
