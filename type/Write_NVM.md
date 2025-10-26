# Write Controller Non-volatile Memory (e.g. SPI NOR Flash)

## Security-relevance

The capability for someone on the host to write non-volatile memory (NVM), such as SPI NOR flash, can aid in reverse engineering the Controller code on platforms where all or part of the firmware is stored in NVM as in [1][2]. It can also lead to the capability to install persistent malicious  capabilities in the firmware, if the chip in question does not have secure boot. ([3] is an example of persistent malicious modification, however NVM write was achieved via an over-the-air exploit of the secure update system, rather than via a VSC. And the title of the talk is a misnomer as the chip in question does not have secure boot.)

[1] [InternalBlue a Bluetooth Experimentation Framework Based on Mobile Device Reverse Engineering](https://darkmentor.com/bt.html#InternalBlue%20a%20Bluetooth%20Experimentation%20Framework%20Based%20on%20Mobile%20Device%20Reverse%20Engineering) by Dennis Mantz  
[2] [Finding New Bluetooth Low Energy Exploits via Reverse Engineering Multiple Vendors' Firmwares](https://darkmentor.com/bt.html#Finding%20New%20Bluetooth%20Low%20Energy%20Exploits%20via%20Reverse%20Engineering%20Multiple%20Vendors'%20Firmwares:%5B%5BFinding%20New%20Bluetooth%20Low%20Energy%20Exploits%20via%20Reverse%20Engineering%20Multiple%20Vendors'%20Firmwares%5D%5D%20%5B%5BBluetooth%20Security%20Timeline%5D%5D%20%24%3A%2FTagManager) by Veronica Kovah   
[3] [Breaking Secure Boot on the Silicon Labs Gecko platform](https://darkmentor.com/bt.html#Breaking%20Secure%20Boot%20on%20the%20Silicon%20Labs%20Gecko%20platform) by Sami Babigeon & Benoît Forgette  

## Vendors with VSC present

* [Broadcom](../vendor/Broadcom.md)
* [Espressif](../vendor/Espressif.md)
* [Texas Instruments](../vendor/TexasInstruments.md)
