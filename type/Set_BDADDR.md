# Set Bluetooth Device Address (BD_ADDR)

## Security-relevance

When performing a Machine-in-the-Middle (MitM) attack (such as with WHAD[1]), if the intended victim is using Bluetooth Classic or BLE Public addresses, it may be necessary to spoof the victim's address on one of the MitM interfaces. Therefore VSCs which aid in changing the BD_ADDR of a device, aid in performing MitM attacks.

[1] [One for all and all for WHAD: wireless shenanigans made easy!](https://darkmentor.com/bt.html#One%20for%20all%20and%20all%20for%20WHAD%3A%20wireless%20shenanigans%20made%20easy!) by Damien Caquile & Romain Cayre

## Vendors with VSC present

* [Broadcom](../vendor/Broadcom.md)
* [Cambridge Silicon Radio (CSR)](../vendor/CSR.md)
* [Cypress](../vendor/Cypress.md) (Purchased by Infineon)
* [Espressif](../vendor/Espressif.md)
* [Silicon Labs](../vendor/SiliconLabs.md)
* [Texas Instruments](../vendor/TexasInstruments.md)