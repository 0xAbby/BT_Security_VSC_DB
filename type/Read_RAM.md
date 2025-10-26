# Read Controller RAM

## Security-relevance

The capability for someone on the host to read RAM can aid in reverse engineering the Controller code as in [1][2][3][4]. It can also aid in creating a debugging-like system which aid in the creation of over-the-air memory-corruption exploits, as in [2].

[1] [InternalBlue a Bluetooth Experimentation Framework Based on Mobile Device Reverse Engineering](https://darkmentor.com/bt.html#InternalBlue%20a%20Bluetooth%20Experimentation%20Framework%20Based%20on%20Mobile%20Device%20Reverse%20Engineering) by Dennis Mantz  
[2] [Finding New Bluetooth Low Energy Exploits via Reverse Engineering Multiple Vendors' Firmwares](https://darkmentor.com/bt.html#Finding%20New%20Bluetooth%20Low%20Energy%20Exploits%20via%20Reverse%20Engineering%20Multiple%20Vendors'%20Firmwares:%5B%5BFinding%20New%20Bluetooth%20Low%20Energy%20Exploits%20via%20Reverse%20Engineering%20Multiple%20Vendors'%20Firmwares%5D%5D%20%5B%5BBluetooth%20Security%20Timeline%5D%5D%20%24%3A%2FTagManager) by Veronica Kovah  
[3] [Attacking Bluetooth the easy way](https://darkmentor.com/bt.html#Attacking%20Bluetooth%20the%20easy%20way) by Antonio Vázquez Blanco & Miguel Tarascó Acuña  
[4] [Reverse engineering Realtek RTL8761B* Bluetooth chips, to make better Bluetooth security tools & classes]() by Xeno Kovah & Veronica Kovah  

## Vendors with VSC present

* [Broadcom](../vendor/Broadcom.md)
* [Cypress](../vendor/Cypress.md)
* [Espressif](../vendor/Espressif.md)
* [Realtek](../vendor/Realtek.md)
* [Texas Instruments](../vendor/TexasInstruments.md)
